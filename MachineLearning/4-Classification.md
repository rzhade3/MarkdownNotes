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
<p align="center"><img src="svgs/e42743f1ad33f41673a8cc673139047d.svg?invert_in_darkmode" align=middle width=110.14624500000001pt height=18.75984pt/></p>
This looks like this:

![Sigmoid function](images/sigmoid.png)

2. To get an accurate prediction, we thus need to map the output to the [0, 1] interval
	* Thus, we need to use:
	<p align="center"><img src="svgs/ef9cd1bef1bab70b34b3cb29a8f702f6.svg?invert_in_darkmode" align=middle width=57.75264pt height=13.881251999999998pt/></p>

	<p align="center"><img src="svgs/635e4e714461ea4b56e1955f7d0ed6ed.svg?invert_in_darkmode" align=middle width=107.28646499999998pt height=34.360095pt/></p>
	* <img src="svgs/6c010255c12f9647f043e4865ad3fa4e.svg?invert_in_darkmode" align=middle width=110.14624500000001pt height=27.656969999999987pt/> will give the probability that our output is 1 on input _x_

### Decision Boundary
Typically, for classification problems, we want to predict with absolute certainty instead of a probability. We can do this with a decision boundary, i.e. a breakpoint
<p align="center"><img src="svgs/c77d022dfa33a80f0a42ab749d8c9bce.svg?invert_in_darkmode" align=middle width=146.367705pt height=16.438356pt/></p>

<p align="center"><img src="svgs/b83c9664a11ee4efd7d388a1ea921694.svg?invert_in_darkmode" align=middle width=146.367705pt height=16.438356pt/></p>

### Hypothesis
The hypothesis in this case is of the form:
<p align="center"><img src="svgs/487cf5f2a37a3b876cfad612c67595d0.svg?invert_in_darkmode" align=middle width=129.563775pt height=34.367685pt/></p>

### Cost Function
Logistic regression requires a different cost function as well:

<p align="center"><img src="svgs/3328aa09998778cb3db6464409942ef0.svg?invert_in_darkmode" align=middle width=307.3653pt height=49.31553pt/></p>

We plug this cost function into the overal J(θ) function, to get the overall function:

<p align="center"><img src="svgs/bb99d7730a441d6b2c548b3936d580e5.svg?invert_in_darkmode" align=middle width=242.00714999999997pt height=44.897324999999995pt/></p>

which is equal to 

<p align="center"><img src="svgs/402c43a886a8a160a745a13a7c477d2f.svg?invert_in_darkmode" align=middle width=425.39144999999996pt height=44.897324999999995pt/></p>

### Gradient Descent
The formula for gradient descent with these equations is nearly identical to the one that is used for linear regression. 
<p align="center"><img src="svgs/217e66e643cf9619c43757c3037045cf.svg?invert_in_darkmode" align=middle width=249.34965pt height=44.897324999999995pt/></p>

However, note that the hypothesis in this case is different: see [hypothesis](#Hypothesis)
