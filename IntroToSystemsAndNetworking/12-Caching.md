# Caching


## Terminology
**Cache:** A component that stores data so future requests for that data can be served faster.

**SRAM vs DRAM:** SRAM (static RAM) supports higher speed but larger size, whereas DRAM (dynamic RAM) supports larger size but lower speed.

**Hit:** When the CPU finds the contents of the memory address in the cache, saving a trip to the deeper levels of memory hierarchy

**Hit Rate (h):** Probability of a hit occuring

**Miss:** When the CPU fails to find the contents of the memory address in the cache, incurring a trip to the deeper levels of memory hierarchy

**Miss Rate (m):** The probability of a miss occuring (1 - h)

**Miss Penalty:** Time penalty associated with servicing a miss at any level of the memory hierarchy

**Memory Hierarchy:** The storage containing either instructions and/or data that a processor accesses either directly or indirectly.

### Locality
* **Spatial:** High probability of a program accessing *adjacent* memory locations.
* **Temporal:** High probability of a program accessing the *same* memory location.



### EMAT
EMAT is the effective memory access time, or the effective access time experienced by the CPU.

This is calculated by EMAT of L = Access time of L + (m * EMAT of L below OR miss penalty)

The miss penalty is used to calculate the EMAT of the level right above the main memory.

## Cache Organization
Three facets to cache organization:
1. **Placement:** Where do we place the data read from memory in the cache?
2. **Lookup Algorithm:** How do we find something placed in the cache?
3. **Validity:** Is the data in the cache valid?

### Misses
1. **Compulsory:** When the cache is first accessed (it's empty)
2. **Capacity:** Cache is full and miss is incurred
3. **Conflict:** Due to limited associativity, even though cache isn't full

Precedence of misses is in the above order.

## Direct-Mapped
There is a one-to-one correspondance between a cache location and a memory location.

## Caching and Pipelining
I-MEM and D-MEM are replaced with I-Cache and D-Cache.
* **Miss in the IF Stage:** IF stage sends the reference to memory to retrieve this instruction. Until this happens, the processor sends NOPs to the next stage.
* **Miss in the MEM Stage:** Only happens for load/store. MEM sends NOPs to WB till the memory reference completes. It also freezes the previous instructions from advancing.

## Calculations
- block offset = log2(B) (B = Block Size)
- Lines of Cache = S/B (S = Total Size of Cache)
- index bits (n) = log2(L)
- tag = a - (b + n) (a = total address size of cache)

1. Consider a multiworld direct-mapped cache with data size of 64KB. The CPU generates a 32-bit byte-addressable memory address. Each memory word
contains four bytes. The block size is 16 bytes. The cache uses a write-back policy with one dirty bit per word. The cache has one valid bit per data block.
a. how does the CPU interpret the memory address

Block Size = B = 16 bytes

b = log2(16) = 4

L = 64 KB/16 bytes = 4096

n = log2(4096) = 12

t = a - (n + b) = 32 - (12 + 4) = 16

b. compute the total amount of storage for implementing the cache (actual data + metadata)

Data = 16 bytes x 8bits/byte = 128 bits

Valid Bit = 1 bit

Dirty Bits = 4 bits (1 bit for each word)

Tag = 16 bits

Total = 149 bits

149 x 4096 (number of cache lines) = 610,304 bits

The space requirement for metadata = total space - actual data

= 610,304 - 64KB

= 610, 304 - 524,288

= 86,016

The space overhead = metadata/total space = 86,016/610,304 = 14%







