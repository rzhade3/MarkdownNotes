# Interrupts

## Synchronous Vs Asynchronous Activities

### Definition
* **Synchronous:** An event that occurs with respect to the rest of the program, at well- defined points of time
* **Asynchronous:** An event that occurs unexpectedly, without respect to ongoing activities in the system

There are three types of discontinuities in program execution:

* **Interrupts:** Mechanism by which devices catch the attention of the processor
	* Externally generated
	* Asynchronous
* **Exceptions:** When programs perform illegal operations, and we need to discontinue the original sequence of instructions
	* Internally generated
	* Synchronous
* **Traps:** When programs make system calls for File I/O or other services from system
	* Internally generated
	* Synchronous

## Dealing with Program Discontinuities
