---
title: Sequences
tags:
- math410
---

# Sequences
## Introduction
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

## Properties of Sequences
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

> [!Example]- Example: Closed Sets Proof
> Let $S = [0,\infty)$. This is closed!
>
> For any $\{x_n\}$ such that $x_n > 0$ and $x_n \to x$, then it follows that $x \ge 0$. We need to prove this (by contradiction) - show that if we converge to a negative number, then our sequence would be "stuck" there, and could not go till infinity.


### Monotonicity
Let $\{a_n\}$ be a sequence. 

We say that $\{a_n\}$ is **monotone (increasing)** if $\forall n$,
$$
a_{n+1} \ge a_n
$$

Similarly, we say that $\{a_n\}$ is **monotone (decreasing)** if $\forall n$,
$$
a_{n+1} \le a_n
$$

There exist respective strictly increasing ($>$) and strictly decreasing definitions as well!

> [!Abstract] Theorem: Monotone Convergence Theorem
> Let $\{a_n\}$ be monotone. Then, $\{a_n\}$ converges if and only if $\{a_n\}$ is bounded.
> - If monotone increasing, then $a_n \to \sup_{n \ge 1} \{a_n\}$.
> - If monotone decreasing, then $a_n \to \inf_{n \ge 1} \{a_n\}$.
>
> > Recall that by our definition of convergence, the converse was not true. In the case of monotonicity, it is true!
>
> > [!Note]- Proof
> >
> > We prove the backwards direction ($\leftarrow$), as the forwards direction follows by definition of convergence.
> > 
> > Let $\{a_n\}$ be bounded. Without loss of generality, assume $\{a_n\}$ is monotone increasing (if it is monotone decreasing, just flip the sequence with $-1$), and bounded.
> > 
> > Let $S = \{a_n : n \in \mathbb{N}\}$. Because we know that $S$ is bounded, $\sup(S)$ exists, so let $l = \sup(S)$.
> > 
> > Recall that by the $\epsilon$ definition of supremums, $\forall \epsilon > 0$, there $\exists a_N \in S, N \in \mathbb{N}$ such that
> > $$
> > \begin{align*}
> >     l - \epsilon &< a_N \\
> >         &\le a_n, \forall n \ge N &\text{Monotonicity Assumption} \\
> >         &< l &\text{Definition of Supremum} \\
> >         &< l + \epsilon 
> > \end{align*}
> > $$
> > 
> > Thus, $\forall \epsilon > 0$, we have found an $N \in \mathbb{N}$ such that $\forall n \ge N$, 
> > $$
> > l - \epsilon < a_n < l + \epsilon \Longrightarrow |a_n - l| < \epsilon
> > $$
> > So by definition, our sequence converges.

> [!Example]- Example: Monotone Convergence
> $$
> S_n = \sum_{k=3}^n \frac{1}{2^k k^2}
> $$
> Prove that $S_n$ converges as $n \to \infty$.
> 
> Using the monotone convergence theorem, we want to show that $S_n$ is monotone and that $S_n$ is bounded.
> 
> #### Monotone Proof
> We can easily see that $S_n$ is monotone increasing, as we're adding more positive terms to every subsequent $S_{n+1}$ term. Thus,
> $$
> S_{n+1} \ge S_n
> $$
> 
> #### Bound Proof
> If $S_n$ is bounded, then $|a_n| \le M$. We find $M$ show that $S_n$ is bounded.
> $$
> \begin{align*}
>     \left| \sum_{k=3}^n \frac{1}{2^k k^2} \right|
>     &\le \sum_{k=3}^n \left| \frac{1}{2^k k^2} \right| \\
>     &\le \sum_{k=3}^n \frac{1}{2^k k^2} \\
>     &\le \sum_{k=3}^n \frac{1}{2^k} \\
>     &\le \sum_{k=0}^\infty \frac{1}{2^k} \\
>     &\le 2
> \end{align*}
> $$
> We've shown that $S_n$ is bounded by 2.

> [!Abstract] Theorem
> Let $|c| < 1$. Then, $\{c^n\} \to 0$.
>
> > [!Note]- Proof (Sketch)
> > 
> > 1. If $c = 0$, it's clear that we converge to 0.
> > 2. Without loss of generality (in the negative case, the absolute value gets rid of the negative), we can assume that $0 < c < 1$.
> >    
> >    We would want to show that $c^n$ is monotone decreasing, and bounded below by 0. So, by the monotone convergence theorem, we show convergence to the infimum. We end by showing that the infimum is 0.

# Subsequences 
## Introduction
Let $\{n_k\}_{k=1}^\infty$ be a strictly increasing sequence in $\mathbb{N}$. Then, we say 
$$
\{b_k\}_{k=1}^\infty = \{a_{n_k}\}_{k=1}^\infty
$$ 
is a **subsequence** of $\{a_n\}_{n=1}^\infty$.
> Note that by this definition, $\{a_n\}_{n=1}^\infty$ can be a subsequence of itself (choose $n_k = k, \forall k \in \mathbb{N}$)

