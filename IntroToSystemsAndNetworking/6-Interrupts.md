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
    *

## Dealing with Program Discontinuities
**Tricky Situations with Discontinuities:**
1. They can happen anywhere during instruction execution.
2. Unplanned discontinuity occurs and could be unrelated to the program.
3. Hardware has to determine the address of the handler to transfer control from the program to the handler.
4. Since hardware has saved PC implicitly, handler has to discover how to resume normal program execution.

