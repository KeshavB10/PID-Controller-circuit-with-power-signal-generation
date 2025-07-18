module PID_top(
    input clk,
    input pwm_clk,
    input reset,
    input signed [7:0] set_point,
    input signed [7:0] digital_in,
    output power_out,
    output signed [9:0] control_signal
);

    wire signed [9:0] pid_control_signal;

    // Instantiate PID Controller in clk domain
    PID_Controller PID (
        .clk(clk),
        .reset(reset),
        .set_point(set_point),
        .in(digital_in),
        .out(pid_control_signal)
    );

    // Directly drive PWM with pid_control_signal (assumes domain crossing is safe)
    PWM PWM (
        .clk(pwm_clk),
        .reset(reset),
        .control_signal(pid_control_signal),
        .out(power_out)
    );

    assign control_signal = pid_control_signal;

endmodule
