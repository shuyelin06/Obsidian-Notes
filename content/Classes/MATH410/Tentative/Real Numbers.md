---
title: The Real Number System
tags:
- math410
- wip
---

# Fields
## Field Axioms
A **field**, commonly denoted $\mathbb{F}$, is a set of numbers which has two binary operations, called **addition** and **multiplication**, satisfying rules known as **field axioms**. These axioms are split into addition, multiplication, and distributive axioms, and are described below.
> Addition and multiplication don't necessarily have to stand for the addition and multiplication we're used to!

> [!Example]+ Example: Well-Known Fields
> The sets $\mathbb{Q}$ (rational numbers), $\mathbb{R}$ (real numbers), and $\mathbb{C}$ (complex numbers) are all fields.

Both of the addition and multiplication axioms include properties of **commutativity**, **associativity**, **identity**, and **invertibility**.

**Addition Axioms**
$$
\begin{align}
        \forall x,y \in \mathbb{F} \qquad &x + y = y + x &\text{Commutativity} \\
        \forall x,y,z \in \mathbb{F} \qquad &(x + y) + z = x + (y + z) &\text{Associativity} \\
        \exists 0 \in \mathbb{F} : \forall x \in \mathbb{F} \qquad &x + 0 = x &\text{Identity} \\
        \forall x \in \mathbb{F}, \exists (-x) \in \mathbb{F} \qquad &x + (-x) = 0 &\text{Invertibility}
\end{align}
$$

**Multiplication Axioms**
$$
\begin{align}
        \forall x,y \in \mathbb{F} \qquad &x \cdot y = y \cdot x &\text{Commutativity} \\
        \forall x,y,z \in \mathbb{F} \qquad &(x \cdot y) \cdot z = x \cdot (y \cdot z) &\text{Associativity} \\
        \exists 1 \in \mathbb{F} : 1 \ne 0 \land \forall x \in \mathbb{F} \qquad &x \cdot 1 = x &\text{Identity} \\
        \forall x \in \mathbb{F}, x \ne 0, \exists x^{-1} \in \mathbb{F} \qquad &x \cdot x^{-1} = 1 &\text{Invertibility}
\end{align}
$$

Furthermore, a field must relate the properties of addition and multiplication through the property of **distributivity**, given below.

$$
\begin{align}
        \forall x,y,z \in \mathbb{F} \qquad &x \cdot (y + z) = x \cdot y + x \cdot z &\text{Distributivity}
\end{align}
$$

From these base axioms, we can derive all of the rules for standard algebraic manipulations. Below, we discuss some of them.


## Consequences of the Field Axioms
### Consequences of the Addition Axioms
Any set $\mathbb{G}$ with a binary operation satisfying the addition axioms is known as an **Abelian (commutative) group**. In the case that the addition axioms are satisfied, then the following properties are also implied.

> [!Abstract] Theorem: Properties of Abelian Groups
> Let $\mathbb{G}$ be an Abelian group, and let $x,y,z \in \mathbb{G}$. Then,
> - **Cancellation Law**: If $x + y = x + z$, then $y = z$.
> - **Uniqueness of the Identity (Zero)**: If $x + y = x$, then $y = 0$.
> - **Uniqueness of the Inverse (Negative)**: If $x + y = 0$, then $y = -x$.
>
> If we define the map $x \to -x$ as the **negation** of a number, then we also have the following:
> - **Negation of Sums**: $-(x + y) = (-x) + (-y)$.
> - **Negation of Negatives**: $-(-x) = x$.

It is often the case with Abelian groups that we use the notation $nx$, $n \in \mathbb{Z}$ to denote the summation of $x$ ($x + x + \dots$) $n$ times. Then, using the fact that $\mathbb{N}$ (the set of natural numbers) is a field, we can also derive the following.

Let $\mathbb{G}$ be an Abelian group, and $x,y \in \mathbb{G}$, $m,n \in \mathbb{N}$.
- $(m + n) x = mx + nx$ and $(mn) x = n (mx)$
- $n(x + y) = nx + ny$
- $n(-x) = -(nx)$

