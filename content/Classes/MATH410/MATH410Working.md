---
title: Math410Working
tags:
- math410
- wip
---

*We discuss series and sequences*

(Continuity)

# Functions
For a subset of the real numbers $D$, we denote a function $f$
$$
f : D \to \mathbb{R}
$$
As an operation assigning a value to all $x \in D$, denoted $f(x)$.

Two concepts essential to an analysis of functions are **continuity and **differentiability**. Both are discussed below.

## Continuity
### Defining Continuity
Let $f$ be a function. We say $f$ is **continuous** at a point $x_0 \in D$, if whenever any sequence $\{x_n\} \in D$ converges to $x_0$, so too does the sequence $\{f(x_n)\}$. 
$$
\{x_n\} \to x_0 \Longrightarrow \{f(x_n)\} \to f(x_0)
$$
In other words, if a point $x \in D$ is sufficiently close to $x_0$, then the distance $f(x) - f(x_0)$ should become arbitrarily small.

We can similarly define this in terms of limits,
$$
\lim_{n\to\infty} f(x_n) = f \left( \lim_{n\to\infty} x_n \right) = f(x_0)
$$

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

### Geometric Properties of Continuity
Some important implications of continuity are given below: the **extreme value theorem**, and the **intermediate value theorem**.

Let $f$ be a function. For $f$, we define a set
$$
f(D) \equiv \{ y | y = f(x), x \in D \}
$$
As the **image (output)** of $f$.

Now, we say $f$ has a **maximum** given that it's image has a minimum - that is, there exists a point $x_0 \in D$ such that
$$
\forall x \in D, f(x) \le f(x_0) 
$$
Such a point $x_0$ is called a **maximizer**.

Similarly, we say $f$ has a **minimum** given that it's image has a minimum - that is, there exists a point $x_0 \in D$ such that
$$
\forall x \in D, f(x) \ge f(x_0) 
$$
Such a point $x_0$ is called a **minimizer**.

Continuity guarantees the existence of a maximum and/or minimum along bounded domains of a continuous function. This is known as the **Extreme Value Theorem**.

> [!Abstract] Theorem: Extreme Value Theorem 
> Let $f: [a,b] \to \mathbb{R}$ be continuous, where $[a,b]$ is a closed bounded interval. Then, the maximum and minimum of $f$ exist.
>
> > In this theorem, the two key assumptions we need are compactness of $[a,b]$, and the continuity on $f$.
>
> > [!Note]- Proof
> > 
> > We prove a maximum (proof for minimum follows similarly). Let $D = [a,b]$. First, we prove that our image is bounded above, then we prove that the supremum is a functional value.
> > 
> > #### Upper Bound Proof
> > If there exists an upper bound for the image $f(D)$, then 
> > $$
> > \forall x \in [a,b], f(x) \le M 
> > $$
> > By way of contradiction, assume there is no such $M$. Now let $n$ be any natural number. By assumption,
> > $$
> > \forall x \in [a,b], f(x) \le n 
> > $$
> > Thus, there must exist a point $x \in [a,b]$ such that $f(x) > n$. We call this point $x_n$.
> > 
> > Continuing this argument for many $n$, we define a sequence $\{x_n\}$ with the property that $f(x_n) > n$ for all $n$. 
> > 1. By the Sequential Compactness Theorem, we can choose a subsequence $\{x_{n_k}\}$ converging to a point $x_0 \in [a,b]$.
> > 2. By definition of continuity, the image of the sequence, $\{f(x_{n_k})\}$, converges to $f(x_0)$.
> > 
> > However, because $\{f(x_{n_k})\}$ converges, it must be bounded! This contradicts the property that 
> > $$
> > \forall k \in \mathbb{N}, f(x_{n_k}) > n_k \ge k
> > $$
> > Thus, there must exist an upper bound for the image $f(D)$.
> > 
> > 
> > #### Supremum Value Proof
> > Let $S \equiv f([a,b])$. From above, we know that $S$ is bounded above, and because of this, must have a supremum.
> > 
> > Let $c$ be this supremum. We now show a point $x_0 \in [a,b]$ where $c = f(x_0)$.
> > 
> > Let $n \in \mathbb{N}$. By assumption, 
> > $$
> > c - \frac{1}{n}
> > $$
> > is smaller than $c$ and is therefore not an upper bound for $S$.
> > 
> > By the epsilon definition of bounds, this means that there is a point $x \in [a,b]$ such that $f(x) > c - \frac{1}{n}$! Let this point be $x_n$. So,
> > $$
> > c - \frac{1}{n} < f(x_n) \le c
> > $$
> > Continuing this for many $n$, we obtain a sequence $\{x_n\}$ such that $\{f(x_n)\} \to c$!
> > 1. By the Sequential Compactness Theorem, we can find a subsequence $\{x_{n_k}\}$ converging to a point $x_0 \in [a,b]$.
> > 2. By continuity, if $\{x_{n_k}\} \to x_0$, then $\{f(x_{n_k})\} \to f(x_0)$. 
> > 3. But because $\{f(x_n)\} \to c$, this means that $f(x_0) = c$!
> > 
> > Thus, $x_0$ is a value within the function, and must exist. 

