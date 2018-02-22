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
* OS sets this up at boot time
* The **IVT** is kept in a location in memory known to the processor and the OS.

**Exception/Trap Register (ETR)**
* In the case of traps/execptions, the hardware generates this vector internally.
* This unique number associated with the exception/trap will be placed in the ETR.

### Interrupt Handler
An interrupt handler must do the following:
1. Save $k0
2. Enable interrupts
3. Save processor registers
4. Execute device code
5. Restore Processor Registers
6. Disable interrupts
7. Restore $k0
8. Return from interrupt (RTI)
    * Return to original program
    * PC <- $k0
    * Enable interrupts

## Hardware Details to Handle Program Discontinuities

### Datapath Details for Interrupts

Any device that wishes to interrupt the processor asserts the INT line. Upon an interrupt occuring, the processor asserts the INTA line. The INTA line is daisy chained between devices. The electrically closest device to the processor gets the INTA signal first. If the device has requested an intterupt, it knows the processor wants to talk to it, otherwise, it moves on to the next device.

Each distinct pair of INT and INTA lines corresponds to a *priority level*. Device priority is linked to device speed. This is because the higher the speed of the device, the higher the chance of data loss, and hence the need to give prompt attention to that device.

In modern processors the burden of determining which device needs attention is shifted to an external hardware unit called an *interrupt controller*.

### Receiving the Address of the Handler

The *IVT* contains the handler addresses for all the external interrupts. The device knows which table entry that contains its handler code. So, upon receiving the INTA signal from the processor, the device put its vector on the data bus. The processor uses this vector as the index to look up in the vector table and get the handler address, which is loaded into the PC.

A summary of this process is:
1. The device asserts the *INT* line when it's ready to interrupt the processor.
2. The processor upon completion of the instruction checks the *INT* line for pending interrupts.
3. If there is a pending interrupt, then the processor enters the *INT* macro-state and asserts the *INTA* line on the bus.
4. The device upon receiving the *INTA* from the processor, places its vector on the data bus.
5. The processor receives the vector and looks up the entry in the *IVT*. This is the PC value that needs to be executed for the interrupt.
6. The processor completes the action in the *INT* macro-state, saving the current PC into $k0, and loading the PC with the value from (5).

### Stacks
The issue arises with the handler not knowing which part of memory is to be used as a stack. To fix this, it's usual to have two stacks, the **user stack** and **system stack**. Upon entering the *INT* macro-state, the FSM performs *stack switching*.

***Hardware Enhancements Required:***
* **Duplicate Stack Pointers**: We need to duplicate the register designated by the architecture as the stack pointer.
* **Privileged Mode**: We need to let the processor know which version of $sp to use, so we have a *mode* bit in the processor. The processor is either in *user* or *kernel* mode.

The *mode* bit ensures that only the OS can operate the *privileged instructions* such as writing to $k0, and enabling and disabling interrupts.

## Interrupt Macrostates
### INT Macrostate
1. $k0 <- PC
2. ACK INT by asserting INTA
3. Receive interrupt vector from data bus
4. Retrieved address of handler from IVT
5. PC <- handler address
6. Save current mode on system stack
7. mode = kernel (no-op if mode is already kernel)
8. Disable Interrupts

### RETI Macrostate
1. Load PC from $k0
2. Restore mode from system stack
3. Enable Interrupts






