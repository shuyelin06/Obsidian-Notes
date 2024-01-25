---
title: Math410Working
tags:
- math410
- wip
---

*We define what the Real Numbers are*

---

We first begin by introducing some common notations for sets of numbers.

$$
\begin{align*}
        &\mathbb{N} = \{ 1, 2, 3, \dots \} \\
        &\mathbb{Z} = \{ \dots, -2, -1, 0, 1, 2, \dots \} \\
        &\mathbb{Q} = \{ p / q : p,q \in \mathbb{Z}, q \ne 0 \}
\end{align*}
$$

# The Real Number System
We define the Real Numbers, $\mathbb{R}$, as the number system satisfying the following 3 groups of axioms: **field axioms**, **positivity axioms**, and **completeness axioms**.

## Field Axioms
Part of the definition of the Real Numbers $\mathbb{R}$ is that it is a **field**.

A **field** is a set of numbers with two binary operations, called **addition ($+$)** and **multiplication ($\times$)**, that satisfy rules known as **field axioms**. These axioms are split into addition, multiplication, and distributive axioms, and are described below.
> Addition and multiplication don't necessarily have to stand for the addition and multiplication we're used to, though in the purposes of real numbers they do.

### Addition Axioms
The addition axioms include properties of **commutativity**, **associativity**, **identity**, and **invertibility**.

$$
\begin{align}
        \forall x,y \in \mathbb{F} \qquad &x + y = y + x &\text{Commutativity} \\
        \forall x,y,z \in \mathbb{F} \qquad &(x + y) + z = x + (y + z) &\text{Associativity} \\
        \exists 0 \in \mathbb{F} : \forall x \in \mathbb{F} \qquad &x + 0 = x &\text{Identity} \\
        \forall x \in \mathbb{F}, \exists (-x) \in \mathbb{F} \qquad &x + (-x) = 0 &\text{Invertibility}
\end{align}
$$

### Multiplication Axioms
Just like the addition axioms, the multiplication axioms include properties of **commutativity**, **associativity**, **identity**, and **invertibility**.

$$
\begin{align}
        \forall x,y \in \mathbb{F} \qquad &x \cdot y = y \cdot x &\text{Commutativity} \\
        \forall x,y,z \in \mathbb{F} \qquad &(x \cdot y) \cdot z = x \cdot (y \cdot z) &\text{Associativity} \\
        \exists 1 \in \mathbb{F} : 1 \ne 0 \land \forall x \in \mathbb{F} \qquad &x \cdot 1 = x &\text{Identity} \\
        \forall x \in \mathbb{F}, x \ne 0, \exists x^{-1} \in \mathbb{F} \qquad &x \cdot x^{-1} = 1 &\text{Invertibility}
\end{align}
$$

### Distributivity and Nontriviality
Additionally, a field relates the addition and multiplication operation through a property known as **distributivity**, defined below.

$$
\begin{align}
        \forall x,y,z \in \mathbb{F} \qquad &x \cdot (y + z) = x \cdot y + x \cdot z &\text{Distributivity}
\end{align}
$$

Finally, a field has the property of **nontriviality**, which states that $0 \ne 1$.

$$
\begin{align}
        &0 \ne 1 &\text{Nontriviality}
\end{align}
$$

From these base axioms, we can derive all of the rules for standard algebraic manipulations which we can perform in the Real Numbers.


## Positivity Axioms
Another part of the definition of the Real Numbers $\mathbb{R}$ is that it satisfies the **positivity axioms**, given below.

Let $P$ be the subset of $\mathbb{R}$ containing positive numbers. The positivity axioms state the following:

$$
\begin{align}
        \forall a,b \in P &ab \in P, a + b \in P &\text{Closure} \\
        \forall a \in \mathbb{R} &a \in P \lor -a \in P \lor a = 0 &\text{Trichotomy}
\end{align}
$$

These axioms can be used to define the inequality operations, which we often use in the real numbers.