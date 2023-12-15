---
title: Decision Problems, P vs. NP
tags:
- cmsc351
---

In this section, we discuss some time complexity ideas at a higher, more abstract level.

# Decision Problems
A **decision problem** is a problem which takes an input (called an **instance**) and outputs either a "Yes" or a "No". We typically denote a decision problem as $Q$ for the problem, and $I$ for the instance.
> Note that in a decision problem, we only ask for the solution - we don't ask how to find the solution.

> [!Example]+ Example: Decision Problem
> $Q$: Given two numbers, if their product more than 20?
> - If $I = \{ 3,8 \}$, then $Q(I) = \text{Yes}$.
> - If $I = \{ -3,1 \}$, then $Q(I) = \text{No}$.

Now, given a decision problem $Q$ and an instance $I$ such that $Q(I) = \text{Yes}$, a **proof (witness)** is evidence of this fact. Two notes about witnesses:
1. $Q(I) = \text{Yes}$ does not necessarily mean we can easily find a witness/proof showing it is true.
2. Presenting an invalid witness doesn't necessarily mean that $Q(I) = \text{No}$.

> [!Example]+ Example: Proofs and Witnesses
> $Q$: Given a set, does there exist a subset which adds to 0?
>
> If $I = \{ 3,4,-7,8,5 \}$, then $Q(I) = \text{Yes}$ with proof $\{3,4,-7\}$.

> Note that given a problem that is a non-decision problem, it's always possible to rephrase it into a decision problem which is just as hard.

# P and NP
Suppose we're running an algorithm on a **deterministic Turing Machine**, basically your average everyday computer.

Then, an algorithm taking an input of size $n$ runs in **Polynomial Time** if the worst-case time complexity is $O(n^k)$ for some $k \in \mathbb{Z}^+$. In other words, the time complexity has an upper bound which can be given as a polynomial.

The set $P$ is the set of all decision problems which have polynomial time algorithms which can make the decision:
- If $Q(I) = \text{Yes}$, then the algorithm outputs "Yes".
- If $Q(I) = \text{No}$, then the algorithm outputs "No".

> [!Example]+ Example: Polynomial Time Algorithms
> Some polynomial time algorithms are given as follows:
>
> Given a list of length $n$, is it sorted?
> > We can iterate and check if $A[i] \le A[i + 1]$ in $O(n)$ time.
>
> Given a graph, two vertices $s,t$ and positive integer $k$, does there exist a path from $s$ to $t$ with length $\le k$?
> > We can run the shortest path algorithm, and see if the shortest path's length is $\le k$.

> Note that there are problems where we don't know if there is an algorithm to solve it on polynomial time. For these problems, we cannot say if they are in $P$ or not, as we simply do not know.

Now suppose we're running an algorithm on a **non-deterministic Turing Machine**, a theoretical machine that can test many ($\infty$ many) paths, or change to several states simultaneously. By virtue of the machine being more powerful, it can solve more problems faster than a deterministic machine.

The set $NP$ is the set of all decision problems which can be solved using a non-deterministic Turing Machine in Polynomial Time. More formally, formally, we say $Q \in NP$ if there is a **verifier** $v$ taking an instance $I$ and potential witness $X$, running in polynomial time such that:
- If $V(I,x) = \text{Yes}$ then there exists a witness.
- If $V(I,x) = \text{No}$ then $x$ is not a witness.

Note that the converse of these statements does not necessarily have to be true. In other words, our verifier just needs to tell us if a potential witness is a solution or not.

> Intuitively, because non-deterministic Turing Machines can explore every possible state at once, they are bottlenecked by the verification of the solution.

