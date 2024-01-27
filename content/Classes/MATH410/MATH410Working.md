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
Let $P$ be the subset of $\mathbb{R}$ containing positive numbers. Then, as $\mathbb{R}$ satisfies the **positivity axioms**, the following hold:

$$
\begin{align}
        \forall a,b \in P \qquad &ab \in P, a + b \in P &\text{Closure} \\
        \forall a \in \mathbb{R} \qquad &a \in P \lor -a \in P \lor a = 0 &\text{Trichotomy}
\end{align}
$$

These axioms can be used to define the inequality operations, which we often use in the real numbers.


## Completeness Axioms
### Bounds
We say that a subset of the real numbers, $S \in \mathbb{R}$, is **bounded above** if
$$
\exists \beta \in \mathbb{R} : \forall x \in S, x \le \beta
$$
Where $\beta$ is known as an **upper bound**. In other words, there exists some $\beta$ that is greater than or equal to all elements in the set $S$.

Similarly, we say that $S$ is **bounded below** if
$$
\exists \beta \in \mathbb{R} : \forall x \in S, x \ge \beta
$$
Where $\beta$ is known as a **lower bound**. In other words, there exists some $\beta$ that is less than or equal to all elements in the set $S$.

### Supremum and Infimum
Suppose we have a subset of the real numbers, $S \in \mathbb{R}$.

Then, a value $x \in S$ is a **least upper bound (supremum)** of $S$, denoted $\text{sup} (S)$, when:
1. $x$ is an upper bound of $S$.
2. If $y \in X$ is also an upper bound of $S$, then $x \le y$.

Similarly, a value $s \in S$ is a **greatest lower bound (infumum)** of $S$, denoted $\text{inf} (S)$, when:
1. $x$ is a lower bound of $S$.
2. If $y \in X$ is also a lower bound of $S$, then $y \le x$.

We can think of supremum and infimum as the "closest" value in $X$ that serves as an upper (or lower) bound for $S$! However, they are not necessarily maximums or minimums, as supremums and infimums do not have to be in $S$!

> [!Abstract] Theorem: Alternative Definition of Supremum and Infimum
> Let $S \subseteq \mathbb{R}$, and bounded above (by $M$). Then,
> $$
> M = \text{sup}(S) \iff \forall \epsilon > 0, \exists x_\epsilon \in S : x_\epsilon > M - \epsilon
> $$
> In other words, $M$ is a supremum if and only if for all positive epsilon, there exists some point in the set that is greater than the supremum minus epsilon.
>
> Similarly, let $S$ be bounded below (by $m$). Then,
> $$
> m = \text{inf}(S) \iff \forall \epsilon > 0, \exists x_\epsilon \in S : x_\epsilon < m + \epsilon
> $$
>
> > These statements are basically saying that there is no such smaller upper bound, or no such smaller lower bound.\, as we can find an $x \in S$ which fails to satisfy the bound definition.


> [!Example]- Example: Supremums
> 1. Suppose $S = (0,1)$. Then, $\text{sup} (S) = 1$.
> 2. Suppose $S = \{ -1/x : x > 0 \}$. Then, $\text{sup} (S) = 0$.
> 3. Suppose $S = \mathbb{N}$. Then, $\text{sup} (S)$ does not exist, as the naturals aren't bounded above.

> [!Example]+ Example: Infimum Proof
> Suppose $S = (0,1)$. Prove that $\text{inf} (S) = 0$. We need to show that:
> 1. 0 is a lower bound of $S$.
>
> As $0 \le 0 < x < 1$ for all $x \in S$, 0 is a lower bound for $S$.
> 
> 2. For any other arbitrary lower bound $y$, $y \le 0$.
>
> Let $y$ be any lower bound of $S$, and suppose by way of contradiction that $y > 0$. We do a case analysis to show that no value $y > 0$ can possibly be a lower bound.
> - If $0 < y < 1$, we can pick an element in $S$ that is smaller than $y$, by choosing $y / 2$. This yields a contradiction!
> - If $y \ge 1$, we can simply pick any element in $S$, as it will be smaller than $y$. Choosing 0.5, we get a contraditiction!
>
> Thus, if $y$ is a lower bound of $S$, it must be $\le 0$.

### Completeness Axiom
Suppose we have any subset of the real numbers $S \in \mathbb{R}$ that is bounded above. Then, $S$ is guaranteed to have a supremum, which is a property known as the **least upper bound property (completeness axiom)** of $\mathbb{R}$.

We can use this property to prove the existence of infimums as well.

> [!Abstract] Theorem: Existence of Infimum
> Suppose $X$ is a set with the least upper bound property. THen, every subset of $X$ with a lower bound has a greatest lower bound.
>
> By virtue of this theorem, all subsets $S \in \mathbb{R}$ must have infimums
>
> > [!Note]- Proof (Sketch)
> >
> > Suppose we have a subset $S$ whose existence of a supremum is guaranteed. Then, if we form a new set $T$ by multiplying the subset $S$ by -1 (reflecting it), the lower bounds of $S$ becomes the upper bounds of $T$. We thus show that there exists a supremum for $T$, and this supremum is the inverse of the infimum of $S$.


> [!Example]
> Prove $\text{sup}(S)$ is unique. We do this by assuming $\text{sup} (S) = a, \text{sup} (s) = b, a \ne b$, and getting a contradiction.


