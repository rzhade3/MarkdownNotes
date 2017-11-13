---
layout: notes
title: Lists
class: CS 1332
---

* A list is a data structure that stores data in a persistent order, the order in the user defines
* Compare this to a set, which has no user defined ordering
There are several ways to implement this data structure, but the two most important are those backed by:
1. Arrays --> ArrayLists
2. Nodes --> LinkedLists

### Arraylists
* A resizing array, so capacity keeps changing
* If there is no more room to add, we need to resize the array
	* Usually, we resize arrays to (size * 2) + 1
* Resizing Pseudocode:
```python
def regrow(arr):
	newArr = [None] * (len(arr) * 2 + 1)
	for i in len(arr):
		newArr[i] = arr[i]
	arr = newArr
```
* Adding
	* To add, first we must check if the capacity is enough
	* Then, we move everything to the right of the index over one index
	* Finally, add the element at the given index
	* Change the size
* Adding Pseudocode:
```python
def add(index, element):
	if size >= len(arr):
		regrow(arr)
	for j in range(size - 1, index)
		arr[j + 1] = arr[j]
	arr[index] = element
	size += 1
```
* Removing
	* Move everything to the right of the index over one
	* Change the size
* Removing Pseudocode:
```python
def remove(index):
	item = arr[index]
	for j in range(i, size - 2)
		arr[j] = arr[j + 1]
	size -= 1
	return item
```
* Cases
	1. Accessing:
		 * **Best Case:** O(1)
		 * **Average Case:** O(1)
		 * **Worst Case:** O(1)
	2. Inserting:
		* **Best Case:** O(n)
		* **Average Case:** O(n)
		* **Worst Case:** O(n) 
	3. Searching:
		* **Best Case:** O(n)
		* **Average Case:** O(n)
		* **Worst Case:** O(n) 
	4. Removing:
		* **Best Case:** O(n)
		* **Average Case:** O(n)
		* **Worst Case:** O(n) 

### Linked Lists
* A data structure that consists of a sequence of nodes
* Two main types, based on how the nodes are set up
	i. Singly Linked Lists have nodes that only contain references to the next node
	There will only be a head pointer in this case
	ii. Doubly Linked Lists have nodes that contain references to the previous and next node.
	There will be a head and a tail pointer in this case
* There are also circularly linked lists, in which the tail node is connected to the head node
* Inserting Pseudocode:
```python
def addFirst(element)
	node = new Node(element, head)
	head = node
	if len(list) == 0:
		tail = node
	size += 1

def addLast(element):
	node = new Node(element, null)
	if len(list) == 0:
		head = node
	else:
		tail.next = node
	tail = node
	size += 1
```
* Removing Pseudocode:
```python
def removeFirst():
	node = head
	head = head.next
	size -= 1
	return node.data

def removeLast():
	node = head
	for i in range(size - 1):
		node = node.getNext()
	temp = node.getNext()
	node.setNext(null)
	return temp.data
```
* Cases:
	1. Accessing:
		* **Best Case:** O(n)
		* **Average Case:** O(n)
		* **Worst Case:** O(n) 
	2. Searching:
		* **Best Case:** O(n)
		* **Average Case:** O(n)
		* **Worst Case:** O(n) 
	3. Adding:
		* **Best Case:** O(1)
		* **Average Case:** O(n)
		* **Worst Case:** O(n) 
	4. Removing:
		* **Best Case:** O(1)
		* **Average Case:** O(n)
		* **Worst Case:** O(n) 

### Skip Lists
This is pretty much a linked list with multiple levels, to reduce the Big O of finding an element
* Skip lists can only be used with elements that have an inherent ordering
* Features
	* Nodex are arranged from least to most, with a node representing negative infinity on the left, and a node representing positive infinity on the right. 
	* Nodes are randomly promoted up "levels"
		* If the randomness is a coin flip, the node is promoted as many times as the coin comes up heads. If the coin comes up tails, we stop promoting
* Searching
	* Steps:
		1. Start at the top left of the list
		2. Check the data in the node to the right
			* If the data that we are looking for is less than the data in the node or there is no node there, go down a level
			* If the data that we are looking for is greater than the data in the node, go to that node
			* If the data that we are looking for is equal to the data in the node, we have found it
		3. Repeat step two until we either find the node or we go off the list
	* Pseudocode:
	```python
	def search(data, node):
		if node == None:
			return False
		else:
			while data > node.next.data:
				node = node.next
			if data = node.next.data:
				return True
			else:
				return search(data, node.down)
	```
* Adding
	* Steps:
		1. Use the coin flipper to find how many times the data will be promoted
		2. If there aren't enough levels for the new item, create the new levels
		3. Follow the same steps as searching until we find where the node should go. Once we find the location, add the node at this location, then move down a level
		4. Repeat step 3 until we get to the bottom
	* Pseudocode:
	```python
	def add(data, levels, node, upperNode):
		if node == None:
			return
		else:
			while data > node.next.data:
				node = node.next
			if node.level <= levels:
				Node temp = new node(data)
				temp.next = node.next
				node.next = temp
				node.up = upperNode
				upperNode = temp
			add(data, levels, node.down, upperNode)
	```
* Removing
	* Steps:
		i. Follow the same steps as searching until we find the node, or go off the list
		ii. Disconnect the node from the rest of the nodes at this level, and go down a level
		iii. Repeat step 2 until we go off the list
		iv. Remove any empty levels
	* Pseudocode:
	```python
	def remove(data, node):
		if node == None:
			return
		else:
			while data > node.next.data:
				node = node.next
			if data == node.next.data:
				remove(node.next)
				# Remove empty levels here
			else:
				remove(data, node.down)

	def remove(node):
		while node != None:
			# Remove node from this level
			node = node.down
	```
* Cases:
	1. Searching
		1. **Best Case:** O(log n)
		2. **Average case:** O(log n)
		3. **Worst case:** O(n)
	2. Adding
		1. **Best Case:** O(log n)
		2. **Average case:** O(log n)
		3. **Worst case:** O(n)
	3. Removing
		1. **Best Case:** O(log n)
		2. **Average case:** O(log n)
		3. **Worst case:** O(n)
	4. **Space Complexity:** O(n log n)
