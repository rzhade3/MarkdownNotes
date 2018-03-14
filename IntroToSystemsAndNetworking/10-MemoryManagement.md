# 2200 Lecture on Memory Management (Project 3)

* What is memory management?
    * We want to make sure memory is utilized properly
* Goals of Memory Management
    1. Improved Resource Utilization
    2. Independence and Protection
    3. Liberation from resource limitations
    4. Sharing among Processes
        * Implicit
        * Explicit
* To Manage Memory Introduce a Broker, that is between CPU and Memory
    * The Broker is in hardware but its functionality is set by the software
* Simple Management
    * Fence Register (only OS can mess with it)
    * Fence Register checks the value of the CPU generated address
    * We actualy have two Fence registers, one for the lower bound and the upper bound
    * These bounds are set by the OS and differentiate between Kernel and User Memory
    * This gives isolation and protection
```C
    typedef struct control_block_type {
        ...
        address LB;
        address UB;
        ...
    }
```
* Limitations of "Bound" Register Mechanism
    * relocation not possible
    * recall swapping
    * you cant bring P1 back because all the bounds are hard coded
* Make P1 dynamically relocatable
    * dont hard code addresses in executable
    * set memory bounds at load time rather than link time
* Dynamically Relocatable MultiProgrammed OS
    * Instead of an upper and lower bound fence register, have a base and limit register
    * you add the base to the CPU generated address and then use the limit register to change this into a memory address
    * this allows you to swap in different programs in and out of memory

## Memory Allocation by OS
* Fixed Size Partition
* Variable Size Partition
    - all of these policies assume the hardware support is Base + Limit Register (because this gives us dynamic memory allocation)
* PCB is the data structure for the scheduler
* Allocation Table = Data Structure of OS Memory Manager
```C
struct At_Entry {
    int occupied;
    int size;
    int pid;
}
```
* The table tells you the memory is divied up and based on the size of a program, whether you can or can not allocate the process to that address in memory
* if some entry in the table is being used, but not all the size is being used then you internally fragment the memory
* if you internally fragment two places in memory, (lets say index 0 and 2 add up to 4k) and you need 4k for a program, you cannot allocate a program that is 4k to this because it is not continous memory
* This is called External Fragmentation, total memory that is unallocated but is not contigious
* Virtue of Fixed Size Memory
    - simplicity
    - bad news
        - fragmentation
        - external and internal
* How to overcome internal fragmentation?
    * allocate exactly what is needed
    * variable size partition
        * the allocation table is now, start address, size, and process
        * as you go along you partition the memory based on how much is needed for a process
        * when you free some process in the middle you coalesce it with adjacent blocks of memory and then you get a bigger chunk and the size of the allocation table shrinks
        * compaction, if you have some process in the middle of free memory, rellocate P3 and coalesce the free memory
        * problem is that compaction is very expensive
        * no internal fragmentation with variable size partition
* How to solve external fragmentation problem?
    * have a new broker
    * this maps virtual address (From CPU) to physical address (to memory)
    * CPU -> VA -> Broker -> PA -> MEM
    * This broker is some sort of lookup table that is set by the OS
    * how big is this table?
        * in the limit
            * as big as address apce
            ..but this is not feasible
        * concept of a page of continous address
        * kind of like a picture frame, where you can reuse for different pictures (physical page)
        * virtual page can be put into any physical page
* Paging and Virtual Memory
    * Page Table is in the Broker
    * CPU -> VA -> Broker (Page Table) -> PA -> MEM
    * The broker is the hardware mechanism (lookup table)
    * given a virtual page I tell you the physical page
    * users view is still the same, all these pages are contigious
* Address Translation
    * CPU -> VPN | Page Offset
    * this is the virtual address
* Memory System with 32-bit virtual adress, assume page size is 8k BYtes
    * how big is page table?
        * size of offset is 13 bits (0 - 12)
        * VPN is 32 - 13 bits = 19 bits
* Consider a memory system with 32-bit virtual addresses and 24-bit physical memory address. Assume that the pagesize is 4K bytes
    * How many Page frames in memory
        - 2^20 page table entries
        - offset is 12 bits

# Paging
* Virtual Pages map to Physical Frames (in memory)
* given a virtual address we can break it up into virtual page number and an offset (this will map too a page frame number and an offset)
* 32 bit vritual address; 28 bit physical memory address; 4 KB page size; 8 processes currently executing:
    * How many entried in the PT?
        * 2^20
        * reason is because in 32 bit address with a page size of 4k (12 bits of offset) out of 32 bits 12 bits are offset, 2^VPN = entries in page table (2^20)
    * How many page frames in memory?
        * 2^16
        * 28 bit physical address, 12 bits are offset, 16 bits remaining = VPN -> 2^16 frames in memory
    * How many page tables in memory?
        * 8
* Paged Memory Allocation
    * Allocate all at once at load time?
    * Allocate on demand?