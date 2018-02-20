# Pipelining

## Performance Metrics

### Execution Time

CPI: Clocks per Instruction

You can calculate execution time using the following equations, where n is the number of instructions:
Execution Time = $(\sum CPI_{j}) * clock cycle time $, where $1 \leq j \leq n$
Or, you can calculate execution time by using the average CPI:
ExecutionTime = $n * CPI_{avg} * clock cycle time$

### Instruction Frequency

**Instruction Frequency:** How often a particular instruction executes in a program

**Static Instruction Frequency:** The number of times an instruction occurs in compiled code

**Dynamic Instruction Frequency:** The number of times an instruction is executed when the program is ran

For example, if there is a program with a hundred instructions with one ADD instruction, but the ADD instruction occurs in a loop of length 5 that runs 50 times, there would be a difference in static and dynamic frequency.

The static frequency would be $1/100 = 1%$.
The dynamic frequency would be calculated by the following:
$$ Total instructions = (5 * 50) + (100 - 5) = 250 + 95 = 345$$
$$ Number of ADD instructions = 50$$
$$Dynamic Frequency = 50/345 = 14.5%$$

### Speedup
The speedup of processor A over processor B can be calculated using the following formula.
$$ Speedup_{A over B} = \frac{Execution Time of B}{Execution Time of A}

### Amdahl's Law

## Benchmarks

**Benchmarks:** A set of programs representative of the processor's workload.

## Process Performance

**Ways to Improve Peformance:**
1. Increasing Clock Speed
2. Lower CPI (Datapath Organization)
3. Reduction in number of executed instructions

All the three aformentioned optimizations cannot be done in isolation, and they must be done simultaneously, as they affect each other.

