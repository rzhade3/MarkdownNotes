# Processor Implementation
We need abstraction between the processor level and instruction level for a number of reasons:
* Different implementations of the same architecture, for the same processor
* To allow for parallel development of software and hardware
* There needs to be support for legacy software

To this end, we have a particular set of hardware that can work reasonably work with most ISAs.


## Hardware Resources
* Circuits
	* **Combinational Logic:** Stateless logic, done with basic logic gates
		* Output only depends on inputs
	* **Sequential Logic:** Stateful logic, done with flip flops
		* Output is some combination of boolean operations on current state and inputs
		* Include Registers and Memory
* Hardware Resources
	* **Memory:** To store instructions and operands
	* **ALU:** To do arithmetic and logic instructions
	* **Register File:** Since instructions use registers to perform operations
	* **Program Counter:** To point to current instruction, and to implement jump and branch
	* **Instruction Register:** To hold the current instructions
* Clock Cycles
	* The clock works by cycling power on and off

	![Clock Cycles](http://image.slidesharecdn.com/interrupts-100920105212-phpapp01/95/interrupts-15-728.jpg?cb=1284980027)
	* With level logic, changes in state happen whever the clock is high
		* Changes either happen on *rising edge* or *falling edge*
* Hardware Resources

### Processor Design Issues:
