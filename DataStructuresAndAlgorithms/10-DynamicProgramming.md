---
layout: notes
title: Dynamic Programming
class: CS 1332
---

Dynamic programming is a technique for solving a complex problem by breaking it down into simpler recurrent subproblems, solving the subproblems once, and storing the solutions
Bottom up approach
* Identify smaller subproblems
* Find order of solving subproblems
* Make sure subproblems are 
* Subproblems overlap, or are not interdependent
Matrix multiplication is most common 

### Matrix Multiplication

### Subsequences
A subsequence is a character string *x(1), x(2), x(3)... x(n-1)* of the form *x(j1), x(j2), x(j3)... x(jk)*, where i(j) < i(j + 1)
	* This is not the same thing as a substring, as the characters do not need to be consecutive
Most common problem here is the LCS (Longest common subsequence)
* Definition:
	* Given two strings X and Y, find the longest common subsequence
		* i.e. LCS for *ABCDEFG* and *XZACKDFWGH* is *ACDFG*
* DP Approach
	* Steps:
		1. Define L[i, j] to be the length of the LCS of X[0... i] and Y[0... j]
			* Allow for -1 as an index, so L[-1, k] = 0 and L[k, -1] = 0 indicated that the null part of X and Y has no match with one another
		2. Then, iterate through the strings character by character according to the table
			* If the two characters at those indices match, put 1 + L[j - 1, k - 1] in the cell, e.g.
				```
				L[j, k] = 1 + L[j - 1, k - 1]
				```
			* Otherwise, put the maximum of the number above and below, e.g.
				```
				L[j, k] = max(L[j - 1, k], L[j, k - 1])
				```
		3. The length of the LCS is the number at the bottom right corner