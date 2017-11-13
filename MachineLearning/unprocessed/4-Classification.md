---
layout: notes
title: Classification
class: Intro to Machine Learning
---

# Classification
---

Classification is a way to map discrete values, i.e. true or false
* Regression techniques do not work well with classification

### Logic Regression Methods
1. For binary classification, we use the Sigmoid function (aka logistic function)
$$
h_\theta(x)= g(\theta^T x)
$$
This looks like this:

![Sigmoid function](images/sigmoid.png)

2. To get an accurate prediction, we thus need to map the output to the [0, 1] interval
	* Thus, we need to use:
	$$
	z = \theta_T x
	$$

	$$
	g(z) = \frac{1}{1 + e^{-z}}
	$$
	* $ h_{\theta}(x)=g(\theta^T x) $ will give the probability that our output is 1 on input _x_

### Decision Boundary
Typically, for classification problems, we want to predict with absolute certainty instead of a probability. We can do this with a decision boundary, i.e. a breakpoint
$$
h_\theta (x) \geq 0.5 \rightarrow y = 1
$$

$$
h_\theta (x) < 0.5 \rightarrow y = 0
$$

### Hypothesis
The hypothesis in this case is of the form:
$$
h_\theta(x) = \frac{1}{1 + e^{-\theta^tx}}
$$

### Cost Function
Logistic regression requires a different cost function as well:

$$
cost(h_\theta (x), y) =
\begin{cases}
          -\log h_\theta(x) \quad \, x = 1\\
          -\log (1 - h_\theta (x)) \quad \, x = 0
     \end{cases}
$$

We plug this cost function into the overal J(θ) function, to get the overall function:

$$
J(\theta) = - \frac{1}{m} \sum_{i = 1}^{m} cost(h_\theta (x^{(i)} ), y^{(i)})
$$

which is equal to 

$$
J(\theta) = - \frac{1}{m} \sum_{i = 1}^{m} [y^{(i)} \log h_\theta(x^{(i)} )+ (1 - y^{(i)})\log(1 - h_\theta (x^{(i)})]
$$

### Gradient Descent
The formula for gradient descent with these equations is nearly identical to the one that is used for linear regression. 
$$
\theta_j := \theta_j - \alpha \sum_{i = 1}^{m}(h_\theta(x^{(i)}) - y^{(i)})x_j^{(i)} 
$$

However, note that the hypothesis in this case is different: see [hypothesis](#Hypothesis)

### Advanced Optimizations
There are better ways to optimize the hypothesis than using gradient descent:
* Conjugate Gradient
* BFGS
* L- BFGS

These algorithms have the benefits of being faster, and having no need for a predefined learning rate. However, they are much more complex, so will not be discussed in detail here. What we do need to know is that Octave has a built in `fminunc()` function, which implements the above algorithms.


### Multiclass Classifications
What if we need to classify data into multiple classes, i.e. emails being organized into Work, School, and Personal folders?

We use the __one vs all__ algorithm:

![One Vs All algorithm](images/onevsall.png)

Basically, we group the data into _n_ different sets, assigning one group a positive value, and one a negative, then training classifiers on each set. To make a prediction on a new $ x $, we pick the classify that maximizes $ h_\theta (x) $.

### Overfitting
Sometimes we might fit the data to closely,  
