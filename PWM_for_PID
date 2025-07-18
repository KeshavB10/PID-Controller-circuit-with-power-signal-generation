module PWM(clk,reset,control_signal,out);
    input clk,reset;
    input signed [9:0] control_signal;
    output reg out;

    //PWM drives the actuator

    //NOTE control signal=0 => 50% duty cycle (present clock power is enough to drive)

    reg [7:0] counter;
    wire [7:0] duty_cycle;
    wire signed [10:0]duty_temp;
    
    assign duty_temp=11'sd1024+control_signal;
    assign duty_cycle=(duty_temp<0)?10'd0:
                        (duty_temp>1023)? 10'd1023:
                       duty_temp[7:0];

    always @ (posedge clk or posedge reset) begin //synchronous reset
        if (reset) begin
            counter<=8'b0;
        end

        else if (counter==10'd1023)
              counter=8'd0;

        else begin
            counter<=counter+8'd1;
        end
    end
    always @ (posedge clk or posedge reset) begin
        if (reset)
            out <=1'b0;
        else begin
            out <=(counter<=duty_cycle)?(1'b1):(1'b0);
        end
    end
endmodule

