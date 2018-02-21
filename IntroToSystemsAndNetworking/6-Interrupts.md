# Interrupts

## Synchronous Vs Asynchronous Activities

### Definition
* **Synchronous:** An event that occurs with respect to the rest of the program, at well- defined points of time
* **Asynchronous:** An event that occurs unexpectedly, without respect to ongoing activities in the system

There are three types of discontinuities in program execution:

* **Interrupts:** Mechanism by which devices catch the attention of the processor
	* Externally generated
	* Asynchronous
    * Examples: I/O Device Completion
* **Exceptions:** When programs perform illegal operations, and we need to discontinue the original sequence of instructions
	* Internally generated
	* Synchronous
    * Examples: Overflow, Divide by zero, Illegal memory address
* **Traps:** When programs make system calls for File I/O or other services from system
	* Internally generated
	* Synchronous
    * Examples: System call, software interrupts, page fault, emulated instructions

## Dealing with Program Discontinuities
* **Handler:** Procedure that is executed when a discontinuity occurs

Since program discontinuities happen at any time, there are four things that are tricky
1. Can happen anytime during program execution, even in the middle of an instruction
2. Can be unplanned, and completely unrelated to the current program
3. When the program notes the program discontinuity, the hardware needs to determine the address of the handler
4. The handler needs to be able to return back to normal program execution

To handle different types of interrupts, the OS uses a ***Interrupt Vector Table***
* Holds handler addresses for each of the interrupt instructions

