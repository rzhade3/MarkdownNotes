---
layout: notes
title: Linear Regression
class: Intro to Machine Learning
---

# Linear Regression
---

Linear Regression is one of the most common applications of machine learning
* Given a data set, coming up with a function that best maps _x_ to __y__


### Terminology
_m_: The number of training examples
_x_: The features (or the number of features)
__y__: The target variable (aka the output)
_Hypothesis_: A function that describes the data

### Hypothesis
A hypothesis is a function that seeks to describe a set of data
* It is the function that generates a best fit line
* Equation
<p align="center"><img src="svgs/afce74144874023f611d8ae2009e0a9a.svg?invert_in_darkmode" align=middle width=289.1526pt height=16.438356pt/></p>

This can also be written as:

<p align="center"><img src="svgs/a7575407708261ab7cba20e9fe9e94a1.svg?invert_in_darkmode" align=middle width=247.9323pt height=98.63106pt/></p>

### Cost Function
Let us define a cost function to be the difference between the expected value, and the value generated by the hypothesis
* Thus, the best fit line is the line with the least cost function, i.e. J(x) is closest to 0

Usually, we use the cost function:
<p align="center"><img src="svgs/38e7c2fcfb9a7ed179624523a424dcb8.svg?invert_in_darkmode" align=middle width=233.49314999999999pt height=44.897324999999995pt/></p>

### Gradient Descent
To algorithmically generate a better hypothesis (this is machine _learning_ after all), we use gradient descent
* __Definition__: Following the negative of the gradient (derivative at a point) to get to the local minima
* Algorithm:
<p align="center"><img src="svgs/4ba13b8d8b1d0776c38f75926140fbdb.svg?invert_in_darkmode" align=middle width=233.79345pt height=44.897324999999995pt/></p>

where α is the learning rate

### Learning Rate
As mentioned in the previous section, α is the learning rate, i.e. the amount that the function "moves" after each iteration of gradient descent. Picking a correct value for α is very important
* If α is too small, it will take too long for J(θ) to converge
* If α is too large, J(θ) might not decrease on every iteration, and thus diverge from the extrema

From these two observations, we can determine two rules to follow to choose a good learning rate
1. If J(θ) ever increases between any two iterations, decrease α
2. If J(θ) decreases by less than some value E between two iterations (where E is some small number), declare convergence or increase α

### Feature Scaling
Since we are doing this iteratively, there might be no limit on how long it takes for gradient descent to work. To make it go faster, it is best to _normalize_ the ranges of the features, i.e.

<p align="center"><img src="svgs/d3d555e1f86e69f0ac9f485265133898.svg?invert_in_darkmode" align=middle width=87.92685pt height=13.059337499999998pt/></p>

or

<p align="center"><img src="svgs/24477ea0b9555b6ba5aecb9db0329ac9.svg?invert_in_darkmode" align=middle width=113.497725pt height=13.059337499999998pt/></p>

There are two main methods for doing so:
1. __Feature Scaling__: Dividing the feature by the range (normalizes the features to a range of 1)
2. __Mean Normalization__: Subtracting the mean of the feature set from the feature (normalizes the features to a mean of 0)

Thus, after feature scaling, the input set would have values generated with the following function

<p align="center"><img src="svgs/511b0b4d155263ac1ea1b38103cf725d.svg?invert_in_darkmode" align=middle width=93.66093pt height=34.451339999999995pt/></p>

where µ is the mean, and _s_ is the range

### Polynomial Regression
If a line does not fit the data set well, we can use other shapes as well, making features quadratic, squares, cubics, or any form we choose.

In this case, it is important to do feature scaling, as if x_1 has range 1 - 1000, x_1^2 has range 1 - 1000000, and so on