> [!Info] Corollary
> Note by the definition of a subsequence, it must be true that $\forall k \in \mathbb{N}$, $n_k \ge k$.
>
> > [!Note]- Proof
> >
> > As a base case, note that $n_1 \ge 1$ because $n_1$ must be a natural number.
> > 
> > Now, as an inductive step, suppose $n_k \ge k$ for all $k \in \mathbb{N}$. Then 
> > $$
> > \begin{align*}
> >     n_{k+1} 
> >     &> n_k &\text{Strictly Increasing Definition} \\
> >     &\ge k &\text{Assumption}
> > \end{align*}
> > $$
> > So, because $n_{k+1}$ is a natural number, $n_{k+1} \ge k + 1$.

Informally, a subsequence is a "choice" of the elements in the sequence (left to right) - for every element in our sequence, we decide whether we want it or not in our subsequence.

> [!Example]+ Example: Subsequence
> $$
> \{a_n\}_{n=1}^\infty = \{ 0, 1, 2, 3, 4, \dots \}
> $$
> 
> Suppose we have subsequence
> $$
> \{a_{n_k}\}_{k=1}^\infty = \{0,2,4,6,\dots\}
> $$
> 
> Then, $n_1 = 1$, $n_2 = 3$, $n_3 = 5$, and so on, telling us that
> $$
> \{a_{n_k}\}_{k=1}^\infty = \{a_{2k-1}\}_{k=1}^\infty
> $$

> [!Example]- Example: Not a Subsequence
> $$
> \{a_n\} = \{0,1,2,3,4, \dots\}
> $$
>
> The sequence 
> $$
> \{1,1,1,1,1,\dots\}
> $$
> 
> Is **not** a subsequence of $\{a_n\}$, as $n_k$ is not strictly increasing ($n_k = 1, \forall k \in \mathbb{N}$)

## Convergence of Subsequences
Because $n_k$ is strictly increasing, we can show the following.

> [!Abstract] Theorem: Convergence of Subsequences
> If sequence $\{a_n\} \to a$, then any subsequence $\{a_{n_k}\} \to a$.
>
> > [!Note]- Proof
> >
> > By definition, $\forall \epsilon > 0$, there exists a $N \in \mathbb{N}$ such that $\forall k \ge N$,
> > $$
> > | a_k - a | < \epsilon
> > $$
> > But $n_k \ge k$ for all $k \in \mathbb{N}$, so for all $\epsilon > 0$, we show that there exists a $N \in \mathbb{N}$ such that $\forall k \ge N$,
> > $$
> > | a_{n_k} - a | < \epsilon
> > $$
> > So by definition, $a_{n_k} \to a$ as $k \to \infty$.

See the below example.

> [!Example]+ Example: Convergence of Subsequenes
> $$
> \{a_n\} = \left\{ 1, \frac 1 2, \frac 1 3, \frac 1 4, \dots \right\} = \left\{ \frac{1}{n} \right\}_{n=1}^\infty \to 0
> $$
> 
> Then, the following subsequence also converges to 0. Let $n_k = k^2$.
> $$
> \left\{ \frac{1}{k^2} \right\}_{k=1}^\infty \to 0
> $$

We can additionally use the idea of monotonicity to show convergence of subsequences. 

> [!Abstract] Theorem: Monotone Subsequence Theorem
> Any sequence has a monotone subsequence.

> [!Abstract] Theorem: Bolzano-Weierstrass Theorem
> Any bounded sequence contains a convergent subsequence.
>
> > [!Note]- Proof
> > 
> > Let $\{a_n\}$ be bounded. Then, $\{a_n\}$ contains a monotone subsequence, and because the subsequence is bounded, it converges by the Monotone Convergence Theorem.

## Sequential Compactness
A subset $S$ of $\mathbb{R}$ is **sequentially compact (compact)** if any sequence $\{a_n\}$ of $S$ has a subsequence converging to an element of $S$. 
> The convergence of a subsequence is guaranteed by the previous theorem!

> [!Abstract] Sequential Compactness
> In $\mathbb{R}$ (or $\mathbb{R}^n$), a set $S$ is sequentially compact if and only if it is closed and bounded.
>
> > [!Note]- Proof
> >
> > #### Proof ($\leftarrow$):
> > Suppose $S$ is closed and bounded. By the Bolzano-Weierstrass Theorem, any sequence $\{a_n\}$ in $S$ will contain a subsequence $\{a_{n_k}\}$ that converges to some $x_0$. But $S$ is closed, so the limit must be in $S$.
> > 
> > #### Proof ($\rightarrow$)
> > Let $S$ be sequentially compact.
> > 
> > We prove that $S$ is closed. So let us have a sequence $\{a_n\} \in S$ such that$\{a_n\} \to x_0$. We prove that this limit lies within $S$. By the definition of compactness, $\{a_n\}$ has a subsequence $\{a_{n_k}\}$ that converges to some $x_1 \in S$. However, by our sequence convergence theorem, if $\{a_n\} \to x_0$, then $\{a_{n_k}\} \to x_0$! So, by the uniqueness of limits, $x_0 = x_1$, meaning that $x_0 \in S$.
> > 
> > We prove that $S$ is bounded. By way of contradiction, suppose $S$ is not bounded. Then, there exists some sequence in $S$ such that $\forall n \in \mathbb{N}$, $|x_n| > n$. Any subsequence of this sequence must also "blow up", meaning that there does not exist any subsequence that converges to an element in $S$. This is a contradiction!


> [!Example]+ Example: Sequential Compactness
> Let $S = [0,5]$. $S$ is closed and bounded, so it is compact, meaning that for any sequence taken from $S$, it has a subsequence that converges to $x \in S$.
