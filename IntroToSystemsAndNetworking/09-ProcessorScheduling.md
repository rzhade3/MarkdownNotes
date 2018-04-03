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
Metrics can be either *system centric* or *user centric*

| Name | Notation | Units | Centricity | Description |
|-----|-----|-----|-----|-----|
| CPU Utilization | - | % | User | Percent of time that the CPU is busy |
| Throughput | n / T | Jobs / sec | System | Metric quantifying the number of jobs n executed in time interval T |
| Avg. Turnaround time | (t1 + t2 + ... + tn) / n | Seconds | System | Metric quantifying the average time it takes for a job to complete |
| Avg. Waiting time | ((t1-e1) + (t2-e2) + ... + (tn-en)) / n | Seconds | System | Metric quantifying the average waiting time that a job experiences |
| Response time/ turnaround time | t*i* | Seconds | User | metric quantifying the turnaround time for a specific job *i* | 
| Variance in Response time | E[(ti – ei)^2] | Seconds^2 | User | metric that quantifies the statistical variance of the actual response time (ti) experienced by a process (Pi) from the expected value (tavg) |
| Starvation | - | - | User | Qualitative metric that signifies denial of service to a particular process or a set of processes due to some intrinsic property of the scheduler |
| Convoy effect | - | - | User | Qualitative metric that results in a detrimental effect to some set of processes due to some intrinsic property of the scheduler |

Below is an example of scheduling metrics

![Sigmoid function](images/example_metrics.png)

### Types of Scheduling
| Name | Preemptive | Starvation | Convoy Effect |
| ---- | ---------- | ---------- | ------------- |
| First Come First Serve | No(Yes) | No | Yes |
| Shortest Job First | No(Yes) | Yes | No |
| Priority | Yes/No | sometimes | sometimes |
| Shortest Remaining Job First | Yes | Yes | No | 
| Round Robin | Yes | No | No | 