> [!Example]+ Example: NP Problems
> Some non-polynomial time algorithms are given as follows:
>
> Given a set of integers $n$, is there a subset that adds to 0? Given the list $I$ and any subset $x$, we can check if the sum of elements in the subset is 0 in linear time.
> 1. $V( \{3,4,2,-7\}, \{3,4,-7\} ) = \text{Yes}$
> 2. $V( \{3,4,2,-7\}, \{3,4\} ) = \text{No}$
>
> Given a set of integers, is one of them $\ge 100$? Given a set $I$ and any particular integer $x$, the verifier could just ignore the witness $x$ entirely and solve the problem in linear time.
> 1. $V( \{1,5,107\}, 107 ) = \text{Yes}$ because there exists an element $107 \ge 100$.
> 2. $V( \{1,5,107\}, 42 ) = \text{Yes}$ because there exists an element $107 \ge 100$.
> 3. $V( \{1,2,3\}, 846) = \text{No}$ because there does not exist an element $\ge 100$.
>
> > This is a really important distinction! The verifier doesn't necessarily have to be "verifying" the witness itself.
>
> Given a partially filled $n^2 \times n^2$ sudoku board, does there exist a solution? Given a partially filled board $I$ and potential solution $x$, our verifier can check if $x$ is a solution.

Note that from this example, it's the case that $P \subseteq NP$ as we could just set the verifier to solve any problem $Q \in P$ in polynomial time. However, there are many problems in $NP$ that we don't know are in $P$!

This brings us to a major question in Computer Science:
$$
\text{Is} \; NP = P \; ?
$$


# Polynomial Reducibility
Part of the problem in the question $NP = P$ relates to a concept known as **polynomial reducibility**.

Let us have two decision problems, denoted $Q_1$ and $Q_2$. We say that $Q_1$ is  **polynomially reducible** to $Q_2$, if there exists a polynomial-time function that can transform instances of $Q_1$ into $Q_2$ - more forally, $Q_1(I) = \text{YES} \iff Q_2 (p(I)) = \text{YES}$. In the case that $Q_1$ is polynomially reducible to $Q_2$, we denote this as
$$
Q_1 \le_P Q_2
$$

Given two problems that are polynomial reducible, we can show that by using some theoretical algorithm solving one of them, we can solve the other problem in polynomial time. Consider the following example. 

> [!Example]+ Example: Polynomially Reducible Problems
> Consider the two problems:
> - `ORACLE(S,x)`: Is there a subset of $S - \{x\}$ whose sum is $-x$?
> - `SUMZERO(S)`: Does $S$ have a nonempty subset which adds to 0?
>
> We can use the `ORACLE` function to solve `SUMZERO` as follows:
> ```python
> def sumzero(S):
>     for x in S:
>         if ORACLE(S, x):
>            return True
>     return False
> ```
>
> As we can solve `SUMZERO` in a polynomial time algorithm using `ORACLE`, we've shown that the two problems are polynomially reducible to each other!

Polynomial reduction is especially important in $NP = P$, as if we can show that two problems are polynomially reducible to each other, then if one can be solved in polynomial time, so can the other! This is an extremely vital argument for showing that problems in $NP$ are also in $P$.

Though not commonly done, we can also use polynomial reducibility with sets! Given two sets $A$ and $B$, we can say that $A$ is polynomially reducible to $B$ if there exists a polynomial time function $f(x)$ such that
$$
x \in A \iff f(x) \in B
$$
So, given some value $a$, if we know that $p(a)$ is in set $B$, then it also must be in set $A$. In other words, there exists a function that can map one set to the other.

Consider some examples.

> [!Example]+ Example: Polynomial Reducibility with Sets
> Suppose we have sets $A,B$ such that
> $$
> \begin{align*}
>       A &= \{ 3x : x \in \mathbb{Z} \} \\
>       B &= \{ 5x + 1 : x \in \mathbb{Z} \}
> \end{align*}
> $$
>
> To show that these sets are polynomially reducible, we define function $f(x)$ as so:
> $$
> f(x) = 5 * \frac{x}{3} + 1
> $$
>
> We use this function to show that these sets are polynomially reducible to each other.
> - We know that if $x \in A$, then $x = 3j$ where $j \in \mathbb{Z}$. Plugging this into $f(x)$, we can see that
>   $$
>   f(x) = 5 \frac{3j}{3} + 1 = 5j + 1 \in B
>   $$
> - If $f(x) \in B$, then $f(x) = 5k + 1$ for some $k \in \mathbb{Z}$. But $f(x) = 5 \frac{x}{3} + 1$, so
>   $$
>   5k + 1 = 5 \frac{x}{3} + 1 \Longrightarrow x = 3k \in A
>   $$
