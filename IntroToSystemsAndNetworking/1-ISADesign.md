# Processor and ISA Design

Before the advent of modern programming languages, most code was written in assembly, and thus processor design was more of a hardware issue. However, as most modern code needs to be compiled, there became a need for processors to be dictated by the ISA. 


## Instructions
A single instruction is one that performs some elementary operation for the computer
* Don't need to interface directly with the hardware this way

Instructions can be viewed in two ways:
* **Microstate:** One clock cycle of the instruction
* **Macrostate:** The entire instruction, until completion
An instruction will have several microstates, but only one macrostate, while a program will have several macrostates

### Instruction Set
The *Instruction Set* is the particular set of instructions for any computer
* The ISA for any computer is stored within the ROM

There are two main types of Instruction Set Architectures:
* **CISC (Complex Instruction Set Computers):** ISAs built for completing a task with the least lines of assembly as possible
	* Come with a larger set of instructions, esp. those that can be made with simpler instructions
		* E.g. will have a MULT instruction
	* Advantage that compilers will have to do less work to translate a high level language to assembly
* **RISC (Reduced Instruction Set Computers):**
	* Have smaller set of instructions
		* Typically only the most fundamental instructions
	* Advantage that ISA takes less memory in RAM

	
## Compilers
A compiler for any modern computing language works by translating the high level language into assembly code that the computer can use.

> All high level languages have arithmetic/ logical expressions and assignment statements

 An important thing to note about high level languages are operands.

E.g.
```java
int n = a + b;
int q = a + 4;
```

The purpose of a compiler is to translate this into machine readable language. So, somehow, we must encode this information into machine code.

Clearly there are three different operands in each statement above. Where do we store these operands, and how do we access them?

### Addressing Mode
Elementary operations are all done in the ALU. However, where do we keep the operands on which we perform the operations?

> Operands are stored in registers so we don't need to address them in memory

Most processors use *register addressing* to **store** and **load** operands to perform actions on them

To load the values that we want into the registers, we use *memory addressing*