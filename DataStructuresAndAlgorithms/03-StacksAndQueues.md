---
layout: notes
title: Stacks and Queues
class: CS 1332
---

### Queues
* A First in First out data structure
	* Insertions are at the rear, and removals are at the front. DO NOT perform any functions at any other point in the queue
* Two main methods
	* Enqueue(object):- Inserts an element at the end of the queue
	* Dequeue():- Removes and returns the element at the front of the queue
* Pseudocode for Enqueue:
```python
def enqueueArrayList(object):
	arr.add(size - 1, object)
	size += 1

def enqueueLinkedList(object):
	addLast(object)
	size += 1
```
* Pseudocode for Dequeue:
```python
def dequeueArrayList():
	size -= 1
	return arr.remove(size - 1)

def dequeueLinkedList():
	size -= 1
	return removeFirst()
```
* Cases:
	* For ArrayList backed queues:
		1. **Enqueue:** amortized O(1)
		2. **Dequeue:** O(1)
	* For LinkedList backed queues:
		1. **Enqueue:** O(1)
		2. **Dequeue:** O(1)

### Stacks
* A First in Last out data structure
* Two main methods
	* Push(object): Inserts the element 
	* Pop: Returns the last added element
* Push adds an element to the stack
	* Typically, we add the element to the back of the Arraylist/ LinkedList
* Pseudocode for Push:
```python
def pushArrayList(element):
	arr.add(size, element)

def pushLinkedList(element):
	list.addLast(element)
```
* Pop removes the last added element
	* This means, that we typically also remove from the back as well
* Pseudocode for Pop:
```python
def popArrayList():
	size -= 1
	item = arr[size]
	arr[size] = null
	return item

def popLinkedList():
	size -= 1
	return list.removeFirst()
```
* Cases:
	* For ArrayList backed stacks
		* Push is amortized O(1)
		* Pop is O(1)
	* For LinkedList backed stacks
		* Push is O(n)
		* Pop is O(n)

### Deques
* A deque is another name for a 'double ended queue'
	* Basically, this is a queue for which items can be added or removed from both the front and the back
* O(1) for everything regarding this
