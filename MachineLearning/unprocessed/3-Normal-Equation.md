---
layout: notes
title: Normal Equation
class: Intro to Machine Learning
---

# Normal Equation
---

Linear regression is great and all, but it is still iterative. What if there was a way to minimize J in one step?
* The normal equation works by taking the derivative of J with respect to θ_j, and setting it to zero (normalizing the curve). This is given by the formula:

$$
\theta = (X^{T}X)^{-1}X^{T}y
$$

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