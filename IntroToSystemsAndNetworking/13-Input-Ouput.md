# Input/Output and Stable Storage

## Introduction

I/O devices communicate to the CPU through a device controller.

### Keyboard Controller
* **Data Register:** Storage space for character typed on keyboard
* **Status Register:** Holds the current state of information exchange between keyboard and CPU.

The state in the status register contains:
* **Ready Bit:** Is the char in the data register not seen by the processor yet? This is set by the device.
* **Interrupt Enable (IE):** Is the processor allowing the interrupt to enable it?
* **Interrupt Flag (IF):** Is the controller ready to interrupt the processor?

The CPU sets the IE bit, checks for new data, and reads the data.

### Memory Mapped I/O
![Image](images/mappedmemory.png)
In the above diagram, the processor reads and writes to memory using load and store instructions. This technique is known as memory mapped I/O. It allows interaction between the CPU (processor) and the device controller without causing any change to the processor.

In this case of the **data** and **status** registers, the processor views them as memory locations. These registers are given unique memory addresses. High memory addresses are reserved for I/O device registers.

The advantage of memory mapped I/O is that no special I/O instructions are required, but a disadvanatge is that a portion of memory address space is lost to device registers.

## Programmed I/O

This refers to the moving of data back and forth between a device and a processor.

* **Polling:** Processor continually checking if the device has new data.
* **Interrupt:** Enabling interrupt bit for a device upon an interrupt.

Polling and interrupt work for slow-speed devices that produce data asynchronously (data production is not rhythmic). However, programmed I/O doesn't work for high-speed devices like disks that produce data synchronously. Even for slow speed devices, programmed I/O is an inefficient use of the processor's resources.
