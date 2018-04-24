# Chapter 11 File Systems
- These notes will not be too in-depth, these should be used as a guide for the important things from the chapter


# Introduction
- The file system is a way of interfacing with I/O and maintaining the hard disk in the computer
- Each file has metadata attached to it
  - i-node (index into a file management table (explained later))
  - permissions bit-vector (tells you who has what permissions)
  - access list (tells you who can access the file)
  - data created
  - name
- Linking of Files
  - **Hard Link**
	- hard link ```ln foo bar```
	- this is linking bar to foo
	- a hard link means, bar, points directly to the index in table that foo points to
	- this means that foo and bar are the same file, not two copies of a file
	- if you delete foo, bar will still exists
	- in the i-table there is a refcount that keeps track of how many references there is to a particular i-node (in the table)
	- both of these files have the same i-node
  - **Soft Link**
  	- ```ln -s foo bar```
  	- a soft link means that the file is a true alias
  	- the original name of the file is saved in the aliasing of the file
  	- The i-node is different
  	- this means that this lookup is in a different table, that is at the address located to by the i-node
  	- What is stored in the table is a reference to the original file (ie.if the file is at /usr/tmp/foo, then /usr/tmp/foo is stored at the location in the page table)
# Storage for Techniques
- What we need to optimize for a good technique
	- we need to optimize the time spent by the head to find something on the disk
		- this is related to seek time, rotational latency, transfer time, DMA transfer time
	- User might want to look at the files in a directory sequentially **Sequential Access**
	- User might want to search for something in file **Random Access**
	- we want a technique that has:
		- Fast Sequential Access
		- Fast Random Access
		- Ability to grow the file
		- Easy Allocation of Storage
		- Efficiency of Space Utilization on the Disk
- Contiguous Access
	- This is just a list of data blocks assigned to a program
	- a program is only given a data block that is sufficient for it, if it needs to grow we have problems
	- lot of external and internal fragmentation
	- the FreeList is also a LinkedList
	- When a diskblock returns to the free list the system may compact adjacent nodes to create one large node
		- however it rarely does this cause its too complex
	- Very Good for Sequential and Random Access
	- Bad for growing files
	- Medium to High Overhead
	- **Learn Calculation**
- Contiguous Access w/ overflow
 	- this is the same as LinkedList implementation except that it has some space allocated for overflow of a program
 	- Very good Sequential and Random Access for small files
- Linked Allocation
	- Each file in the file system has an address to the first memory address (the head) of the linked list
	- as the file grows it adds (a disk block from the free list) on to its already allocated Disk Blocks, adding to the end of a LinkedList
	- each disk block has a pointer to the next disk block
	- Bad Random Access, Good Sequential Access (dependent on seek time)
	- very good file growth
- File Allocation Table
	- Table stored in memory that stores the location of the disk block in memory
	- For example a program has a start index associated with it
	- This start index is used to index into the FAT, this is the location of one disk block for that file
	- The index might have a number in the next column, this tells you where the next block of disk is locate in the FAT
	- If it is the last block, the next is set to -1
	- Good (dependent on seek time) Sequential and Random
	- Excellent Space Efficiency
- Indexed Allocation
	- Each file has its own i-node table
	- In the metadata for a file, the i-node is stored (this is the address at which the table begins)
	- The i-node table stores all the memory locations of the disk blocks currently in use by the file
	- This is better for Random Access since this aggregates all the blocks into on table, instead of having it spread out like in FAT
	- This method is not so good for increasing file size
		- since i-node is a fixed size data structure for each file, that directly maps it to data blocks
		- the number of data block pointers is the maximum size of the file
	- Good (dependent on seek time) Sequential and Random
	- Excellent Space Efficiency
	- **Learn Calculation**
- Multi-Level Indexed Allocation
	- Added a level of abstraction
	- Each file points to an i-table address (same as before)
	- each i-table now contains address to more i-tables
	- these i-tables then are directly connected to data blocks
	- this is one level of abstraction
	- you can have as many as you want
	- Excellent Space Efficiency
	- Good (dependent on seek time) Sequential and Random
- Hybrid Allocation
	- each file has an address that points to the start of an i-table
	- this i-table has different types of indices that point to different types of indexed allocation
		- this i-table could directly point to memory
		- it could point to a single indirect table
		- a double indirect
		- or a triple indirect
	- Each level of abstraction allows you to have more and more data blocks allocated to a program
	- Good (dependent on seek time) Sequential and Random
	- Excellent Space Efficiency
	- **Learn Calculation** max file size, max file size of blocks, number of data blocks needed, number of index blocks needed
- UNIX systems use a hybrid allocation strategy
- show the i-node for files in the directory that reference other files (hard or soft linking)
- a file will point to the same i-node table if it is a hard link
- if it is a soft link, it will point to its own i-node table which has the path to the file it is soft linking with