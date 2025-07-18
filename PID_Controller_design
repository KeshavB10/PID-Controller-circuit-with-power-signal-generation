module PID_Controller(clk,reset,in,set_point,out);
    input clk,reset;
    input signed [7:0] in,set_point;
    output signed [9:0] out;

    parameter kp = 8'd1;
    parameter ki =8'd1;
    parameter kd =8'd1;

    parameter INTEGRAL_MAX=100;
    parameter INTEGRAL_MIN=-100;

    reg signed [7:0] error,prev_error;
    reg signed [15:0] integral=0;
    reg signed [15:0] derivative=0;
    reg signed [9:0] control_signal;

    reg signed [15:0] control_signal_temp;

    assign out=control_signal;

    /*-----------------------GOAL-------------------------*/

    //Control signal=0 ==> duty cycle=50%

    /*control signal>0 ==> set_point > in ==> increase power to circuit 
     ==> PWM pusle width (and hence duty cycle) increases*/

    /*control signal<0 ==> set_point < in ==> decrease power to circuit 
     ==> PWM pusle width (and hence duty cycle) decreases*/

    always @(posedge clk or posedge reset) begin //synchronous reset
        if (reset) begin
            error <=0;
            prev_error<=0;
            integral <=0;
            derivative <=0;
            control_signal <=0;
        
        end
        else begin
            error <= set_point-in;
            integral <= integral + (error);
            if (integral>INTEGRAL_MAX)
                integral<=INTEGRAL_MAX;
            else if (integral<INTEGRAL_MIN)
                integral<=INTEGRAL_MIN;

            derivative <= error - prev_error;
            control_signal_temp <= (kp*error) + (ki*integral) + (kd * derivative);
            if (control_signal_temp>511) 
                control_signal <=511;
            else if (control_signal_temp<-512)
                control_signal<=-512;
            else 
                control_signal <= control_signal_temp[10:0];
            prev_error<=error;
        end
    end

endmodule
