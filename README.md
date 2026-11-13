1. Objectives

The purpose of this lab is to implement a complete system allowing the multiplication of 2 numbers. This entails reading hardcoded values from ROM, performing intermediate buffering and arithmetic, and finally outputting previously calculated values on the Basys 3’s seven segment display. Doing so requires the implementation of a control unit module to oversee the system’s progression using state machine logic.

2. Introduction

Although this system requires decently complicated logic to perform the desired multiplication, we were able to reuse a number of previously written modules to simplify the design process. These included the SevenSegDisplay module (containing all necessary submodules to output data to the boards 7SD), ROM (8 line, 4-bit width) and RAM (8-line, 8-bit width) modules, and MultiplierCombinational module (performs the multiplication of 2 4-bit binary numbers to produce an 8-bit result).

The first new file we wrote was the RegFile module, a simple module allowing 2 values to be held prior to multiplication. Because our ROM module only permits a single value to be read per clock cycle, this module was essential in ensuring both the correct multiplier and multiplicand were available for the multiplier at once.

The most complex of the three new modules was the ControlUnit module. This module contained the system’s FSM logic, dictating which actions were allowed to be taken at any given time. It uses 5 states, S0_idle (an idle state),  S1_read_rom1 (to read the first value from ROM), S2_read_rom2 (to read the second value from ROM), S3_write_ram (to calculate and commit the new product to ram), and S4_read_ram (to read any of the stored products from RAM). To allow previously stored values to be read, S4 remains in place until either or both of the ROM addresses are updated. To read an older RAM value, one can simply update the current RAM address to read its value. Additionally, this module sends signals to RegFile and RAM dictating permission to overwrite current data. To the RegFile specifically, it dictates both which register new data is written to and which register stored data is read from.

Lastly, we joined each submodule into a single top module for implementation and testing. With just 2 ROM addresses, 1 RAM address, a clock signal, and 7SD outputs for I/O, it allows 2 numbers to be read from ROM, multiplied, stored to RAM, and displayed on the 7SD.


3. Instructions for simulation and FPGA implementation

  Simulation: 

    a. Create a project in vivavdo containing all of these files.

    b. Select the desired testbench file and corresponding design file as the top modules.

    c. Run simulation and view waveform.

  FPGA implementation:

    a. Create a project in vivavdo containing all of these files.

    b. Select the design file "top.v" as the top module.

    c. Generate the bitstream and connect to FPGA board.

    d. SW[2:0] represent rom_adr1[2:0], SW[5:3] represent rom_adr2[2:0], SW[8:6] represent ram_adr[2:0], and SW[9] represents the rst signal.

    e. First select the the RAM address you would like to write to.

    f. Then select the ROM addresses of the inputs you would like.

    g. Before writing a new product make sure you first select the new RAM address before changing either of the input ROM addresses.

    h. When reading back results, DO NOT change any other inputs besides the RAM address you would like to read. Changing either ROM address will overwrite previously stored results at current selected location. 

5. Additional Soures

https://hilite.me/ - Used to format Appendix code in Lab Report
