# Memory
To do any sort of action on a computer, we need to load and store stuff in memory.


## Memory Addressing
To load operands into registers so we can perform operations on them, we must first load them into registers. We do this using *memory addressing*

* **Base + Offset Mode:** Addressing a memory as the sum of contents in a register with an offset
	* We can use the PC, or any register that we want

### Granularity


## Storage
Since we need to address the memory somehow, we can use *word addressing* to load larger bits of memory at a time

### Endianness
Endianness refers to how the bytes are ordered within the word. There are two types of endianness
* **Little Endianness:** Least significant bit is first in the word
	* Backwards in memory
* **Big Endianness:** Most significant bit is last in the word

### Memory Alignment
Since different things might be different sizes in memory, this can create problems in a word addressable system

> Word addressable systems create a tradeoff between memory efficiency and time efficiency of calling memory

![Misaligned Memory Alignment](https://www.geeksforgeeks.org/wp-content/uploads/MemoryAlignment2.gif)

There are two ways that computers deal with storing memory:
* **Packing:** The compiler stuffs all memory into the first given spot in memory
	* Can store more stuff, as there is no wastage of memory
	* Slower to access something, as the memory might spill over across words


## Important Stuff
* For large data structures/ arrays, we cannot store the entire thing in a register. Thus, we keep this in memory and address it one array element at a time