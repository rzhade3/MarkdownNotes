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