Continuity also guarantees the existence of values within a range of a continuous function.

> [!Abstract] Theorem: Intermediate Value Theorem
> Let $f : [a,b] \to \mathbb{R}$ be a continuous function.
>
> Pick any $c$ in the interval $f(x_1) < c < f(x_2)$, where $x_1$ and $x_2$ are in the interior of $[a,b]$. Then, there exists an $x$ strictly between $x_1$ and $x_2$ such that $f(x) = c$.
>
> > The proof is ommitted, as it is long and technical. It uses the Nested Interval Theorem and Bisection Method.

Finally, continuity is maintained along intervals. We define an **interval** $I$ as the set with bounds $u,v$, such that all real numbers $x$ between the bounds exist within the set.
$$
\begin{align*}
    &[u,v] &u \le x \le v \\
    &[u,v) &u \le x < v \\
    &(u,v) &u < x < v \\
    &(u,v] &u < x \le v \\
\end{align*}
$$

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

### Uniform Continuity
*This topic is essential for defining integrals!*

We say $f : D \to \mathbb{R}$ is **uniformly continuous on $D$** if for any two sequences $\{x_n\}, \{y_n\} \in D$ such that if their difference converges to 0,
$$
\{ x_n - y_n \} \to 0
$$
Then $\{ f(x_n) - f(y_n) \} \to 0$. In other words, for any two sequences that become arbitrarily close, so too should our function along these points $\{f(x_n)\}$ and $\{f(y_n)\}$.
> Our sequences don't even have to converge!

The following theorem may help inform us when to expect that a function is uniformly continuous. It will be given later formally, as we haven't yet defined a derivative; but is listed here for our understanding.

> [!Abstract] Theorem: Uniform Continuity
> If $f : D \to \mathbb{R}$ has a **bounded derivative** on $D$, then $f$ is uniformly continuous.

Uniform continuity is a fairly strong result! While continuity does not necessarily imply uniform continuity; uniform continuity can imply continuity!

