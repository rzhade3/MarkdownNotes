---
layout: notes
title: Normal Equation
class: Intro to Machine Learning
---

# Normal Equation
---

Linear regression is great and all, but it is still iterative. What if there was a way to minimize J in one step?
* The normal equation works by taking the derivative of J with respect to θ_j, and setting it to zero (normalizing the curve). This is given by the formula:

<p align="center"><img src="svgs/eb2026dab93a888baa5aaab2ff4cca11.svg?invert_in_darkmode" align=middle width=134.611455pt height=18.75984pt/></p>

With this equation, there is no need to do feature scaling, or bother with learning rates

However, as this formula uses an inverse matrix, it has its own pitfalls

### Pros and Cons
| Gradient Descent   |    Normal Equation   |
|--------------------|----------------------|
| Needs to choose α  | No need for an alpha |
| Iterative			 | One step function	|
| O(kn^2) 			 | O(n^3) 			    |
| Better for large n | Better for small n   |

In practice, we want to us __gradient descent__ for around n > 10000