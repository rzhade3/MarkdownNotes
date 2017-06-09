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
$ h_[\theta](x)=g(\theta^[T] x) $ will give the probability that our output is 1 on input _x_

### Decision Boundary
Typically, for classification problems, we want to predict with absolute certainty instead of a probability. We can do this with a decision boundary, i.e. a breakpoint
$$
hθ(x) \geq 0.5 \rightarrow y = 1
$$
$$
hθ(x) < 0.5 \rightarrow y = 0
$$