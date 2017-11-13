---
layout: notes
title: Trees
class: CS 1332
---

A tree is a recursively implemented data structure that has multiple levels, consisting of linked nodes
* Terminology:
    * **Root Node:** The topmost node
    * **Internal Node:** A node with at least one child
    * **Leaf Node/ External Node:** A node with no children
    * **Parent Node:** The node directly above a node
    * **Ancestors:** The parents, grandparents, etc. of a node
    * **Children:** Nodes immediately below a node
    * **Descendants:** The children, grandchildren, etc. of a node
    * **Height:** Maximum number of nodes needed to be traversed to reach a leaf node from here (bottom up)
    * **Depth:**  Maximum number of nodes needed to be traversed to reach the root from here (top down)
    * **Subtree:** Tree consisting of a node and all its descendants in order

### Binary Trees
A tree whose nodes can have up to 2 children, left and right
* There's no relation between any of the nodes, so any searching, adding or removing is always O(n)
* To optimize functionality, we use special kinds of binary trees:

### Binary Search Trees
A type of binary tree where each left node is smaller than the parent, and every right node is larger than the parent
* Searching:
    * Steps:
        1. Start at the root node
        2. Check the data in the node
            * If the data we are looking for is less than this, go to the left child
            * If the data we are looking for is greater than this, go to the right child
            * If the data is equal, we have found the node
        3. Repeat step 2 until we find the node, or go off the tree
    * Pseudocode:
    ```python
    def search(data, node):
        if node == None:
            return False
        if data < node.data:
            return search(data, node.left)
        elif data > node.data:
            return search(data, node.right)
        else:
            return True
    ```
* Adding:
    * Steps:
        1. Follow the same steps as searching until we find the data in a node, or reach a leaf node
        2. If the data is not in the tree, add a new node to the leaf as either the left or right child
        3. If the data is in the tree, typically we do nothing. However, this is implementation defined
    * Pseudocode:
    ```python
    def add(data, node):
        if node == None:
            return new Node(data)
        if data < node.data:
            node.left = add(data, node.left)
        elif data > node.data:
            node.right = add(data, node.right)
        else:
            # Implementation defined behavior
        return node
    ```
* Removing:
    * Terminology
        * **Predecessor:** The node that has the largest data but is smaller than the data in the current node (rightmost left node)
        * **Successor** The node that has the smallest data but is larger than the data in the current node (leftmost right node)
    * Steps:
        i. Follow the same steps as searching until we find the data in the tree, or go off the tree
        ii. Once we find the node, 
            * If the node has no children, simply remove the node
            * If the node has one child, that child node takes the place of the parent node
            * If the node has two children, then either the predecessor or the successor takes the place of the node
    * Pseudocode:
    ```python
    def remove(data, node):
        if node == None:
            # The data isn't in the tree
        else:
            if data == node.data:
                # Remove the data according to the rules defined above
            elif data < node.data:
                node.left = remove(data, node.left)
            else: 
                node.right = remove(data, node.right)
            return node
    ```
* Traversals:
    1. Preorder: Visit the node, then its left node, then its right node
    * Pseudocode
        ```python
        def preorder(node, list):
            if node != None:
                list.add(node)
                preorder(node.left)
                preorder(node.right)
            return list
        ```
    2. Postorder: Visit the left node, then the right node, then the node itself
    * Pseudocode
    ```python
    def postorder(node, list):
        if node != None:
            postorder(node.left)
            postorder(node.right)
            list.add(node)
        return list
    ```
    3. Inorder: Visit the left node, then the node itself, then the right node
    * Pseudocode
    ```python
    def inorder(node, list):
        if node == None:
            inorder(node.left)
            list.add(node)
            inorder(node.right)
        return list
    ```
* Cases:
    1. Searching:
        * **Best Case:** O(1)
        * **Average Case:** O(log n)
        * **Worst Case:** O(n)
    2. Adding:
        * **Best Case:** O(log n)
        * **Average Case:** O(log n)
        * **Worst Case:** O(n)
    3. Removing:
        * **Best Case:** O(log n)
        * **Average Case:** O(log n)
        * **Worst Case:** O(n)

### AVL Trees
A type of binary search tree that rebalances itself to prevent it form becoming degenerate
* Properties
    * **Balance Factor:** The height of the left child node minus the height of the right child
    * If the balance factor is greater than 1 or less than -1, then we rotate the tree until it is fixed
