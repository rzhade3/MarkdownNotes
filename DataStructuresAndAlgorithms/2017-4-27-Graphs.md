---
layout: notes
title: Graphs
class: CS 1332
---

* A graph is a set of nodes/ vertices, and a collection of edges that connect the vertices
* Terminology
	1. **Order:** The number of vertices in the graph
	2. **Size:** The number of edges in the graph
	3. **Degree:** The number of edges incident to a vertex
		* If all degrees in a graph are the same, the graph is said to have that degree
	4. **Path:** A set of edges connecting two nodes
	5. **Directed Graph:** A graph where edges only go one way
	6. **Undirected Graph:** A graph where edges flow in both directions
	7. **Weighted Graph:** A graph where there are weights/ costs associated with each edge
	8. **Self-loop:** An edge that connects a vertex back to itself
	9. **Parallel Edges:** Edges that connect the same pair of vertices 
	10. **Adjacent Vertices:** A pair of vertices connected by an edge
	11. **Incident Edge:** The edge connecting a pair of vertices
	12. **Path:** A sequence of vertices connected by edges
		* **Simple Path:** A path with no repeated vertices
	13. **Cycle:** A path with at least one edge, with the same beginning and ending vertex
	14. **Length:** The number of edges in a path/ cycle
* Implementations for a graph are:
	1. **Adjacency Matrix:** Static implementation, two dimensional matrix containing all edges and weights
		* Size Complexity: O(n^2)
		* Contains duplicate elements
		* Easier to find edges between two vertices
	2. **Adjacency List:** Dynamic implementation, stores each of the edges leading out of a point as a list
		* Size Complexity: O(n^2)
		* Contains a list of the vertices, with a set of all edges leading out of the vertex associated with each vertex
		* Harder to find edges between two vertices
	3. **Edge List:** Like the previous one, but stores all of the edges instead
* There are two algorithms for searching for vertices in a graph: **depth first search** and **breadth first search**

### Depth First Search
An algorithm for systematically search every vertex and every edge in a graph
* This one is implemented using a stack (or can be done recursively)
* Steps:
	1. Start from one vertex
	2. Move forward along one path (don't pass through a vertex that has already been visited)
	3. When stuck, go back until you can step forward to an unvisted vertex
* Pseudocode
```python
def dFS(start, graph):
	traversal = new ArrayList()
	for edge in graph.adjacencyList.get(start):
		traversal = dFS(edge.getV(), graph, traversal)
	return traversal

def dFS(start, graph, traversal):
	for edge in graph.adjacencyList().get(start):
		if (!traversal.contains(edge.getV())):
			traversal = dFS(edge.getV(), graph, traversal)
	return traversal
```

### Breadth First Search
* An algorithm for systematically search every vertex and every edge in a graph
* This one is implemented using a queue
* Steps:
	1. Start from one vertex
	2. Move forward along one path (don't pass through a vertex that has already been visited)
	3. When stuck, go back until you can step forward to an unvisted vertex
* Pseudocode:
```python
def bFS(start, graph):
	queue = new Queue()
	traveral = new ArrayList()
	traversal.add(start)
	queue.add(start)
	while length(queue) != 0:
		start = queue.remove()
		for edge in graph.adjacencyList.get(start):
			if traversal.contains(edge.getV()):
				queue.add(edge.getV())
				traversal.add(edge.getV())
	return traversal
```

### Djikstra's Algorithm
* An algorithm for finding the shortest path joining two vertices
* Steps:
	1. Start from one vertex, choose a stop vertex
	2. Move forward along the shortest path using BFS
	3. Keep track of the distance of the path, as compared to other paths
	4. If the stop vertex is not reached, disregard the path
* Pseudocode:
```python
def djikstras(start, graph):
	
```

### Prim- Jarnik's Algorithm
* An algorithm for finding the minimum spanning tree
	* A spanning tree that connects all the vertices of the graph, and has a minimum total weight
* The basic algorithm is the same as Djikstra's, but we keep track of the edges that we traverse instead of the path weights