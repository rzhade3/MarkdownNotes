---
layout: notes
title: Sorting
class: CS 1332
---

There are two major distinctions that are made for sorting algorithms
1. Stability
   Stability refers to how the algorithm handles duplicate values
	* Stable
		Stable algorithms preserve the order of duplicate values
	* Unstable
		Unstable algorithms do not preserve the order of duplicate values
2. Place
	Place refers to how much memory the algorithm takes up
	* In place
	* Out of Place

### Bubble Sort
* Stable, and in place
* Steps:
	1. Compare the first two items. If they aren't in the right order, swap them. If not, keep them as is. Move to the right one index.
	2. Repeat the above until you get to the end. 
	3. Repeat the above two steps, but don't go to the end each time. Make the window smaller by one each time.
	4. If you do not make any swaps during one cycle of step 2, you can terminate early.
* Pseudocode:
```python
def bubbleSort(array):
	i = 0
	swapped = True
	while i < len(array) - 1 and swapped:
		swapped = False
		for j in range(len(array) - i - 1):
			if array[j] > array[j + 1]:
				swap(array[j], array[j + 1])
				swapped = True
	return array
```
* Cases:
	* The best case is O(n)
	* All other cases are O(n^2)

### Insertion Sort
* Stable and in place
* Pseudocode:
```python
def insertionSort(array):
	for i in range(1, len(array) - 1):
		j = i
		while j > 0 and array[j - 1] > array[j]:
			swap(array[j - 1], array[j])
			j -= 1
	return array
```
* Cases:
	* The best case is O(n)
	* All other cases are O(n^2)

### Cocktail Shaker sort
* Two passthroughs of bubble sort per iteration
	* Do one pass of bubble sort going towards the right, then one pass of bubble sort going to the left
* In each iteration, the window that is sorted gets smaller
	* After first passthrough, we know that the last element is sorted. After second passthrough, we know that first element is sorted, and so on.
* Same Big O as the other two, but is on average, twice as fast as the other two.
* Stable and in place

### Selection Sort
* Unstable and in place
* Pseudocode:
```python
def selectionSort(array):
	for i in range(len(array)):
		minIndex = i
		for j in range(i, len(array) - 1):
			if array[j] < array[minIndex]:
				minIndex = j
		swap(array[minIndex], array[i])
	return array
```
* Cases:
	* All cases for selection sort are O(n^2)

### Merge Sort
* Stable, but out of place
* Recursive implementation
* Pseudocode:
```python
def mergeSort(array):
	length = len(array)
	if length == 1:
		return array
	midIndex = length // 2
	leftArray = array[0::midIndex - 1]
	rightArray = array[midIndex::length - 1]
	mergeSort(leftArray)
	mergeSort(rightArray)
	leftIndex = 0
	rightIndex = 0
	currentIndex = 0
	while leftIndex < midIndex and rightIndex < length - midIndex:
		if leftArray[leftIndex] < rightArray[rightIndex]:
			array[currentIndex] = leftArray[leftIndex]
			leftIndex += 1
		else:
			array[currentIndex] = rightArray[rightIndex]
			rightIndex += 1
		currentIndex += 1
	while leftIndex < midIndex:
		array[currentIndex] = leftArray[leftIndex]
		leftIndex += 1
		currentIndex += 1
	while rightIndex < length - midIndex:
		array[currentIndex] = rightArray[rightIndex]
		rightIndex += 1
		currentIndex += 1
	return array
```
* Cases:
	* In all cases, merge sort is O(n log n)

### Quick Sort
* Unstable, but in place
* Pseudocode:
```python
def quickSort(array):
	return quickSort(array, 0, len(array))

def quickSort(array, left, right):
	if len(array) == 1:
		return array
	pivotIndex = random(left - right) + right
	pivot = array[pivotIndex]
	swap(array[left], array[pivotIndex])
	leftIndex = left + 1
	rightIndex = right - 1
	while leftIndex < rightIndex:
		while leftIndex < rightIndex and array[leftIndex] <= pivot:
			leftIndex += 1
		while leftIndex < rightIndex and array[rightIndex] >= pivot:
			rightIndex -= 1
		if leftIndex < rightIndex:
			swap(array[leftIndex], array[rightIndex])
			leftIndex += 1
			rightIndex -= 1
	swap(array[left], array[rightIndex])
	quickSort(array, left, rightIndex - 1)
	quickSort(array, rightIndex + 1, right)
```
* Cases:
	* In the best case, and average case, quicksort is O(n log n)
	* In the worst case, quicksort is O(n^2)

### LSD Radix Sort
* Stable, but out of place
```python
def lsdRadixSort(array):
	buckets = list() * 10
	iterations = len(max(array))
	length = len(array)
	for i in range(1, iterations):
		for j in range(length - 1):
			bucket = ith digit of array[j]
			buckets[bucket].append(array[j])
		index = 0
		for bucket in buckets:
			while len(bucket) != 0:
				array[index] = bucket.pop()
				index += 1
	return array
```
* Cases:
	* In all cases, LSD is O(kn), where k is the length of the longest number

### MSD Radix Sort
* Unstable and out of place
```python
def msdRadixSort(array):
	buckets = list() * 10
	iterations = len(max(array))
	length = len(array)
	return array
```