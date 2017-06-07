---
layout: notes
title: Heaps
class: CS 1332
---

A heap is a data structure that only keeps track of the greatest, or the least, element contained in it.
* There are two types of heaps
	1. **Min heap:** Keeps track of the smallest element in the heap
	2. **Max heap:** Keeps track of the largest element in the heap
* Properties of a heap:
	* **Order Property:** The parent node is always smaller than the children (in a min heap), and always larger than the children (in a max heap)
	* **Shape Property:** A heap is always complete, which means that every level of a heap is filled, except from the bottom, which is filled from left to right
	* None of the elements except the root can be accessed
* We can thus implement heaps with arrays
	* Skip the first element, leaving heap[0] empty
	* If index is the index of the parent, the children of each element will be at heap[index * 2] and heap[index * 2 + 1]
* Adding
	* Steps:
		1. Add the new item into the next open slot in the array
		2. Compare the newly added element to its parent. If the order property is broken, swap the parent and the child
		3. Repeat step 2 until we reach the root, or until we stop making swaps
	* Pseudocode:
	```python
	def add(data):
		index = length(heap)
		heap[index] = data
		parentIndex = index / 2
		# This next part differs depending on if its a min heap or a max heap
		# This implementation is of a max heap
		while parentIndex > 1 && heap[parentIndex] < heap[index]:
			swap(heap[parentIndex], heap[index])
			index = parentIndex
			parentIndex /= 2
	```
* Removing
	* Steps
		1. Remove the root
		2. Move the item at the last spot to the heap of the root
		3. Compare this item with its left and right child. If it breaks the order property with either one, swap the child with the parent
		4. Repeat step 3 until you either reach the bottom or you stop making swaps
	* Pseudocode
	```python
	def remove():
		index = length(heap)
		data = heap[1]
		heap[1] = heap[index]
		heap[index] = None
		index = 1
		oneMoreHeapify = True
		while heap[index] has child && oneMoreHeapify:
			oneMoreHeapify = False
			# Again, this depends on whether we are using a max heap or a min heap
			# This implementation is of a max heap
			if heap[index] > heap[index * 2]:
				swap(heap[index], heap[index * 2])
				index *= 2
				oneMoreHeapify = True
			elif heap[index] > heap[index * 2 + 1]:
				swap(heap[index], heap[index * 2 + 1])
				index = index * 2 + 1
				oneMoreHeapify = True
		return data
	```
* Cases
	1. Adding
		1. **Best Case:** O(1)
		2. **Average Case:** O(log n)
		3. **Worst Case:** O(log n)
	2. Removing
		1. **Best Case:** O(log n)
		2. **Average Case:** O(log n)
		3. **Worst Case:** O(log n)

### Priority Queue:
A data structure that, when given a list of items, returns them in either ascending or descending order
* Most common application for a heap