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
<p align="center"><img src="https://rawgit.com/rzhade3/MarkdownNotes (fetch/master/svgs/67508d56056814349375c2060b68c1ca.svg?invert_in_darkmode" align=middle width=119.99229pt height=20.495145pt/></p>
This looks like this:

![Sigmoid function](images/sigmoid.png)

2. To get an accurate prediction, we thus need to map the output to the [0, 1] interval
	* Thus, we need to use:
	<p align="center"><img src="https://rawgit.com/rzhade3/MarkdownNotes (fetch/master/svgs/ed91dc980198af5236a0491f67493c31.svg?invert_in_darkmode" align=middle width=184.75875pt height=37.394445pt/></p>
<img src="https://rawgit.com/rzhade3/MarkdownNotes (fetch/master/svgs/ae9e998266dda87d0df355a755a672be.svg?invert_in_darkmode" align=middle width=130.635615pt height=29.19113999999999pt/> will give the probability that our output is 1 on input _x_

### Decision Boundary
Typically, for classification problems, we want to predict with absolute certainty instead of a probability. We can do this with a decision boundary, i.e. a breakpoint
<p align="center"><img src="https://rawgit.com/rzhade3/MarkdownNotes (fetch/master/svgs/1ebd37fa5bc5f7a51c0184e0d4208dfd.svg?invert_in_darkmode" align=middle width=226.7199pt height=16.438356pt/></p>