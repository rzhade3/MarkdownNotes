---
layout: notes
title: Simple Search
class: CS 3600
---

# Simple Search Algorithms
Let us say that we need to get from one side of town to another, in the least amount of time. How would we go about doing that? There might be an infinite number of paths that we could take, but only one that would take the shortest. This chapter discusses ways to find the fastest path, or to just find a path, as quickly as possible.

### Terminology
1. *State:* A unique configuration of the world, encoding all information relevant to the agent
2. *Goal:* The state, or states, that the agent wants to be in
3. *Action:* Something to transfer an agent from one state to another
4. *Problem:* Not being in a goal state
5. *Initial State:* The world prior to solving the problem
6. *State Space:* The set of all possible states
7. *Successor Function:* A function that takes in a state, and generates all subsequent states


### Evaluation Metrics
* *Completeness:* Does it always find a solution?
* *Time Complexity:* Self explanatory
* *Space Complexity:* The number of states stored in memory at any given time
* *Optimality:*Does it always find the lowest cost solution?

### Types of Algorithms
* **Breadth First Search:** Search all successors sequentially
	* Use a queue
	* Optimal, but space complex as it needs to search all possible states
* **Depth First Search:** Search a path, and then backtrack to last branch if not at goal state
	* Use a stack
	* Not an optimal sorting algorithm, but less space complex
* **Bidirectional Search:** Running the search algorithm from both sides, and stopping when the two frontiers intersect
* **Uniform Cost Search:** Minimize costs, so visit paths with lowest total cost first
	* Use a priority queue, with metric being the path cost
* **Best First Search:** Go to path with least heuristic value
* **A Star:** Same as the UCS, except with a *heuristic*
	* Use a priority queue, using sum of path cost and heuristic as the metric
	* If the heuristic is admissible, it is optimal and less space complex

### Characteristics of Each Algorithm
|  | Completeness | Time | Space | Optimality |
| --- | --- | --- | --- | --- |
| BFS | Y | O(b^d) | O(b^d) | Y |
| DFS | N | O(b^m) | O(bm) | N |
| UCS | Y | O() | O() | Y |  
| Bidirectional | Y | O() | O() | Y |

### Heuristic
* A heuristic is an estimate of the distance from the closest goal state.
* A good heuristic has two conditions: *admissibility* and *consistency*
	* **Admissibility:** The weight of the heuristic must never be greater than the actual distance from a state to the goal
		* This condition must be met by all heuristics to work
	* **Consistency:** The heuristic must always be increasing or decreasing as it moves towards the goal
		* I.e. given a state n, and any of its successors n', h(n) ≤ c(n, a, n') + h(n')
		* This condition is only required for graph searching
		* Consistent heuristics are always admissible
