# Processor Scheduling

A processor usually has several *programs* running at any time. How does the processor figure out how to allocate resources to each program?

### Basic Definitions
* **Program:** A set of instructions that makes a computer behave in some predetermined way
* **Process:** A program in execution
* **Address Space:** Space occupied in memory by the program
* **State:** The current contents of the address space and 
register values

| Name        | Connotation           | Use  |
| ------------- |:-------------:| -----:|
| Job      | Unit of Scheduling | Synonymous with process |
| Process      | Unit of scheduling      |   A job |
| Thread | Unit of scheduling/ execution; contained within process      |    All the information a CPU needs to execute a set of instructions |
| Task   | Unit of work, unit of scheduling| The promise of a job in the future |

As can be seen from above, **a process is a program plus all the threads that are executing in that program**


### Scheduling Environments
1. Multiprogrammed
	* Programs were cycled through the processor based on relative priority
	* Punch cards, manually entered by human operator
	* Code written in *job control language (JCL)*
2. Time sharing
	* Multiple interactive users, interfacing with data terminals and mini computers
	* An evolution of the multiprogrammed scheme, but requires automation in program scheduling

| Name	| Environment | Role  |
| ----- |:------------:|------:|
| Long Term Scheduler | Batch oriented OS | Control the job mix in memory to balance use of system resources (CPU, memory, I/O) |
| Loader | In every OS | Load user program from disk into memory |
| Medium Term Scheduler | Every modern OS | Balance the mix of processes in memory to avoid thrashing |
| Short Term Scheduler | Every modern OS | Schedule the memory resident processes on the CPU | 


### Basics of Scheduling
A typical program cycles between activity on the processor and I/O devices. 

* **CPU Burst:** The stretch of time a process runs without making an IO call
* **IO Burst:** The stretch of time a process needs to complete an IO operation

### Performance Metrics

### Types of Scheduling
1. First Come First Serve
2. Shortest Job First
3. 