> [!Abstract] Theorem: Continuity and Uniform Continuity
> If $f: [a,b] \to \mathbb{R}$ is continuous, where $[a,b]$ is a closed bounded interval, then it is uniformly continuous.
> > This only works because of the compact set on $f$'s domain!
>
> > [!Note]- Proof
> >
> > By way of contradiction, let $\{x_n - y_n\} \to 0$, and suppose $\{f(x_n) - f(y_n) \not\to 0$. 
> > 
> > So, there exists an $\epsilon > 0$ such that for all $N \in \mathbb{N}$, there exists an $n \ge N$ such that
> > $$
> > | f(x_n) - f(y_n) | \ge \epsilon
> > $$
> > For $N = 1$, choose $n_1 \ge 1$ such that
> > $$
> > | f(x_{n_1}) - f(y_{n_1}) | \ge \epsilon
> > $$
> > Now, choose $n_2 > n_1$ such that
> > $$
> > | f(x_{n_2}) - f(y_{n_2}) | \ge \epsilon
> > $$
> > Continuing this, we've constructed a sequence on $n$. Letting $\{x_{n_k}\}$, $\{y_{n_k}\}$ be subsequences using this sequence on $n$.
> > $$
> > | f(x_{n_k}) - f(y_{n_k}) | \ge \epsilon
> > $$
> > But we have $\{ x_{n_k} - y_{n_k} \} \to 0$! 
> >
> > So, by the Sequential Compactness Theorem, we can show that 
> > $$
> > \lim_{k \to \infty} x_{n_k} \to u_0
> > $$
> > And because the difference of $x_n$ and $y_n$ converge, this forces
> > $$
> > \lim_{k \to \infty} y_{n_k} \to u_0
> > $$
> > By continuity, this means that $f(x_{n_k}) \to f(u_0)$ and $f(y_{n_k}) \to f(u_0)$! So,
> > $$
> > |f(x_{n_k}) - f(y_{n_k})| \to 0
> > $$
> > But $\epsilon > 0$, which is a contradiction! Thus, $f$ is uniformly continuous on $[a,b]$.
>
> However, if $f : D \to \mathbb{R}$ is uniformly continuous on $D$, then $f$ is continuous.
> 
> > [!Note]- Proof
> >
> > Fix $x_0 \in D$. Define $\{x_n\}$ as a sequence converging to $x_0$, and let $\{y_n\}$ be a sequence that is only $x_0$. Then $f(x_n) \to f(x_0)$ by definition of uniform continuity.

> [!Example]+ Example: Uniform Continuity 
> Let $f : \mathbb{R} \to \mathbb{R}$, $f(x) = 2x$.
> 
> We show that $f$ is uniformly continuous on $\mathbb{R}$. Let ${x_n}$ and $\{y_n\}$ be sequences such that $\{x_n - y_n\} \to 0$. Then,
> $$
> |f(x_n) - f(y_n)| = | 2x_n - 2y_n | = 2 | x_n - y_n | \to 0
> $$

> [!Example]- Example: Uniform Continuity (2)
> Let $f : \mathbb{R} \to \mathbb{R}$, $f(x) = |x|$.
>
> We show that $f$ is uniformly continuous on $\mathbb{R}$. Let ${x_n}$ and $\{y_n\}$ be sequences such that $\{x_n - y_n\} \to 0$. Then, applying the reverse triangle inequality,
> $$
> |f(x_n) - f(y_n)| = | |x_n| - |y_n| | \le |x_n - y_n| \to 0
> $$

> [!Example]- Example: Uniform Continuity (3)
> Let $f : [0, \infty) \to \mathbb{R}$, $f(x) = \sqrt{x}$.
>
> We should expect this to be uniform continuous, as our derivative is bounded between $[c, \infty)$, and our function is continuous in the compact set $[0,c]$!
>
> Using the definition, we show this as follows. 
> $$
> \begin{align*}
>     | \sqrt{x_n} - \sqrt{y_n} |
>     &\le | \sqrt{x_n} - \sqrt{y_n} |^2 = | \sqrt{x_n} - \sqrt{y_n} | \cdot | \sqrt{x_n} - \sqrt{y_n} | \\
>     &\le | \sqrt{x_n} - \sqrt{y_n} | \cdot | \sqrt{x_n} + \sqrt{y_n} | \\
>     &\le | x_n - y_n | \to 0
> \end{align*}
> $$

> [!Example]+ Example: Uniform Continuity Disproof
> Let $f : \mathbb{R} \to \mathbb{R}$, $f(x) = x^2$.
>
> While we have uniform continuity for any compact subset $[a,b]$, our theorem won't apply for infinity! In fact, the end points are where we fail to satisfy the uniform continuity definition.
> 
> Choose $\{x_n\} = n$, $\{y_n\} = n + 1/n$. Then, while they become arbitrarily close,
> $$
> \left\{ n^2 - (n + 1/n)^2 \right\} = \left\{ -2 - \frac{1}{n^2} \right\} \to -2
> $$

> [!Example]- Example: Uniform Continuity Disproof (2)
> Let $f : (0, \infty) \to \mathbb{R}$, $f(x) = \frac{1}{x}$.
> 
> We should expect this to not be uniformly continuous, as our slope blows up as we tend towards 0! 
>
> Choose $\{x_n\} = \{1/n\}$, $\{y_n\} = \{1/n^2\}$. Then, these two sequences both converge to 0, yet
> $$
> \left\{ 1/\frac{1}{n^2} - 1/\frac{1}{n} \right\} = \{ n^2 - n \} \to \infty
> $$

### Epsilon-Delta Criterion for Continuity
Recall how we defined continuity. We propose below an alternative, yet equivalent, definition that may be useful. 

Let $f : D \to \mathbb{R}$ be a function. Then, we say $f$ satisfies the $\epsilon$-$\delta$ criterion at $x_0 \in D$, if for all $\epsilon > 0$, there exists a $\delta > 0$ such that for $x \in D$,
$$
|x - x_0| < \delta \to |f(x) - f(x_0)| < \epsilon
$$
In other words, this is saying that for any interval in $f$'s range, we can choose an interval in $f$'s domain that contains all of the values of this range!

The following theorem establishes a connection between the $\epsilon$-$\delta$ criterion and continuity.

> [!Abstract] Theorem: Continuity and $\epsilon$-$\delta$
> Let $f : D \to \mathbb{R}$ be a function, and let $x_0 \in D$. Then, the following two assertions are equivalent.
> 1. The function $f : D \to \mathbb{R}$ is continuous at $x_0$.
> 2. The $\epsilon$-$\delta$ criterion at $x_0$ holds.

> [!Example]+ Example: Disproof
> Define $f(x)$ as the function where 
> $$
> f(x) = \begin{cases}
>     0 & x < 0 \\
>     1 & x \ge 0
>     \end{cases}
> $$
> We want to show by the $\epsilon$-$\delta$ proof that the function is not continuous at $x = 0$.
> 
> Choose $\epsilon = \frac{1}{2}$. Then, there is no $\delta$ such that $|x| < \delta \to |f(x) - f(0)|$.

> [!Example]- Example: Proof
> Let $f(x) = x^2$. Prove it is continuous at $x_0 \in \mathbb{R}$ by $\epsilon$-$\delta$.
>
> #### Scratch Work
> Fix any $\epsilon > 0$. We start from our $y$ constraint and work backwards to choose a $\delta$.
> 
> $$
> \begin{align*}
>     |f(x) - f(x_0)| 
>     &= |x^2 - x_0^2| = |x - x_0| \cdot |x + x_0| \\
>     &< \delta |x + x_0|
> \end{align*}
> $$
> 
> If $\delta = 1$, then
> $$
> |x - x_0| < 1 \Longrightarrow |x| - |x_0| < 1 \Longrightarrow |x| < 1 + |x_0|
> $$
> 
> $$
> \begin{align*}
>     |f(x) - f(x_0)| 
>     &< \delta |x + x_0| \\
>     &\le \delta ( |x| + |x_0| ) \\
>     &\le \delta ( 2|x_0| + 1 ) < \epsilon
> \end{align*}
> $$
> 
> Provided that $\delta < \frac{\epsilon}{2 |x_0| + 1}$.
> 
> #### Proof
> Let $\epsilon > 0$. Let $\delta = \min\left(1, \frac{\epsilon}{2 |x_0| + 1} \right)$.
> 
> Then, for all $x \in \mathbb{R}$, if $|x - x_0| < \delta$, we get $|x^2 - x_0^2| < \epsilon$ (show from above inequalities).

> [!Example]- Example: Proof
> Suppose $f(x_0) > 0$ and $f : \mathbb{R} \to \mathbb{R}$ is continuous. Prove $f(x) > 0$ for all $x$ on some interval $(x_0 - \delta, x_0 + \delta)$.
> 
> $$
> \begin{align*}
> |f(x) - f(x_0)| < \epsilon \\
> f(x_0) - \epsilon < f(x) < f(x_0) + \epsilon
> \end{align*}
> $$
> 
> Choose $\epsilon = f(x_0) / 2$.
> 
> $$
> \frac{f(x_0)}{2} < f(x)
> $$
> For all $x \in (x_0 - \delta, x_0 + \delta)$.

Similarly, we can establish a connection between the $\epsilon$-$\delta$ criterion and uniform continuity. 

We say $f$ satisfies the $\epsilon$-$\delta$ criterion on the domain $D$, if for all $\epsilon > 0$, there is a $\delta > 0$ such that for all $u,v \in D$,
$$
| u - v | < \delta \qquad | f(u) - f(v) | < \epsilon
$$

> [!Abstract] Theorem: Uniform Continuity and $\epsilon$-$\delta$.
> Let $f : D \to \mathbb{R}$ be a function, and let $x_0 \in D$. Then, the following two assertions are equivalent.
> 1. The function $f : D \to \mathbb{R}$ is uniformly continuous at $x_0$.
> 2. The $\epsilon$-$\delta$ criterion on the domain $D$ holds.

> [!Example]+ Example: Proof
> Prove $f(x) = \sqrt{x}$ is uniformly continuous on $[0,2]$ using $\epsilon$-$\delta$.
> 
> $$
> \begin{align*}
>     |\sqrt{x} - \sqrt{y}|
>     &= |\sqrt{x} - \sqrt{y}| \frac{|\sqrt{x} + \sqrt{y}|}{|\sqrt{x} + \sqrt{y}|} \\
>     &= \frac{|x - y|}{|\sqrt{x} + \sqrt{y}|}
> \end{align*}
> $$
> But this doesn't work, as we can't control the denominator! So, we approach this differently, and begin with a squared term.
>
> $$
> \begin{align*}
>     |\sqrt{x} - \sqrt{y}|^2
>     &= |\sqrt{x} - \sqrt{y}| \cdot |\sqrt{x} - \sqrt{y}| \\
>     &\le |\sqrt{x} - \sqrt{y}| \cdot |\sqrt{x} + \sqrt{y}| \\
>     &\le |x - y|
> \end{align*}
> $$
> Given this, we take the square root of all terms to find 
> $$
> |\sqrt{x} - \sqrt{y}| < |x - y|^\frac{1}{2} < \delta^\frac{1}{2} < \epsilon
> $$
> So we choose $\delta < \epsilon^2$ to finish our proof.


## Inverses, Continuity, and Monotonicity
### Monotonicity
Recall in the intermediate value theorem section, the theorem on the image of continuous functions.

> [!Abstract] Theorem: Intervals of Images
> Let $f : I \to \mathbb{R}$ be continuous, where $I$ is an interval. Then, $f(I)$ is an interval. 

Note that the converse of this is not true in normal cases, but it is when $f$ is monotone! This is expressed below.

> [!Abstract] Theorem: Continuity of Monotone Functions
> If $f : D \to \mathbb{R}$ is monotone, then if $f(D)$ is an interval, $f$ is continuous!
> > Note that $D$ does not have to be an interval. We skip the proof as it is long and technical. 

### Function Inverses
We say a function $f : D \to \mathbb{R}$ is **injective (one-to-one)** if any $y \in f(D)$ has exactly one $x$ value. Formally, if we have any two $x$-values $x_1, x_2$, then
$$
x_1 \ne x_2 \to f(x_1) \ne f(x_2)
$$
> In other words, the function passes the **horizontal line test** - if we draw any horizontal line, it only crosses the function once.

> [!Abstract] Theorem: Monotonicity and Injections
> If $f$ is strictly monotone, then $f$ is injective.
> 
> > [!Note]- Proof
> >
> > Choose any two $x$-values $x_1, x_2$. If $f$ is strictly monotone, then $f(x_1) < f(x_2)$, or $f(x_1) > f(x_2)$. In either case, $f(x_1) \ne f(x_2)$.

Note that the converse is not true, as we can choose a piecewise function to violate monotonicity. However, this changes if $f$ is continuous!

> [!Abstract] Theorem: Continuity, Injections, and Monotonicity
> Let $f : I \to f(I)$ be continuous. Then, $f$ is injective if and only if $f$ is strictly monotone.
>
> > The continuity and interval clauses are extremely important, and without them, this theorem won't hold.

We say that function $f : D \to f(D)$ is **invertible** provided that $f$ is injective. In the event this is true, we define the inverse function as
$$
f^{-1} : f(D) \to D
$$
Such that $x = f^{-1} (y)$ if and only if $f(x) = y$. 

> [!Abstract] Theorem: Monotonicity of Inverses
> If $f : D \to f(D)$ is strictly monotone, then $f^{-1}$ is also strictly monotone.
>
> > [!Note]- Proof
> > 
> > Without loss of generality, suppose $f$ is strictly increasing. Then, for two domain values $u,v \in D$ such that $u < v$,
> > $$
> > u < v \iff f(u) < f(v)
> > $$
> > 
> > Let $u = f^{-1} (x)$, $v = f^{-1} (y)$. Then,
> > $$
> > f^{-1} (x) < f^{-1} (y) \iff f^{-1} ( f(u) ) < f^{-1} ( f(v) ) \Longrightarrow u < v
> > $$
> > So, $f^{-1}$ is strictly increasing.

> [!Abstract] Theorem: Continuity of Inverses
> Let $f : I \to f(I)$ be strictly monotone. Then, $f^{-1}$ is continuous on $f(I)$.
>
> > [!Note]- Proof
> > 
> > Since $f$ is a strictly monotone, so is $f^{-1}$. Because  $f^{-1}$ maps to an interval, and is strictly monotone, it is continuous by an earlier theorem.


## Limits
In this section, we discuss limits and what they mean.

A point $x_0 \in \mathbb{R}$ is a **limit point** of $D \subseteq \mathbb{R}$, provided there exists some sequence $\{x_n\}$ in $D / \{x_0\}$ such that
$$
\{x_n\} \to x_0
$$

> [!Example]+ Example: Limit Points of $\mathbb{R}$
> What are limit points of $D = \mathbb{R}$?
> 
> All of the points in $\mathbb{R}$, as for any $x_0$, we can define the sequence
> $$
> \{x_n\} = x_0 + \frac{1}{n}
> $$
> Which wil converge to $x_0$.

> [!Example]- Example: Limit Points of Intervals
> Let $D = (0,1)$. What are the limit points?
>
> All of the points in the interval $[0,1]$, as we can define a sequence that converges to the endpoints, or any value inside of the interval.

Let $f : D \to \mathbb{R}$ be a function, and let $x_0 \in \mathbb{R}$ be a limit point of $D$. Then, the **limit** of $f$ is
$$
\lim_{x \to x_0} f(x) = L
$$
If for any sequence $\{x_n\}$ in $D/\{x_0\}$, if $\{x_n\} \to x_0$, then $f(x_n) \to L$.
> Limits can only be defined if there exists a sequence in our domain that converges to the point (by definition of a limit point).

Formally, for all $\epsilon > 0$, there exists a $\delta > 0$ such that for all $x \in D$,
$$
0 < | x - x_0 | < \delta \to | f(x) - L | < \epsilon
$$

Note that all of our limit rules apply, and can be used.