### Consequences of the Multiplication Axioms
In the case that the multiplication axioms are satisfied, then the following properties as also implied.

> [!Abstract] Theorem: Implications of the Multiplicative Axiom
> Let $\mathbb{F}$ be a field, and let $x,y,z \in \mathbb{F}$. Then,
> - **Cancellation Law**: If $x \ne 0$ and $xy = xz$, then $y = z$.
> - **Uniqueness of the Identity (One)**: If $x \ne 0$ and $xy = x$, then $y = 1$.
> - **Uniqueness of the Inverse (Reciprocal)**: If $x \ne 0$ and $xy = 1$, then $y = x^{-1}$.
>
> If we define the map $x \to x^{-1}$ as the **reciprocation** of a number, then we also have the following:
> - **Reciprocation of Products**: If $x \ne 0$, and $y \ne 0$, then $xy \ne 0$ and $(xy)^{-1} = x^{-1} y^{-1}$.
> - **Reciprocation of Reciprocals**: If $x \ne 0$, then $(x^{-1})^{-1} = x$.

Just like with addition, we also have a convenient notation for repeated multiplications given as $x^n$, $n \in \mathbb{Z}^+$ which denotes the product of $x$ ($x * x * \dots$) $n$ times. With this notation, we have the following.

Let $\mathbb{F}$ be a field, $x,y \in \mathbb{F}$, and $m,n \in \mathbb{Z}^+$. Then,
- $x^{m + n} = x^m x^n$ and $x^{mn} = (x^m)^n$
- $(xy)^n = x^n y^n$
- If $x \ne 0$, then $x^n \ne 0$ and $(x^n)^{-1} = (x^{-1})^n$

### Consequences of the Distributive Axioms
In the case that addition and multiplication are properly related with the distributive axiom, then the following properties are implied.

> [!Abstract] Theorem: Implications of the Distributive Axiom
> Let $\mathbb{F}$ be a field, and $x,y \in \mathbb{F}$. Then,
> - **Product with Zero**: $x 0 = 0$.
> - **Factors of Zero Products**: If $xy = 0$, then $x = 0$ or $y = 0$.
> - **Negation of Products**: $(-x)y = -(xy) = x(-y)$.
> - **Reciprocal of Negations**: $(-x)^{-1} = -x^{-1}$.

Furthermore, using our addition, multiplication, and distributive axioms, we can derive the **difference of powers** and **binomial formulas**.

