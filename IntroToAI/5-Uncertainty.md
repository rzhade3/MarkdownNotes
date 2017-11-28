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
		* <img src="https://raw.githubusercontent.com/rzhade3/MarkdownNotes/master/IntroToAI/images/conditional_probability.png" alt="P(a | b) = \frac{P(a \wedge b)}{P(b)}" height=27.656969999999987pt>
		* The above holds as long as P(b) is not 0, or <img src="https://raw.githubusercontent.com/rzhade3/MarkdownNotes/master/IntroToAI/images/conditional_probability_limit.png" alt="P(b) \neq 0" height=16.438356pt> 
		* Another way to write this is called the *product rule*, and is shown as <img src="https://raw.githubusercontent.com/rzhade3/MarkdownNotes/master/IntroToAI/images/product_rule.png" alt="P(a \wedge b) = P(a | b)P(b)">
	* *Inclusion- exclusion principle:* <img src="https://raw.githubusercontent.com/rzhade3/MarkdownNotes/master/IntroToAI/images/inclusion_exclusion.png" alt="P(a \vee b) = P(a) + P(b) - P(a \wedge b)" height=27.656969999999987pt>
* In most cases, there are not a discrete number of probabilities
	* In these cases we use a *probability distribution function*, which is a function mapping each state to a probability
	* A *joint probability distribution* is a distribution function with multiple parameters, one for each condition of the state. The function is some variant of the product rule

### Inference
Its no use just being able to describe the probability of each state, if we can't predict what happens next
* **Probabilistic inference** is the computation of posterior probabilities given observed evidence
	* *Marginilization:* Removing other variables from an equation by summing up their values across the joint PDF
	* *Conditioning:* A form of marginilization with conditional probability rather than joint probabilities
		* <img src="https://raw.githubusercontent.com/rzhade3/MarkdownNotes/master/IntroToAI/images/marginilization.png" alt="P(Y) = \sum_z P(Y | z) P(z)" height=16.438356pt>
