# Pipelining

The basic idea behind pipelining is using the hardware resources in the processor all the time. Comparing it to our old datapath, if we have three instructions, we would Fetch the first, while Decoding the second and Executing the third.

## Instruction Pipeline:

### The Five Functional Stages:
1. **IF:** This fetches the instruction pointed to by the PC from I-MEM and places it into IR. It also increments the PC to be ready to fetch the next instruction. For this stage, we need the PC, ALU and I-MEM.
2. **ID/RR:** This decodes the instruction and reads the register files to pull out two source operands. For this stage, we need the DPRF(Dual Ported Register File).
3. **EX:** This does all the arithmetic and/or logic operations needed to process the instruction. This stage requires at most two ALUs.
4. **MEM:** This reads or writes from D-MEM if instructions require them (LW and SW). This requires the D-MEM.
5. **WB:** This writes to the appropriate destination register (Rx). This requires the DPRF.

### Pipeline Buffers
1. **FBUF:** It is the output of *IF*, and contains instruction read from memory.
2. **DBUF:** It is the output of *ID/RR*, and contains the decoded IR and values read from the DPRF.
3. **EBUF:** It is the output of *EX*, and contains the result of the ALU operation plus any other parts of the instruction based on its specifics.
4. **MBUF:** It is the output of *MEM*, and contains the same as *EBUF* if the instruction is not *LW* or *SW*. If it is *LW*, it contains the contents of the memory location read.


## Pipeline-Conscious Architecture

***Desigining a Pipeline-Conscious Architecture:***
1. **Need for a symmetric instruction format:** This means that locations of certain fields in the instruction (reg specifiers, offset size) remain unchanged independent of the instruction.
2. **Need to ensure equal amount of work in each stage:** Ensures that clock cycle time is optimal since the slowest member of the pipeline determines it.

## Pipeline Hazards

Hazards reduce pipeline efficiency.

### Structural Hazards

This primarily comes about due to hardware limitations. Some examples could be a single bus or a single ALU. This can be fixed by adding a *feedback line*, which would tell previous stages to not send a different instruction and stay on the same instruction so that stage could finish the instruction it was on.

**Key Points:**
1. The pipeline is stalled when an instruction cannot proceed to the next stage.
2. The result of such stall is to introduce a bubble in the pipeline.
3. A NOP instruction is the bubble in the pipeline. A stage executing a NOP instruction does nothing for one cycle.

### Data Hazards
This can happen when there's a dependency between two instructions.
1. **RAW (Read After Write)**: This can be solved using data forwarding, by stalling the instruction that causes the *RAW* hazard in *ID/RR* till the register value is available.
2. **WAR (Write After Read)**
3. **WAW (Write After Write)**

### Control Hazards
Control hazards refer to the breaks in the program due to branch instructions.

1. **Conservative Approach:** We add one NOP if branch isn't taken, and two if branch is taken.
2. **Delayed Branch:** We assume that the instruction following the branch executes irrespective of the branch outcome. We put a NOP in the instruction following the branch instruction (delay slot). The smart compiler will insert useful instructions into these delay slots.
3. **Branch Prediction:**