The **difference of powers** formula is given as
$$
x^{n+1} - y^{n+1} = (x - y) (x^n + x^{n-1} y + \dots + x^{n-k} y^k + \dots + x y^{n-1} + y^n
$$

The **binomial** formula is given as
$$
(x + y)^n = x^n + n x^{n-1} y + \dots + \frac{n!}{(n-k)! k!} x^{n-k} y^k + \dots + nxy^{n-1} + y^n
$$


# Ordered Sets
## Order Axioms
An **ordered set** is a set with a binary operator $<$, called an **order**, satisfying the following **order axioms**.

Suppose $x,y,z \in X$. Then,
$$
\begin{align}
        &\text{If} \; x < y \; \text{and} \; y < z \; \text{then} \; x < z &\text{Transitivity} \\
        &\text{Exactly} \; x < y, x = y, \; \text{or} \; y < x \; \text{is true for all} \; x,y \in X &\text{Trichotomy}
\end{align}
$$
> We are typically used to $<$ standing for "less than", though by this definition, it could also represent unconventional comparisons (ex. "greater than").

Some common notations using order are given below.

$$
\begin{align*}
        &x > y &\equiv y < x \\
        &x \le y &\equiv x < y \; \text{or} \; x = y \\
        &x \ge y &\equiv y < x \; \text{or} \; x = y \\
        &x < y < z &\equiv x < y \; \text{and} \; y < z \\
        &x < y \le z &\equiv x < y \; \text{and} \; y \le z
\end{align*}
$$

## Bounds of Ordered Sets
### Upper and Lower Bounds
Let $X$ be an ordered set, and suppose we have a subset $S \subset X$.

A point $x \in X$ is an **upper bound** of $S$ if for all $y \in S$, $y \le x$. Similarly, a point $x \in X$ is a **lower bound** of $S$ if for all $y \in S$, $x \le y$.

If $S$ has an upper bound or a lower bound, then it is said to be **bounded above** or **bounded below**, respectively. If $S$ is both bounded above and below, then it is said to be **bounded**.
> Note that by this definition, there are a variety of points in $X$ that serve as bounds for $S$! As long as a point $x \in S$ is above (or below) the greatest (or smallest) value in $S$, it serves as a bound.

> [!Example]+ Example: Upper and Lower Bounds
> Consider the interval $[a,b] \in \mathbb{R}$. Suppose $S = [a,b]$, and $X = \mathbb{R}$.
>
> Then, any point in the interval $[b,\infty) \in \mathbb{R}$ is an upper bound for $S$, and any point in the interval $(-\infty, a] \in \mathbb{R}$ is a lower bound for $S$!

### Supremums, Infimums, Maximums, Minimums
We say a point $x \in X$ is a **least upper bound (supremum)** of $S$, denoted $\text{sup} \{ z : z \in S \}$, when:
1. $x$ is an upper bound of $S$.
2. If $y \in X$ is also an upper bound of $S$, then $x \le y$.

Similarly, we say $x$ is a **greatest lower bound (infimum)** of $S$, denoted $\text{inf} \{ z : z \in S \}$, when:
1. $x$ is a lower bound of $S$.
2. If $y \in X$ is also a lower bound of $S$, then $y \le x$.

We can think of supremum and infimum as the "closest" value in $X$ that serves as an upper (or lower) bound for $S$!

We say that a point $x \in S$ is a **maximum** of $S$, denoted $\max \{ z : z \in S \}$, when $x$ is an upper bound of $S$.

Similarly, we say that a point $x \in S$ is a **minimum** of $S$, denoted $\min \{ z : z \in S \}$, when $x$ is a lower bound of $S$.

Note that while both describe similar concepts, **supremum and infimums are not the same as maximum and minimums**.

> [!Example]+ Example: Supremum / Infimum vs. Maximum / Minimum
> Note that the concept of supremums and infimums is **not** the same as maximum and minimums! Even though both serve as upper (and lower) bounds for $S$, some sets may lack maximum and minimums.
>
> For example, consider the open interval $(a,b) \in \mathbb{R}$. This interval does not have a maximum or minimum, yet has a supremum of $b$, and an infimum of $a$. 

### Least Upper Bound Property
Suppose we have an ordered set $X$. Then, $X$ is said to have the **least upper bound property** whenever every nonempty subset of $X$ with an upper bound has a least upper bound.

> [!Abstract] Theorem
> Let $X$ be an ordered set with the least upper bound property. Then, every nonempty subset of $X$ with a lower bound has a greatest lower bound.

Some sets such as $\mathbb{N}$ and $\mathbb{Z}$ have the least upper bound property, but not all! For example, consider $\mathbb{Q}$ (the set of rationals).

> [!Example]+ Example: $\mathbb{Q}$ and the Least Upper Bound Property
> To show that $\mathbb{Q}$ does not have the least upper bound property, we show subsets that lack a least upper bound.
>
> Consider the sets
> $$
> S = \{ r \in \mathbb{Q} : r > 0, r^2 < 2 \} \qquad \bar{S} = \{ r \in \mathbb{Q} : r > 0, r^2 > 2 \} 
> $$
>
> We can see that both sets of non-empty. Furthermore, we see that every point in $\bar{S}$ is an upper bound for $S$.
>
> We see that as an irrational number, $r^2 = 2$ is not in $\mathbb{Q}$. Because of this, if $p$ is a least upper bound of $S$, then $p$ must either be in $S$ or $\bar{S}$. We can prove that both cases cannot be true using Newton's method (apply it to find a $q$ greater than or less than $p$, showing it cannot be a supremum or infimum), to show that $S$ lacks a least upper bound.


# Ordered Fields
## Ordered Field Axioms
An ordered set $(\mathbb{F}, <)$ where $\mathbb{F}$ is a field, is called an **ordered field** whenever the following ordered field axioms are satisfied:
1. If $x,y,z \in \mathbb{F}$, then $x < y$ implies $x + z < y + z$
2. If $x,y \in \mathbb{F}$, then $0 < x$ and $0 < y$ implies $0 < xy$

Given an ordered field $\mathbb{F}$, and an element $x \in \mathbb{F}$, we say $x$ is **positive** when $x > 0$. We similarly have descriptions for $x$ when $x < 0$ (negative), $x \ge 0$ (non-negative), $x \le 0$ (non-positive).
> We often denote the set of all positive elements of $\mathbb{F}$ as $\mathbb{F}_+$, and the set of all negative elements as $\mathbb{F}_-$.

> [!Example]+ Example: Ordered Fields
> We can easily see that $\mathbb{Q}$ and $\mathbb{R}$ are ordered fields. 

## Consequences of the Ordered Field Axioms
From these ordered field axioms, we can use many of the inequality rules we are used to using in the context of $\mathbb{R}$. Some of these rules are given in the following theorem.

> [!Abstract] Theorem: Inequality Rules
> Let $\mathbb{F}$ be an ordered field. Then, the following must be true.
> 1. If $x > 0$, then $-x < 0$, and vice versa.
> 2. If $x > 0$ and $y < z$, then $y < x + z$ and $x y < x z$.
> 3. If $x < 0$ and $y < z$, then $x + y < z$ and $x y > x z$.
> 4. If $x \ne 0$ then $x^2 > 0$.
> 5. If $0 < x < y$ and $n \in \mathbb{Z}_+$, then $0 < x^n < y^n$ and $0 < y^{0n} < x^{-n}$.

Using the above inequality rules, we find that given an ordered field $\mathbb{F}$, $\mathbb{F}_+$ satisfies the following **positivity properties**.
1. If $x,y \in \mathbb{F}_+$, then $x + y \in \mathbb{F}_+$ and $xy \in \mathbb{F}_+$
2. For every $x \in \mathbb{F}$, exactly one of $x \in \mathbb{F}_+$, $-x \in \mathbb{F}_+$, or $x = 0$ is true.

Interestingly enough, these properties can be used to define an ordered field. See the below theorem.

> [!Abstract] Theorem: Positivity Properties and Ordered Fields
> Let $\mathbb{F}$ be a field, and suppose $\mathbb{F}_+ \subset \mathbb{F}$ satisfies the positivity properties. Define the binary relation $<$ on $\mathbb{F}$ as
> $$
> x < y \Longrightarrow y - x \in \mathbb{F}_+
> $$
>
> Then, $(\mathbb{F}, <)$ is an ordered field.

## The Absolute Value Function
Suppose $\mathbb{F}$ is an ordered field. We can naturally create an **absolute value function** for it, defined as
$$
|x| =
\begin{cases}
        x & x > 0 \\
        0 & x = 0 \\
        -x & x < 0
\end{cases}
$$

Properties of the absolute value function are given in the as follows. Note that each of them can be proven from the definition of absolute value, as well as the ordered field axioms.

> [!Abstract] Theorem: Properties of the Absolute Value
> Let $\mathbb{F}$ be an ordered field. Then, for $x,y \in \mathbb{F}$, the following properties hold true.
> $$
> \begin{align*}
>         &|x| \ge 0 &\text{Non-Negativity} \\
>         &|x| = 0 \iff x = 0 &\text{Definiteness} \\
>         &|x + y| \le |x| + |y| &\text{Triangle Inequality} \\
>         &|xy| = |x| \; |y| &\text{Multiplicativity} \\
>         &\left| |x| - |y| \right| \le |x - y| &\text{Difference Inequality}
> \end{align*}
> $$

Define the **distance** between two points $x,y \in \mathbb{F}$ as the function $d(x,y) = |x - y|$. Such a distance function satisfies the following properties.

> [!Abstract] Theorem: Properties of the Distance Function
> Suppose $\mathbb{F}$ be an ordered field, and let $d(x,y)$ be the distance. Then, for every $x,y,z \in \mathbb{F}$, the following properties hold.
> $$
> \begin{align*}
>         &d(x,y) \ge 0 &\text{Non-Negativity} \\
>         &d(x,y) = 0 \iff x = 0 &\text{Definiteness} \\
>         &d(x,y) = d(y,x) &\text{Symmetry} \\
>         &d(x,z) \le d(x,y) + d(y,z) &\text{Triangle Inequality} 
> \end{align*}
> $$

We can also use the absolute value function to characterize bounded sets. If $\mathbb{F}$ is an ordered field, then a subset $S \subset \mathbb{F}$ is bounded if and only if there exists an $m \in \mathbb{F}_+$ such that

$$
x \in S \Longrightarrow |x| \le m 
$$
In other words, there exists a number in $\mathbb{F}_+$ serving as an upper and lower limit for the elements in $S$.


# Real Numbers
Using such definitions, we can define the real number system. First, consider the following theorem.

> [!Abstract] Theorem
> There exists a unique ordered field with the least upper bound property that contains $\mathbb{Q}$ as a subfield.
> > Proofs of this theorem are quite long and technical.

The **real numbers**, denoted $\mathbb{R}$, is formally defined as this unique ordered field with the least upper bound property containing $\mathbb{Q}$ as a subfield. By the above theorem, its existence is guaranteed.
> In other words, any subset (interval) of $\mathbb{R}$ has very explicit bounds which we can state, and such a field encompasses all of $\mathbb{Q}$.

## Powers
Due to the existence of a least upper bound property, the existence of the real numbers lets us show the existence of solutions to many equations involving powers! Before, under $\mathbb{Q}$, this was not possible.

> [!Abstract] Theorem: Existence of Powers
> In fact, under the real numbers, we can show that for every $x \in \mathbb{R}_+$, and every $n \in \mathbb{Z}_+$, where exists a unique $y \in \mathbb{R}_+$ such that $y^n = x$. While such a fact may seem obvious, it can also be formally proven!
>
> > [!Note]- Proof
> > We wish to show that a $y$ such that $y^n = x$ exists. Consider the sets given by
> > 
> > $$
> > S = \{ r \in \mathbb{R}_+ : r^n < x \} \qquad \bar{S} = \{ r \in \mathbb{R}_+ : r^n  > x \} 
> > $$
> >
> > First, we show that both sets are non-empty.
> > 1. We show $S$ is non-empty. Define $s = x / (1 + x)$.
> >
> >    We can manipulate this to obtain $s = x - sx$, and as both $s$ and $x$ are positive, it must be true that $s < x$. Furthermore, as $s = x / (1 + x)$ is less than 1, by property of powers, $s^n < s$. Thus, we have explicitly constructed an element in $\mathbb{R}_+$ that belongs in $S$, as $s^n < s < x$.
> >
> > 2. We now show that $\bar{S}$ is non-empty. Define $s = 1 + x$. We can easily see that $s^n = (1 + x)^n$ is greater than $x$, as $x$ is by assumption a positive number.
> >
> > Observe that every point in $\bar{S}$ is an upper bound for $S$. Furthermore, observe that $S \cup \{ x \} \cup \bar{S}$ are disjoint sets.
> >
> > Thus, if $y$ is the supremum of $S$, by trichotomy, $y$ must be in $S$, $\bar{S}$, or $y^n = x$. We show that the first two are not true, forcing $y^n = x$.
> > 1. Let $p \in S$. Applying one iteration of Newton's method to $f(r) = 1 - x / r^n = 0$, we can find a $q \in S$ such that $p < q$, showing that the supremum $y$ cannot be in $S$.
> > 2. Let $p \in \bar{S}$. Applying one iteration of Newton's method to $f(r) = r^n - x = 0$, we can find a $q \in \bar{S}$ such that $q < p$, showing that the supremum $y$ cannot be in $\bar{S}$.
> >
> > This forces $x = y^n$.

Using this theorem, we can prove the following. Let $x \in \mathbb{R}_+$. Then,
$$
(x^\frac{1}{n})^m = (x^m)^\frac{1}{n}
$$
> We can do this by showing that both $(x^\frac{1}{n})^m$ and $(x^m)^\frac{1}{n}$ satisfy $y^n = x^m$, and using the uniqueness trait of our previous theorem to show equality.

Define $x^\frac{m}{n} = (x^\frac{1}{n})^m = (x^m)^\frac{1}{n}$ as $x^p$ for all $x \in \mathbb{R}_+$ and $p \in \mathbb{Q}$. We can use this to define $x^r$ for all $x \in \mathbb{R}_+$ and $r \in \mathbb{R}$, by defining $x^r$ as
$$
x^r =
\begin{cases}
        \text{sup} \{ x^p : p \in \mathbb{Q}, p < r \} & x \ge 1 \\
        \text{sup} \{ x^p : p \in \mathbb{Q}, p > r \} & 0 < x < 1
\end{cases}
$$

Which can be used to derive the following properties of power. Let $x,y \in \mathbb{R}_+$, and $r,s \in \mathbb{R}$. Then,
1. $x^{r + s} = x^r x^s$
2. $(xy)^r = x^r y^r$
3. $x^{rs} = (x^r)^s$


## Intervals
An **interval** is a special subset of $\mathbb{R}$ containing all values $x \in \mathbb{R}$ between two bounds. We denote intervals using **interval notation**.

Let $a,b \in \mathbb{R}$. We can define the following intervals.

$$
\begin{align*}
        &\varnothing = \text{The Empty Set} &[a,a] = \{a\} \\
        &(a,b) = \{ x \in \mathbb{R} : a < x < b \} &[a,b) = \{ x \in \mathbb{R} : a \le x < b \} \\
        &(a,b] = \{ x \in \mathbb{R} : a < x \le b \} &[a,b] = \{ x \in \mathbb{R} : a \le x \le b \}
\end{align*}
$$

In the case that both $a$ and $b$ are used, we call them the **left endpoint** and **right endpoint**, respectively. Similarly, we also define

$$
\begin{align*}
        &(a,\infty) = \{ x \in \mathbb{R} : a < x \} &(-\infty,b) = \{ x \in \mathbb{R} : x < b \} \\
        &[a,\infty) = \{ x \in \mathbb{R} : a \le x \} &(-\infty,b] = \{ x \in \mathbb{R} : x \le b \}
\end{align*}
$$

An endpoint is said to be **closed** if it is contained inside of the interval, and said to be **open** otherwise. Furthermore, we say an interval is **closed** if all of its endpoints are closed, and **open** if all of its endpoints are open.

## Properties of the Real Numbers
The following properties relate the real numbers with the positive integers $\mathbb{Z}_+$, the integeres $\mathbb{Z}$, and the rationals $\mathbb{Q}$.

> [!Abstract] Theorem: Properties of the Real Numbers
> The following are true.
> 1. **Archimedean Property**: If $x,y \in \mathbb{R}$ and $x > 0$, then there exists $n \in \mathbb{Z}_+$ such that
>    $$
>    nx > y
>    $$
> 2. **Uniformity of Integers**: If $x \in \mathbb{R}$ then there exists a unique $m \in \mathbb{Z}$ such that
>    $$
>    m \in (x - 1, x]
>    $$
> 3. **Denseness of $\mathbb{Q}$**: If $x,y \in \mathbb{R}$ and $x < y$, then there exists a $q \in \mathbb{Q}$ such that
>    $$
>    x < q < y
>    $$

Such properties can be proven.

