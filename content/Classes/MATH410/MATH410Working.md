---
title: Math410Working
tags:
- math410
- wip
---

*We discuss series and sequences*

(Continuity)

# Functions
## Continuity
Suppose we have a function that maps from one domain $D$ to $\mathbb{R}$, $f: D \to \mathbb{R}$. 

We say $f$ is **continuous** at $x_0 \in D$, if whenever any sequence $\{x_n\} \in D$ converges to $x_0$, so too does the sequence $\{f(x_n)\}$. More formally,
$$
\{x_n\} \to x_0 \Longrightarrow \{f(x_n)\} \to f(x_0)
$$
We can similarly think of this in terms of the limit definition,
$$
\lim_{n\to\infty} f(x_n) = f \left( \lim_{n\to\infty} x_n \right) = f(x_0)
$$
Which we can show to prove continuity.

> [!Example]+ Example: Continuity Proof
> Prove $f: \mathbb{R} \to \mathbb{R}, f(x) = x^3$ is continuous.
> 
> Take any real number $x_0$, and take any convergent sequence $\{x_n\} \to x_0$. Then, applying the product property of the limits,
> $$
> \lim_{n\to\infty} (x_n)^3 = (\lim_{n\to\infty} x_n)^3 = (x_0)^3
> $$

> [!Example]- Example: Continuity Disproof
> Prove that $f: \mathbb{R} \to \mathbb{R}$
> $$
> f = \begin{cases}
>        1 & x < 0 \\
>        2 & x \ge 0
>     \end{cases}
> $$
> is not continuous.
>
> Let us have sequence $\{-1/n\}$, which converges to 0. However, $f(-1/n)$ will converge to 1, which is not equal to $f(0) = 2$!

> [!Abstract] Theorem: Properties of Continuity 
> Let $f$ and $g$ be continuous functions. Then $fg$, $\frac{f}{g}$, $f + g$, $f - g$, $f \circ g$ are also continuous.
> 
> > These properties trivially follow from the limit properties.

Continuity yields a lot of interesting results! See the below.

### Extreme Value Theorem
Let $f$ be a function.

Then, $x_0 \in [a,b]$ is a **maximizer** of $f$, $f(x_0)$ the **maximum** of $f$, if 
$$
f(x_0) \ge f(x) \forall x \in [a,b]
$$
Similarly, $x_0 \in [a,b]$ is a **minimizer** of $f$, $f(x_0)$ the **minimum**, if
$$
f(x_0) \le f(x) \forall x \in [a,b]
$$

Continuity guarantees the existence of a maximum and/or minimum along the domain of a continuous function. This is known as the **Extreme Value Theorem**.

> [!Abstract] Theorem: Extreme Value Theorem 
> Let $f: [a,b] \to \mathbb{R}$ be continuous. Then, the maximum and minimum of $f$ exist.
>
> > In this theorem, the two key assumptions we need are compactness of $[a,b]$, and the continuity on $f$.
>
> > [!Note] Proof
> > 
> > Let $D = [a,b]$. First, by way of contradiction, we show that $\sup(f(D))$ exists. Then, we show that there exists a $x_0 \in D$ such that 
> > $$
> > f(x_0) = \sup_x (f(D))
> > $$
> > 
> > *Proof ommitted - refer to book*

### Intermediate Value Theorem
Continuity also guarantees the existence of values within a range of a continuous function.

> [!Abstract] Theorem: Intermediate Value Theorem
> Let $f : [a,b] \to \mathbb{R}$ be a continuous function.
>
> Pick any $c$ in the interval $f(x_1) < c < f(x_2)$, where $x_1$ and $x_2$ are in the interior of $[a,b]$. Then, there exists an $x$ strictly between $x_1$ and $x_2$ such that $f(x) = c$.
>
> > The proof is ommitted, as it is long and technical. It uses the Nested Interval Theorem and Bisection Method.

### Continuity Along Intervals
We define an **interval** $I$ if for any $u,v \in I$, then $[u,v] \subseteq I$.

> [!Abstract] Theorem: Continuity along Intervals
> If $f : I \to \mathbb{R}$ is a continuous function where $I$ is an interval, then the output $f(I)$ is also an interval.
> 
> > [!Note]- Proof
> >
> > Let $y_1, y_2 \in f(I)$, and choose any value $C \in (y_1, y_2)$. Without loss of generality, suppose $y_1 < y_2$. We wish to show that $C$ exists within $(y_1, y_2)$, which by definition shows the existence of the interval between $y_1, y_2$.
> > 
> > We know that
> > $$
> > f(x_1) < c < f(x_2)
> > $$
> > And thus, by the intermediate value theorem, there exists some $x$ between $x_1$ and $x_2$ such that $f(x) = c$, 
> > 
> > Note that for this proof to work, we assumed that $[x_1, x_2]$ is an interval.
