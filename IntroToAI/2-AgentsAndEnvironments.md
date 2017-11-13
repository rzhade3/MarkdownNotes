---
layout: notes
title: Agents And Environments
class: CS 3600
---

# Agents and Environments

### Agents
An agent is anything that perceives the environment through **sensors** and acts on the environment with **effectuators**.
* Terminology:
    1. *Percepts:* An agent's perceptual inputs at any given point in time
    2. *Percept Sequence:* The complete history of everything the agent has ever perceived.
    3. *Agent Function:* A function that maps any given percept sequence to an action
    4. *Agent Program:* An implementation of the agent function
    5. *Rational Agent:* An agent which selects the action that is expected to maximize its performance measure, given the evidence provided by the percept sequence
    6. *Autonomy:* Whether an agent is able to rely on its own percepts or on the prior knowledge of the designer
* An agent is **rational** if it always chooses the best action based on its knowledge
* Knowledge of an Agent:
    * Percept history
    * Built in knowledge


### Environments
* A *task environment* is the problem to which the agent is the solution.
    * E.g. for a chess playing robot, the task environment is the chess board

* **Observability**

| Fully Observable | Partially Observable |
| --- | --- |
| Can sense everything in the environment | Can only observe some of the environment |
| Perfect sensors everywhere | Causes: Noise and incomplete data
| E.g. Chess board | E.g. pretty much everything else |

* **Determinism**

| Deterministic | Stochastic |
| --- | --- |
| World changes only upon action by agent | World can change anytime |
| World changes exactly as desired | Randomness |
| E.g. Chess board | E.g. Anything else |

* **Static**

| Static | Dynamic |
| --- | --- |
| World doesn't change until agent makes decision | World keeps changing even while agent is deliberating |
| E.g. Poker | E.g. Actual world |

* **Discreteness**

| Discrete | Continuous |
| --- | --- |
| World broken up into discrete chunks | Infinite number/ gradiations of chunks |
| E.g. Poker | E.g. driving a car |

* **Episodic**

| Episodic | Sequential |
| --- | --- |
| History does not matter | History affects present and future |
| E.g. Identifying defects on a product line | E.g. Game of chess |

* **Agents**

| Single Agent | Multi Agent |
| --- | --- |
| You are the only agent in the world | There are other agents in the world, either cooperative or competitive. |

