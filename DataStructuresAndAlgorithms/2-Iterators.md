---
layout: notes
title: Iterators
class: CS 1332
---

* An iterator is a special class that allows a user to traverse a data structure
* They typically have three methods:
	1. Get the current item
	2. Go to next item
	3. Go to previous item
* The data structure typically implements its own iterator, as an inner/ private class

### Iterators in Java
* In Java, each data structure will implement the `java.lang.Iterator` interface.
* The data structure would also implement the `java.lang.Iterable` interface, which has one method `iterable()`, that returns a new iterator object
* `java.lang.Iterator` methods
	* **hasNext():** Returns a boolean representing whether there is another item in the structure
	* **next():** Returns the next item in the structure
	* **remove():** An optional method that returns the most recently returned element
* `java.lang.Iterable` methods
	* **iterator():** returns a new iterator object
* Instead of directly using the iterator object, Java lets us use a for each loop.
	* Java implicitly uses the iterator for the data structure, returning items as the iterator defines
* We can make fancy iterators, like an iterator for preorder/ postorder/ inorder in a BST