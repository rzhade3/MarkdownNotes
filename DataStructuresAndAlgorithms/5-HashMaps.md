---
layout: notes
title: Maps
class: CS 1332
---

A map is a data structure where, for each value, there is a key mapping to it
* Usually, the keys are unique, while the values can be duplicate
* They can be implemented with either Arraylists or LinkedLists, resulting in O(n) efficiency

### HashMaps
A hashmap is a type of map in which the hashcode of the key is used to find the index into which the mapping is put
* Generally, it is implemented with an array
* Index Calculation:
	* To find the index in which the item will be put, we use hashcode(key) % length of the backing array
* Load Factor:
	* Hash maps have a load factor, which determines when the array should be resized
	* Calculation:
		* Load Factor = numEntries / array.length
	* Once the load factor exceeds the value that was predetermined, we resize the backing array
* Collision Resolution Methods:
	* Since we are modding the hashcode, it is possible that two keys go to the same index
	* There are multiple ways to resolve collisions
		1. **Linear Probing:** If there is already a item at index i, go to index i + 1, until we find something empty
		2. **Quadratic Probing:** If there is already a item at index i, go to index i + 1^2, until we find something empty
		3. **External Linking:** Have a collection of nodes at each index, and every time there is a collision, add the item as a linked list
* The rest of the implementation depends on which of the collision resolution methods is used
* Cases:
	1. **Best Case:** O(1)
	2. **Average Case:** O(1)
	3. **Worst Case:** O(n)