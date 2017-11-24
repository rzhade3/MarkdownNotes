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
<p align="center"><img src="./svgs/sigmoid_function.svg" align=middle width=110.14624500000001pt height=18.75984pt/></p>
This looks like this:

![Sigmoid function](images/sigmoid.png)

2. To get an accurate prediction, we thus need to map the output to the [0, 1] interval
	* Thus, we need to use:
	<p align="center"><img src="./svgs/logistic_remapping_partial.svg" align=middle width=57.75264pt height=13.881251999999998pt/></p>

	<p align="center"><img src="./svgs/logistic_remapping_full.svg" align=middle width=107.28646499999998pt height=34.360095pt/></p>
	* <img src="./svgs/logistic_probability.svg" align=middle width=110.14624500000001pt height=27.656969999999987pt/> will give the probability that our output is 1 on input _x_

### Decision Boundary
Typically, for classification problems, we want to predict with absolute certainty instead of a probability. We can do this with a decision boundary, i.e. a breakpoint
<p align="center"><img src="./svgs/breakpoint_1.svg" align=middle width=146.367705pt height=16.438356pt/></p>

<p align="center"><img src="./svgs/breakpoint_2.svg" align=middle width=146.367705pt height=16.438356pt/></p>

### Hypothesis
The hypothesis in this case is of the form:
<p align="center"><img src="./svgs/logistic_hypothesis.svg" align=middle width=129.563775pt height=34.367685pt/></p>

### Cost Function
Logistic regression requires a different cost function as well:

<p align="center"><img src="./svgs/logistic_cost.svg" align=middle width=307.3653pt height=49.31553pt/></p>

We plug this cost function into the overal J(θ) function, to get the overall function:

<p align="center"><img src="./svgs/bb99d7730a441d6b2c548b3936d580e5.svg" align=middle width=242.00714999999997pt height=44.897324999999995pt/></p>

which is equal to 

<p align="center"><img src="./svgs/402c43a886a8a160a745a13a7c477d2f.svg" align=middle width=425.39144999999996pt height=44.897324999999995pt/></p>

### Gradient Descent
The formula for gradient descent with these equations is nearly identical to the one that is used for linear regression. 
<p align="center"><img src="./svgs/logistic_gradient_descent.svg" align=middle width=249.34965pt height=44.897324999999995pt/></p>

However, note that the hypothesis in this case is different: see [hypothesis](#Hypothesis)
