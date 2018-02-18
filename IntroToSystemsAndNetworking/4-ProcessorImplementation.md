# Processor Implementation
We need abstraction between the processor level and instruction level for a number of reasons:
* Different implementations of the same architecture, for the same processor
* To allow for parallel development of software and hardware
* There needs to be support for legacy software

To this end,


## Hardware Resources
* Circuits
	* **Combinational Logic:** Stateless logic, done with basic logic gates
		* Output only depends on current inputs
	* **Sequential Logic:** Stateful logic, done with flip flops
* Hardware Resources