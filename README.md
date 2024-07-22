# Pipelined-Multiplier
Try this example to understand how Pipelining is done in Hardware Designs.

To run simulation:
1. Clone the repo
2. Open Modelsim.
3. Go to Files -> Change Directory in Modelsim.
4. Choose the Design_Files directory.
5. In the Console, enter the command - "do sim.do"

RTL View of the Pipelinedd Multiplier

![RTL View](https://github.com/Satvik3799/Pipelined-Multiplier/blob/main/Images/RTL%20View.png)

Klayout

![Klayout](https://github.com/Satvik3799/Pipelined-Multiplier/blob/main/Images/Klayout.png)


# Built-In Self-Test (BIST) Module with LFSR and MISR for Multiplier Verification

This repository contains a Verilog implementation of a Built-In Self-Test (BIST) system that uses Linear Feedback Shift Register (LFSR) and Multiple Input Signature Register (MISR) to generate and verify inputs for a multiplier module. The BIST system ensures that the multiplier module produces correct results by comparing the outputs against expected values.

## Modules

### LFSR (Linear Feedback Shift Register)
The LFSR module generates an 8-bit pseudo-random sequence using the polynomial x^8 + x^6 + x^5 + x^4 + 1.

### MISR (Multiple Input Signature Register)
The MISR module captures the output of the multiplier and compresses it into an 8-bit signature to verify correctness.

### Multiplier
The multiplier module performs multiplication of two 8-bit inputs and produces a 16-bit output.

### BIST (Built-In Self-Test)
The BIST module integrates the LFSR, MISR, and Multiplier modules. It generates test vectors using LFSR, applies them to the Multiplier, and verifies the results using MISR.

### Top Module
The Top module instantiates the BIST module and provides the interface for the overall system.

## File Structure

- `LFSR.v`: Verilog code for the LFSR module.
- `misr_8bit.v`: Verilog code for the MISR module.
- `multiplier.v`: Verilog code for the Multiplier module.
- `BIST.v`: Verilog code for the BIST module.
- `Top.v`: Verilog code for the Top module.

## How to Use

1. **Clone the repository:**
    ```sh
    git clone https://github.com/yourusername/bist-multiplier.git
    cd bist-multiplier
    ```

2. **Compile and simulate the Verilog code using your preferred simulation tool (e.g., ModelSim, Vivado, etc.).**

3. **Check the outputs:**
    - `lfsr_out`: Output of the LFSR used as input for the multiplier.
    - `result`: Output of the multiplier.
    - `bist_pass`: Indicates if the BIST passed (1) or failed (0).

## Example

Here's an example instantiation of the Top module:
```verilog
module Top (
    input wire clk,
    input wire rst,
    output wire bist_pass
);

    wire [7:0] lfsr_out;
    wire [15:0] result;

    // Instantiate BIST module
    BIST bist_inst (
        .clk(clk),
        .rst(rst),
        .lfsr_out(lfsr_out),
        .result(result),
        .bist_pass(bist_pass)
    );

endmodule
