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
<p align="center"><img src="svgs/0117dce132b033ba8daef8a4d8597e42.svg?invert_in_darkmode" align=middle width=138.93049499999998pt height=16.438356pt/></p>

<p align="center"><img src="svgs/9e5b5f04b873564283e37077ad10a33f.svg?invert_in_darkmode" align=middle width=138.93049499999998pt height=16.438356pt/></p>