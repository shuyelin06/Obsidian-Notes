---
title: Math410Working
tags:
- math410
- wip
---

*We discuss series and sequences*

# Sequences
A **sequence** is a function $f: \mathbb{N} \to \mathbb{R}$ that takes in a natural number $n \in \mathbb{N}$ as input, and returns a real number.

Letting $n \in \mathbb{N}$, we typically write a sequence in one of the following ways:
$$
\begin{align*}
        &a_n = f(n) \\
        &\{ a_n \}_{n=1}^\infty \\
        &\{ a_n \}
\end{align*}
$$

Sequences can really be anything we want - they don't necessarily have to follow a pattern.

> [!Example]+ Example: Fibonacci Sequence
> An example of a sequence is the **Fibonacci Sequence**, defined as $a_n = a_{n-1} + a_{n-2}$.
> $$
> 1,1,2,3,5,8,\dots
> $$

## Properties of Sequences
### Convergence of Sequences
Given a sequence $a_n$, we say that the $a_n \to a$ as $n \to \infty$, alternatively denoted as $\lim_{n\to\infty} a_n = a$, if
$$
\forall \epsilon > 0, \exists N \in \mathbb{N} : \forall n \ge N, (|a_n - a| < \epsilon)
$$
Intuitively, this is saying that for all epsilon values, we can find a term in the sequence such that all terms after are within some range around $a$ (the range $(a - \epsilon, a + \epsilon)$.
> By this definition, you need to find an $N$ given $a$ and $\epsilon$ that satisfies our definition. Note that by this definition, we need to know what $a$ is.

> [!Example]+ Example: Convergence of Sequences
> Let $a_n = 1 / n$. Prove that $a_n \to 0$.
>
> Let $\epsilon > 0$ and $a = 0$.
>
> **Scratch Work**: We want
> $$
> \left| \frac{1}{n} - 0 \right| < \epsilon \Longrightarrow \frac{1}{n} < \epsilon
> $$
> So we can choose a $N \in \mathbb{N}$ such that $1 / N < \epsilon$ to satisfy our definition, and this $N$'s existence is guaranteed by the Archimedian property.
>
> **Formal Proof**: Fix any $\epsilon > 0$, and let $N \in \mathbb{N}$ such that $1 / N < \epsilon$. Then, $\forall n \ge \mathbb{N}$, we have
> $$
> \left| \frac{1}{n} - 0 \right| = \frac{1}{n} \le \frac{1}{N} < \epsilon
> $$

> [!Example]- Example: Convergence of Sequences (2)
> Prove that
> $$
> \frac{1}{a_n} \to \frac{1}{2}
> $$
> if $a_n \to 2$ as $n \to \infty$.
> 
> **Scratch Work**: Let $\epsilon > 0$. We want
> $$
> \left| \frac{1}{a_n} - \frac{1}{2} \right| = \frac{|2 - a_n|}{2 |a_n|} < \epsilon \\
> $$
> 1. Using the limit definition, we know that provided that $n \ge N_1$ for some $N_1 \in \mathbb{N}$,
>    $$
>    |2 - a_n| < 2 \epsilon
>    $$
>    So, we know that
>    $$
>    \frac{|2 - a_n|}{2 |a_n|} < \frac{2 \epsilon}{2 |a_n|}
>    $$
>    Provided that $n \ge N_1$.
> 2. Furthermore, using the limit definition, we know that provided we choose $N_2 \in \mathbb{N}$ such that $\forall n \in \mathbb{N}$,
>    $$
>    |a_n - 2| < 1 \Longrightarrow
>    $$
>    So for $n \ge N_2$, we bound $a_n$ by $1 < a_n < 3$, which forces $1 / a_n < 1$. So,
>    $$
>    \frac{2 \epsilon}{2 |a_n|} < \epsilon
>    $$
>    Provided that $n \ge N_2$.
> 
> **Proof**: Fix any $\epsilon > 0$.
> - Let $N_1 \in \mathbb{N}$ such that $|a_2 - 2| < 2 \epsilon$, $\forall n \ge N_1$.
> - Let $N_2 \in \mathbb{N}$ such that $|a_2 - 2| < 1$, $\forall n \ge \mathbb{N_2}$.
> 
> Choose $N = \max(N_1, N_2)$. Then, $\forall n \ge N_1$,
> $$
> \left| \frac{1}{a_n} - \frac{1}{2} \right| = \frac{|2 - a_n|}{2 |a_n|} < \frac{2 \epsilon}{2} = \epsilon
> $$

> [!Example]- Example: Divergence of a Sequence
> Consider the sequence $\{(-1)^n\}$. Does it converge?
>
> No! Choose $\epsilon = 1/10$. Then, $\forall n \ge N$, 
> $$
> |x_n - x| \le \frac{1}{10}
> $$
> But this isn't possible, as the -1 and 1 elements are distance 2 apart!

> [!Abstract] Theorem: Limit Rules
> If $a_n$ and $b_n$ are sequences such that $a_n \to a$, $b_n \to b$, then
> $$
> \begin{align}
> a_n \pm b_n &\to a \pm b \\
> a_n b_n &\to ab \\
> \frac{a_n}{b_n} &\to \frac{a}{b}
> \end{align}
> $$

> [!Abstract] Theorem: Comparison Lemma; Squeeze Theorem
> Let $a_n$ be a sequence such that $a_n \to a$, and assume there exists some $C \in \mathbb{R}^+$ and $N_1 \in \mathbb{N}$ such that
> $$
> |b_n - b| \le C |a_n - a|, \forall n \ge N
> $$
> Then, $b_n \to b$.
> 
> > [!Note]- Proof (Scratch)
> >
> > **Scratch Work**: Fix any $\epsilon > 0$.
> > Choose some $N_1$ such that $\forall n \ge N_1$, $|a_n - a| < \epsilon$ so that our convergence applies. We have
> > $$
> > |b_n - b| \le C |a_n - a|
> > $$
> > Choose some $N_2$ such that $\forall n \ge N_2$, $|a_n - a| < \frac{\epsilon}{C}$. We have
> > $$
> > C |a_n - a| < \epsilon
> > $$

### Sequence Bounds
We say that a sequence $\{x_n\}$ is **bounded** if
$$
\exists M \in \mathbb{R} : \forall n \in \mathbb{N}, |x_n| \le M
$$

> [!Abstract] Theorem: Convergence and Bounds
> Let $\{a_n\}$ be a sequence. If $\{a_n\}$ converges, then $\{a_n\}$ is bounded.
> 
> > [!Note]- Proof
> > 
> > Suppose $a_n \to a$. Then,
> > 
> > $$
> > \begin{align*}
> >     |a_n| &= |a_n (- a + a)| \\
> >         &\le |a_n - a| + |a| \\
> >         &\le \epsilon + |a| &\text{Provided} \; n \ge N \\
> > \end{align*}
> > $$
> > This doesn't show a bound for all $n$, only $n \ge N$! However, we note that before $N$, we only have a finite number of terms. So, we can just take the max of all possible terms as a bound!
> > 
> > Let $M = \max(|a_1|, |a_2|, \dots |a_{N-1}|, \epsilon + |a|)$. Now, $\forall n \in \mathbb{N}$, we have $|a_n| \le M$.

### Sequential Density
A set $S$ is **sequentially dense in $\mathbb{R}$** if $\forall x \in \mathbb{R}$, 
$$
\exists \{x_n\} \in S : x_n \to x
$$
In other words, a set is sequentially dense if we can find a sequence in our set that converges to any real number we choose. 
> Note that density and sequential density mean the same thing.

> [!Abstract] Theorem: Density and Sequentially Density
> A set $S$ is dense if any only if $S$ is sequentially dense.
>
> > [!Note]- Proof
> > 
> > We will only prove one direction for the sake of example.
> > 
> > #### **Proof ($\to$)**
> > Consider a set $S$, and assume it is dense. We want to show that $S$ is sequentially dense.
> > 
> > Fix any $x$ in $\mathbb{R}$. Choose the interval $\left( x, x + \frac{1}{n} \right)$. By the definition of density, $\exists s_n \in S$ such that 
> > $$
> > s_n \in \left( x, x + \frac{1}{n} \right)
> > $$
> > For any $n \in \mathbb{N}$.
> > 
> > So, $|s_n - x| < \frac{1}{n}$, making $s_n \to x$ as $n \to \infty$ by the Comparison Lemma.

### Closed Sets
We say a set $S \subseteq \mathbb{R}$ is **closed** if for all sequences $x_n \in S$ converge to $x$ with $x_n \to x$, then the limit exists in $S$ ($x \in S$).

> [!Example]+ Example: Closed Sets Disproof
> Let $S = \mathbb{Q}$. This is not closed, as we could choose the sequence
> $$
> 3.1, 3.14, \dots \to \pi \not\in \mathbb{Q}
> $$

> [!Example]- Example: Closed Sets Disproof (2)
> Let $S = (0,1)$. This is not closed, as we could choose the sequence
> $$
> \left\{ \frac{1}{n} \right\}_{n=2}^\infty \to 0 \not\in (0,1)
> $$

> [!Example]+ Example: Closed Sets Proof
> Let $S = \{ \pi \}$. This is a closed set, as the only possible sequence is
> $$
> \pi, \pi, \pi, \dots \to \pi
> $$
> Which is in $\{\pi\}$.

> [!Example] Example: Closed Sets Proof
> Let $S = [0,\infty)$. This is closed!
>
> For any $\{x_n\}$ such that $x_n > 0$ and $x_n \to x$, then it follows that $x \ge 0$. We need to prove this (by contradiction) - show that if we converge to a negative number, then our sequence would be "stuck" there, and could not go till infinity.
