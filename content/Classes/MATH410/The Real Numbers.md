---
title: The Real Numbers
tags:
- math410
---

Here, we define what the Real Number system is, and its properties. We begin by introducing some common notations for sets of numbers.

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

If the supremum is within $S$ itself, then it is known as a **maximum**.

Similarly, a value $s \in S$ is a **greatest lower bound (infumum)** of $S$, denoted $\text{inf} (S)$, when:
1. $x$ is a lower bound of $S$.
2. If $y \in X$ is also a lower bound of $S$, then $y \le x$.

If the infimum is within $S$ itself, then it is known as a **minimum**.

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
> Suppose $X$ is a set with the least upper bound property. Then, every subset of $X$ with a lower bound has a greatest lower bound.
>
> By virtue of this theorem, all subsets $S \in \mathbb{R}$ must have infimums
>
> > [!Note]- Proof (Sketch)
> >
> > Suppose we have a subset $S$ whose existence of a supremum is guaranteed. Then, if we form a new set $T$ by multiplying the subset $S$ by -1 (reflecting it), the lower bounds of $S$ becomes the upper bounds of $T$. We thus show that there exists a supremum for $T$, and this supremum is the inverse of the infimum of $S$.


> [!Example] Example: Uniqueness of Supremum
> Prove $\text{sup}(S)$ is unique. We do this by assuming $\text{sup} (S) = a, \text{sup} (s) = b, a \ne b$, and getting a contradiction.

# Properties of the Real Numbers
Below, we describe some interesting and useful properties of the Real Numbers.

## Archimedian Property of $\mathbb{R}$
The Archimedian Property states the following:

> [!Abstract] Theorem: Archimedian Property
> 1. For all $c \in \mathbb{R}$ such that $c > 0$, there $\exists n \in \mathbb{N}$ such that $n > c$.
> 2. For all $\epsilon > 0$, there $\exists n \in \mathbb{N}$ such that $1/n < \epsilon$.
>
> Note that we can obtain one from the other by setting $\epsilon = 1/c$.
>
> > [!Note]- Proof (1)
> >
> > We will prove lemma (1) using contradiction. Suppose by way of contradiction that
> > $$
> > \lnot (\forall c > 0, \exists n \in \mathbb{N} : n > c)
> > $$
> > In other words, there exists a $c > 0$ such that $\forall n \in \mathbb{N}$, $n \le c$. By this assumption, $\mathbb{N}$ must be bounded above by definition, which by the **completeness axiom**, guarantees the existence of a supremum.
> > 
> > Let this supremum be $b = \text{sup}(\mathbb{N})$. We obtain a contradiction by finding a natural number $n \in \mathbb{N}$ that is strictly larger than $b$, violating our definition of a supremum.
> > 
> > We show this in 2 ways.
> > 
> > 1. By Lemma 1.8 (see later), we know that there must exist a unique integer $k$ such that
> >    $$
> >    b < b + 1 \le k < b + 2
> >    $$
> >    Then $k$ is an element of $\mathbb{N}$, and is **strictly larger** than $b$, givingus a contradiction.
> > 
> > 2. Since $b = \text{sup}(\mathbb{N})$, we know that there exists an $n \in \mathbb{N}$ such that
> >    $$
> >    n > b - \frac{1}{2}
> >    $$
> >    This follows by our epsilon definition of a supremum. Note that we could have chosen any value in place of $1 / 2$, as if there does not exist an $n$, then $b$ is not the least upper bound.
> > 
> >    We rearrange this to find a natural number larger than b (add 1).
> >    $$
> >    n + 1 > b + \frac{1}{2} > b
> >    $$

## Density in $\mathbb{R}$
A set $S$ is **dense in $\mathbb{R}$** if for any interval $(a,b)$, you can find some element of $S$ inside that interval. More formally, for any $a,b \in \mathbb{R}$ such that $a < b$,
$$
\exists s \in S : a < s < b
$$

See the example below.

> [!Example]+ Example: Density of $\mathbb{Z}$ in $\mathbb{R}$
> Is $\mathbb{Z}$ dense in $\mathbb{R}$?
>
> No, as we can choose an interval in $\mathbb{R}$ that does not contain any integers as a counterexample. For example, the interval $(0.5, 0.6)$ does not contain any integers.

### Density of $\mathbb{Q}$ in $\mathbb{R}$
We use the following lemmas below to show that $\mathbb{Q}$ is dense in $\mathbb{R}$. Such lemmas can be proven, but these proofs are ommitted for convenience.

> [!Abstract] Lemmas
> **(1.6)** For all $n \in \mathbb{Z}$, there is no integer in the interval $(n, n+1)$.
>
> **(1.7)** Let $S$ be a nonempty set in $\mathbb{Z}$, and bounded above. Then, $S$ has a maximum.
>
> **(1.8)** For all real numbers $c \in \mathbb{R}$, there exists a unique integer $k \in \mathbb{Z}$ such that
>    $$
>    k \in [c, c+1)
>    $$

> [!Abstract] Theorem: Density of $\mathbb{Q}$ in $\mathbb{R}$
> $\mathbb{Q}$ is **dense** in $\mathbb{R}$. This means that, for any $x,y \in \mathbb{R}$, $x < y$, then there must exist a $q \in \mathbb{Q}$ such that
> $$
> x < q < y
> $$
>
> > [!Note]- Proof (Sketch)
> >
> > Let $(a,b)$ be any interval in $\mathbb{R}$. By definition, we need to show that there exists some $q \in \mathbb{Q}$ that is in $(a,b)$.
> > 
> > First, by the Archimedian property (showed later), we choose a natural number $n \in \mathbb{N}$ such that
> > $$
> > \frac{1}{n} < b - a
> > $$
> > We use this to find the interval $[b - 1/n, b)$, which is within $(a,b)$.
> > 
> > By Lemma (3), applied to $[nb - 1, nb)$, we know that there exists an $m \in \mathbb{Z}$ that is within $[nb - 1, nb)$, so
> > $$
> > nb - 1 \le m < nb \Longrightarrow a < b - \frac{1}{n} \le \frac{m}{n} < b
> > $$

### Density of the Irrationals in $\mathbb{R}$

> [!Abstract] Theorem: Density of the Irrationals in $\mathbb{R}$
> The irrational numbers are also dense in $\mathbb{R}$.
>
> > [!Note]- Proof
> >
> > Suppose we have an interval $(a,b)$. We want to find an irrational number $z$ such that $a < z < b$.
> > 
> > To solve this, we find a different interval and use it to find our $(a,b)$ interval. Namely, we will use the interval
> > $$
> > \left( \frac{a}{\sqrt{2}}, \frac{b}{\sqrt{2}} \right)
> > $$
> > And want to use the fact that $\mathbb{Q}$ is dense in $\mathbb{R}$ to find a $q \in \mathbb{Q}$ within that interval. We can then multiply by $\sqrt{2}$ to find $z = q \sqrt{2}$