* Rotations
    1. Left Rotation
        * If the balance factor of a node is -2
        * Pseudocode
        ```python
        def leftRotation(node):
            Node temp = node.right
            node.left = temp.left
            temp.left = node
            # update height and balance factor of node
            # update height and balance factor of temp
            return temp
        ```
    2. Right Rotation
        * If the balance factor of a node is 2
        * Pseudocode
        ```python
        def rightRotation(node):
            Node temp = node.left
            node.right = temp.right
            temp.right = node
            # update height and balance factor of node
            # update height and balance factor of temp
            return temp
        ```
    3. Left- Right Rotation
        * If the balance factor of a node is 2, and the balance factor of its child is -1
        * Pseudocode
        ```python
        def leftRightRotation(node):
            node.left = leftRotation(node.left)
            return rightRotation(node)
        ```
    4. Right- Left Rotation
        * If the balance factor of a node is -2, and the balance factor of its child is 1
        * Pseudocode
        ```python
        def rightLeftRotation(node):
            node.right = rightRotation(node.right)
            return leftRotation(node)
        ```
* Adding
    * Adding is just like adding in a BST, but while we move back up the tree, we rebalance
    * Pseudocode:
    ```python
    def add(data, node):
        if node == None:
            return new Node(data)
        else:
            if data == node.data:
                # Implementation defined behavior
            elif data < node.data
                node.left = add(data, node.left)
            else:
                node.right = add(data, node.right)
            updateHeightAndBalanceFactors(node)
            if node.isUnbalanced:
                balance node
                updateHeightAndBalanceFactors(node)
            return node
    ```
* Removing
    * Removing is done like the add method, but keeping track of variables with dummy nodes
* Cases:
    1. Accessing
        * **Best Case:** O(log n)
        * **Average Case:** O(log n)
        * **Worst Case:** O(log n)
    2. Adding:
        * **Best Case:** O(log n)
        * **Average Case:** O(log n)
        * **Worst Case:** O(log n)
    4. Removing:
        * **Best Case:** O(log n)
        * **Average Case:** O(log n)
        * **Worst Case:** O(log n)

### B Trees
A type of tree whose nodes can contain multiple elements
* Terminology
    1. **Order:** How many children a node can have
        * A node can have order - 1 items
    2. **2- 4 Tree:** A type of B tree with an order of 4
        * Thus, it can have up to 3 items
        * Items are stored in ascending order
* Properties
    1. The depth of all the leaf nodes is the same
    2. If there are *n* data items in a node, there must be either *0* or *n + 1* children
* Searching:
    * Steps:
        1. Start at the root node
        2. Compare the first data item with what you're searching for
            * If the data we are looking for is less than the data in the node, then go to the *nth* child, where *n* is the position of the data in the node
            * If the data we are looking for is greater than the data in the node, then go to the next child in the node
            * If the data we are looking for is equal to the data that we found, we're done
        3. Repeat step 2 until we go off the tree or find the data
    * Pseudocode
    ```python
    def search(data, node):
        if node == None:
            return True
        else:
            for i in range(n):
                if data == node.data[i]:
                    return True
                elif data < node.data[i]:
                    child = #*ith* child node
                    return search(data, child)
            return search(data, child)
    ```
* Adding:
    * Steps:
        1. When adding to a B- tree, the data is always added to a leaf node
        2. Follow the same steps as searching until we find the data in the tree or reach a leaf node
        3. Add the data at the proper place in this node
        4. If there are too many items in this node, then we call this **overflow**
            * In this case, the middle item is promoted, and the rest of the items will be split into right and left nodes
    * Pseudocode:
    ```python
    def add(data, node):
        for i in range(n):
            if data == node.data[i]:
                # Implementation defined behavior
            elif data < node.data[i]:
                if #node has any children:
                    child = #*ith*  child node
                    add(data, node.child[i])
                    if #child has too many children:
                        #break children into two nodes, promoting middle node
                return 
            else:
                #add data into this node in the *ith* position
                return
        if #node has any children:
            child = #last child node
            add(data, child)
            if #child has too many items:
                #break child up into two nodes, promoting the middle node
        else:
            #Add data into the last slot of this node
    ```
* Removing:
    * Steps:
    * Pseudocode:
    ```python
    def remove(data, node):
    ```
* Cases:
    1. Accessing
        * **Best Case:** O(1)
        * **Average Case:** O(log n)
        * **Worst Case:** O(log n)
    2. Adding
        * **Best Case:** O(log n)
        * **Average Case:** O(log n)
        * **Worst Case:** O(log n)
    3. Removing
        * **Best Case:** O(log n)
        * **Average Case:** O(log n)
        * **Worst Case:** O(log n)

### Splay Trees
A Binary Search tree that rebalances itself after each query so the most recently accessed element
* Rotations
    1. Zig
    2. Zigzig
* Cases:
    1. Accessing
        * **Best Case:** O(log n)
        * **Average Case:** O(log n)
        * **Worst Case:** O(log n)
    2. Adding:
        * **Best Case:** O(log n)
        * **Average Case:** O(log n)
        * **Worst Case:** O(log n)
    3. Removing:
        * **Best Case:** O(log n)
        * **Average Case:** O(log n)
        * **Worst Case:** O(log n)