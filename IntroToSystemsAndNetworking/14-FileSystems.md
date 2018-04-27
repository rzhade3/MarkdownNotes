# File Systems
Until now, we dealt with how hardware interfaces with software and vice versa. But how does the software organizes things within itself?

## Introduction

### Definition
* **File System:** A way of interfacing with I/O and maintaining the hard disk in the computer
* **File:** The software abstraction for an input/output device, since a device serves as either a source or sink of information
* **Metadata:** The attributes associated with a file

### Metadata
To organize files, the computer associates a set of values with each file:

| Attribute | Meaning |
| ---- | --- |
| Name | Name of the file |
| Alias | Other names for file |
| Owner | The person that created file |
| Creation Time | Time when file was created |
| Last Write Time | Time when file was last written to |
| Privileges | Permissions or access rights |
| Size | Total space occupied on file system |
| I- node | **Explained later** |

* Name: Can be used to implement hierarchical file structure
		* I.e. /Users/me/Documents/HelloWorld.txt is a name
* Access Rights: Include: *read, write, execute, change ownership, change privileges*

### Linking of Files
Aliasing causes files to be "linked"
* **Hard Link**
	* ```ln foo bar```
	* *bar*, points directly to the index in table that *foo* points to
	* This means that *foo* and *bar* are the same file, not two copies of a file
	* If you delete *foo*, *bar* will still exists
	* Both of these files have the same i-node
* **Soft Link**
	* ```ln -s foo bar```
	* A soft link means that the file is a true alias
	* The original name of the file is saved in the aliasing of the file
	* I-node is different
	* Lookup is in a different table, that is at the address located to by the i-node
	* Table is a reference to the original file (ie. if file is at /usr/tmp/foo, then /usr/tmp/foo is stored at the location in the page table)

## Storage Design Techniques
### Considerations
Different implementations for the filesystem have different merits and demerits
* Ideally, want to optimize the time spent by the head to find something on the disk
	* Related to *seek time*, rotation latency
* Five metrics to look at:
	* Fast Sequential Access
	* Fast random access
	* Ability to Grow file
	* Easy allocation of storage
	* Efficiency of space utilization

### Design Techniques
* Contiguous Access
	* A list of data blocks assigned to a program
	* A program is only given a data block that is sufficient for it, if it needs to grow we have problems
	* Lot of external and internal fragmentation
		* When a diskblock returns to the free list, system may compact adjacent nodes to create one larger node, however uncommon, as its too complex
	* Very Good for Sequential and Random Access
	* Bad for growing files
	* Medium to High Overhead
* Contiguous Access With overflow
 	* Same as LinkedList implementation except that it has some space allocated for overflow of a program
 	* Very good Sequential and Random Access for small files
* Linked Allocation
	* Each file in the file system has an address to the first memory address (the head) of the linked list
	* As the file grows it adds (a disk block from the free list) on to its already allocated Disk Blocks, adding to the end of a LinkedList
	* Each disk block has a pointer to the next disk block
	* Bad Random Access, Good Sequential Access (dependent on seek time)
	* very good file growth
* File Allocation Table
	* Table stored in memory that stores the location of the disk block in memory
	* For example a program has a start index associated with it
	* This start index is used to index into the FAT, this is the location of one disk block for that file
	* The index might have a number in the next column, this tells you where the next block of disk is locate in the FAT
	* If it is the last block, the next is set to -1
	* Good (dependent on seek time) Sequential and Random
	* Excellent Space Efficiency
* Indexed Allocation
	* Each file has its own i-node table
	* In the metadata for a file, the i-node is stored (this is the address at which the table begins)
	* The i-node table stores all the memory locations of the disk blocks currently in use by the file
	* This is better for Random Access since this aggregates all the blocks into on table, instead of having it spread out like in FAT
	* This method is not so good for increasing file size
		* Since i-node is a fixed size data structure for each file, that directly maps it to data blocks
		* Number of data block pointers is the maximum size of the file
	* Good (dependent on seek time) Sequential and Random
	* Excellent Space Efficiency
	- **Learn Calculation**
* Multi-Level Indexed Allocation
	* Added a level of abstraction
	* Each file points to an i-table address (same as before)
	* each i-table now contains address to more i-tables
	* these i-tables then are directly connected to data blocks
	* One level of abstraction
	* Can have as many as you want
	* Excellent Space Efficiency
	* Good (dependent on seek time) Sequential and Random
* Hybrid Allocation
	* each file has an address that points to the start of an i-table
	* this i-table has different types of indices that point to different types of indexed allocation
		* this i-table could directly point to memory
		* it could point to a single indirect table
		* a double indirect
		* or a triple indirect
	* Each level of abstraction allows you to have more and more data blocks allocated to a program
	* Good (dependent on seek time) Sequential and Random
	* Excellent Space Efficiency
	* **Learn Calculation** max file size, max file size of blocks, number of data blocks needed, number of index blocks needed

### I- node
- UNIX systems use a hybrid allocation strategy
- show the i-node for files in the directory that reference other files (hard or soft linking)
- a file will point to the same i-node table if it is a hard link
- if it is a soft link, it will point to its own i-node table which has the path to the file it is soft linking with
