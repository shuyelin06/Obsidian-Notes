---
title: STAT401
tags:
- stat401
---

# Basic Concepts
We say that an **experiment** is a repeatable task with well defined outcomes. The **sample space ($S$)** for this experiment is the set of all possible outcomes of the experiment.

Any subset $E$ of the sample space for an experiment is called an **event**. To say that **an event $E$ has happened** means that we performed the experiment, and had the outcome which was in the set $E$.
> Events with exactly one outcome are called **simple events**.

Given a sample space, we can define a **random variable**, which is a function $X : S \to \mathbb{R}$ which assigns a number to a given sample space outcome. This number will relate to what we're interested in measuring for the experiment.

> [!Example]+ Example: Random Variables
> Say we flip a coin 4 times.
>
> The size of the sample space would be $2^4$, the total number of possible outcomes after flipping the coin. One outcome, for example, is $HHTH$. 
>
> A random variable would take this outcome, $HHTH$, and assign some number to it relevant to our interests (ex. the number of heads 3, the number of tails 1, etc.)

Any collection of random variables $\{X_1, X_2, \dots X_n\}$ is called a **random sample** if the following conditions are met:
- All of the $X_i$'s are identically distributed.
- All of the $X_i$'s are mutually independent.

Given a random sample, a **statistic** $S$ is a function of this random sample taking values in $\mathbb{R}$. We can take random samples from a population to make inferences about our data!

Say we have a population, and we took a sample from it. With this, we can do 2 things:
1. **Deduction**: Given something known about the population, analyze the sample.
2. **Generalization**: Given the sample, try to make an inference about the population.
