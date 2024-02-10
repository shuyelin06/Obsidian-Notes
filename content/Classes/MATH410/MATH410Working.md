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
\{x_n\} \to x_0 \Longrightarrow \{f(x_n)\} \to x_0
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

> [!Abstract] Theorem: Continuity 
> Let $f$ and $g$ be continuous functions. Then $fg$, $\frac{f}{g}$, $f + g$, $f - g$, $f \circ g$ are also continuous.
> 
> > These properties trivially follow from the limit properties.

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

> [!Abstract] Theorem: Extreme Value Theorem 
> Let $f: [a,b] \to \mathbb{R}$ be continuous. Then, the maximum and minimum of $f$ exist.
>
> > In this theorem, the two key assumptions we need are compactness of $[a,b]$, and the continuity on $f$.
>
> > [!Note] Proof
> > 
Let $D = [a,b]$. First, we show that $\sup f(D)$ exists (show by contradiction). Then, we show that there exists a $x_0 \in D$ such that 
$$
f(x_0) = \sup_x f(D)
$$

