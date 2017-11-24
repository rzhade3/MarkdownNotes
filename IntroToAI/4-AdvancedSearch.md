---
layout: notes
title: Advanced Search Algorithms
class: CS 3600
---

# Advanced Search Algorithms
What if there are a very large number of states, or instead of finding one goal state, we need to find the "best" state? Such problems are called *optimization* problems, and require specialized algorithms to deal with them. These algorithms are called **local search algorithms**.

### Terminology
* **Local Search Algorithm:** A search algorithm which can only make local changes, i.e. only moving in the local area right or left
* **State- Space Landscape:** A graph, with the y- axis (elevation) being the objective function and the x- axis (location) being the state
* **Local Minimum:** A trough in the state- space landscape
* **Local Maxima:** A peak in the state- space landscape
* **Global Minimum:** The lowest trough in the state- space landscape
* **Global Maximum:** The highest peak in the state- space landscape

### Types
* **Hill Climbing:** Most generic local search algorithm;
	* **Blind Hill Climbing:** Start in some random state, pick best successor as next state
		* Gets stuck in local extrema
	* **Random-restart Hill Climbing:** Conduct a series of hill climbing searches from randomly generated starting points until the goal is found
	* **Simulated Annealing:** Instead of picking best successor as next state, randomly go to another point. Chance of going to this random point decreases each iteration
		* Reduces the likelihood of getting stuck
		* The likelihood of randomly going to another point is called *"temperature"*
		* If temperature cools down *too fast*, solution converges faster but less likely to find global max
		* If temperature cools down *too slow*, solution converges slower, but more likely to find global max
	* **Genetic algorithm:** Parallel hill search with information sharing
		1. Start with n random starting positions (*individuals*)
		2. Pick the k individuals with the best fitness
		3. Combine these individuals to create a new set of n individuals:
			* *Mutation:* Randomly change some of these values
			* *Cross over:* Mix and match two or more indviduals
		4. Find the k individuals with the best fitness and continue the above process
	* **Just in time algorithm:** Some variant of the above algorithms, that can be halted at any time to find a solution
