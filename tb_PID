module tb_PID_top;
    reg clk, pwm_clk, reset;
    reg signed [7:0] set_point, digital_in;
    wire power_out;
    wire signed [9:0] control_signal;

    // Instantiate top module
    PID_top uut (
        .clk(clk),
        .pwm_clk(pwm_clk),
        .reset(reset),
        .set_point(set_point),
        .digital_in(digital_in),
        .power_out(power_out),
        .control_signal(control_signal)
    );

    // Clock generation
    initial begin
        clk = 0;
        forever #100 clk = ~clk; // Period = 100 time units
    end

    initial begin
        pwm_clk = 0;
        forever #1 pwm_clk = ~pwm_clk; // Period = 2 time units
    end

    // Test stimulus
    initial begin
        // Initialize signals
        reset = 0;
        #5 reset=1;
        set_point = 8'd0;
        digital_in = 8'd0;
        #10;
        reset=0;
        #50;


        // Test case 1: set_point > digital_in
        set_point = 8'd100;
        digital_in = 8'd10;
        #3000;

        // Test case 1: set_point > digital_in
        set_point = 8'd100;
        digital_in = 8'd120;
        #3000;

        // Test case 1: set_point > digital_in
        set_point = 8'd100;
        digital_in = 8'd81;
        #3000;

        // Test case 1: set_point > digital_in
        set_point = 8'd100;
        digital_in = 8'd120;
        #3000;

        $finish;
    end

    // Monitor signals
    initial begin
        $monitor("Time=%0t, reset=%b, set_point=%d, digital_in=%d, control_signal=%d, power_out=%b",
                 $time, reset, set_point, digital_in, control_signal, power_out);

        $dumpfile("waveform_PID.vcd");
        $dumpvars(0,tb_PID_top);
    end
endmodule
