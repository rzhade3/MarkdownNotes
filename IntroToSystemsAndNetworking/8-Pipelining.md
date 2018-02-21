# Pipelining

The basic idea behind pipelining is using the hardware resources in the processor all the time. Comparing it to our old datapath, if we have three instructions, we would Fetch the first, while Decoding the second and Executing the third.

## Instruction Pipeline:

### The Five Functional Stages:
1. **IF:** This fetches the instruction pointed to by the PC from I-MEM and places it into IR. It also increments the PC to be ready to fetch the next instruction. For this stage, we need the PC, ALU and I-MEM.
2. **ID/RR:** This decodes the instruction and reads the register files to pull out two source operands. For this stage, we need the DPRF(Dual Ported Register File).
3. **EX:** This does all the arithmetic and/or logic operations needed to process the instruction. This stage requires at most two ALUs.
4. **MEM:** This reads or writes from D-MEM if instructions require them (LW and SW). This requires the D-MEM.
5. **WB:** This writes to the appropriate destination register (Rx). This requires the DPRF.


## Pipeline-Conscious Architecture

***Desigining a Pipeline-Conscious Architecture:***
1. **Need for a symmetric instruction format:** This means that locations of certain fields in the instruction (reg specifiers, offset size) remain unchanged independent of the instruction.
2. **Need to ensure equal amount of work in each stage:** Ensures that clock cycle time is optimal since the slowest member of the pipeline determines it.