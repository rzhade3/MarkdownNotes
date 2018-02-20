# Understanding Processor Performance
Processor design is quantitative, so we need ways by which to quantitatively analyze processors against one another


## Memory Footprints

* **CPI:** Clocks per Instruction
	* Number of clock cycles required per instruction

You can calculate execution time using the following equations, where *n* is the number of instructions:

Execution Time = $ (\sum CPI_{j}) * clock cycle time $, where $1 \leq j \leq n $

Or, you can calculate execution time by using the **average CPI**:

ExecutionTime = $ n * CPI_{avg} * clock cycle time $


## Instruction Frequency

**Instruction Frequency:** How often a particular instruction executes in a program

There are two types of *instruction frequencies:*
* **Static Instruction Frequency:** Number of times an instruction occurs in *compiled code*
* **Dynamic Instruction Frequency:** Number of times an instruction is executed when the *program is run*
	* Because of loops and branches, instruction might be executed multiple times, or none at all in running code

### Calculating
If there is a program with a hundred instructions, and one ADD instruction, but the ADD instruction occurs in a loop of length 5 that runs 50 times:
1. The static frequency would be $ 1/100 = 1% $.
2. The dynamic frequency would be calculated by the following:
3. Total instructions = $ (5 * 50) + (100 - 5) = 250 + 95 = 345 $
4. Number of ADD instructions = $ 50 $
5. Dynamic Frequency = $ 50/345 = 14.5% $$

## Benchmarks
Since execution time is not completely dependent on processor speed, we need some other way to compare processors against one another

**Benchmarks:** A set of programs representative of the processor's workload

Typically these benchmarks are the *kernels* of real programs, like a matrix multiply function or number of iterations of gradient descent. Using this, there are five ways to calculate 
1. **Total Execution Time:** Sum total of execution time for all programs
2. **Arithmetic Mean:** Normal mean of execution times for all programs
3. **Weighted Arithmetic Mean:** If we know the frequency
	* 
	* Useful if we know the ratio of instructions
4. **Geometric Mean:** Getting the p^th root of the product of the p values in the dataset
	* 
	* 
5. **Harmonic Mean:** Calculated by taking reciprocal of the arithmetic mean of reciprocals of all values
	* $ HM = 1 / arithmetic mean(reciprocals of all values) $
	* Useful when dataset contains a lot of ratios