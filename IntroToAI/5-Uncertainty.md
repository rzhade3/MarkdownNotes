---
layout: notes
title: Uncertainty
class: CS 3600
---

# Uncertainty
Previously, we assumed that everything about the environment and the agent was deterministic. However, this is rarely true in the real world. How do we deal with faulty sensors, agents with incomplete information, and agents that do not behave the same way every time?

### Terminology
* **Belief State:** A representation of the set of all possible world states that are possible given a set of observations
* **Outcome:** A completely specified state, i.e. all information is available about this state
* **Decision Theory = Probability Theory + Utility Theory**
* **Probability Model:** A model associating a probability with every possible world
* **Unconditional/ Prior Probabilites:** Degrees of belief in propositions in the absence of other information

### Basic Probability Notation
* Most probabilities are expressed in conditional terms, i.e. as a combination of prior probabilities and *evidence*
	* For any two propositions *a* and *b*, we have:
		* ![P(a | b) = \frac{P(a \wedge b)}{P(b)}](https://raw.githubusercontent.com/rzhade3/MarkdownNotes/master/IntroToAI/images/conditional_probability.png)