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

> [!Example]- Example: Continuity Proof (2)
> Let $f : \mathbb{R} \to \mathbb{R}$ such that
> $$
> f(x) = 
> \begin{cases}
>     2x & x \le 5 \\
>     0 & x > 5
> \end{cases} 
> $$
> Show that $f(x)$ is continuous at $x = 3$.
> 
> We want to show that for any $\{x_n\} \to x_0$, $\{f(x_n)\} \to f(x_0)$.
> 
> Let $\{x_n\} \to 3$. By definition, $\forall \epsilon > 0$, $\exists N \in \mathbb{N}$ such that $\forall n \ge N$,
> $$
> | x_n - 3 | < \epsilon
> $$
> 
> Let $\epsilon = 1$, and choose the $N$ associated with this epsilon such that $\forall n \ge N$,
> $$
> | x_n - 3 | < 1
> $$
> 
> Now take the expression $|f(x_n) - f(3)|$. Because $\forall n \ge N$, $2 < x_n < 4$, we always apply the $2x$ part of the function. 
> $$
> \begin{align*}
>     |f(x_n) - f(3)| 
>     &= |2x_n - 6| \\
>     &= 2 |x_n - 3|
> \end{align*}
> $$
> Because $\{x_n\} \to 3$, and $|f(x_n) - f(3)| \le 2 |x_n - 3|$, by the squeeze theorem, $\{f(x_n)\} \to f(3)$.

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

> [!Example]- Example: Continuity and Sequential Compactness
> Let $f : D \to \mathbb{R}$ be continuous where $D$ is sequentially compact. Prove that $f(D)$ is sequentially compact.
>
> To show that $f(D)$, is sequentially compact, we want to show that for any $\{y_n\} \in f(D)$, there exists a subsequence $\{y_{n_k}\} \to y_0$ such that $y_0 \in f(D)$.
>
> As all terms of $\{y_n\}$ are in $f(D)$, for all $y_n$, there exists an $x_n$ such that $f(x_n) = y_n$. By sequential compactness on $D$, there exists a subsequence $\{x_{n_k}\} \to x_0$ such that $x_0 \in D$.
>
> By continuity on $f$, as $\{x_{n_k}\} \to x_0$, $\{f(x_{n_k})\} \to f(x_0)$. Letting this $f(x_0) = y_0$, we have a subsequence $\{x_{n_k}\} = y_{n_k}$ converging to a $y_0 \in f(D)$.

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

# Derivatives
## Definition
Consider a function $f : I \to \mathbb{R}$ defined along some interval. Say we want the "slope" of the function at some limit point $x_0 \in I$.

This is the **derivative** of the function, $f'(x_0)$, defined as
$$
f'(x_0) = \lim_{x \to x_0} \frac{f(x) - f(x_0)}{x - x_0} = \lim_{h \to 0} \frac{f(x + h) - f(x_0)}{h}
$$
Where $\{x\} \in I / \{x_0\}$ is any sequence converging to $x_0$.
> Note you can obtain the decond definition from the first by setting $x = x_0 + h$

If the derivative for $f$ exists at a point $x_0$, we say $f$ is **differentiable** at this point.

> [!Abstract] Theorem: Differentiability and Continuity
> If $f'(x_0)$ exists, then $f$ is continuous at $x_0$. In other words, differentiability implies continuity.
>
> > [!Note]- Proof
> >
> > Let $x_n \to x_0$, where $x_n \in I / \{x_n\}$. We want to show that $f(x_n) \to f(x_0)$.
> > 
> > $$
> > \begin{align*}
> >     f(x_n) - f(x_0) = \frac{f(x_n) - f(x_0)}{x_n - x_0} (x_n - x_0) \to f'(x_0) \cdot 0 = 0
> > \end{align*}
> > $$

Derivatives have a variety of useful properties that we can prove! They are given below.

> [!Abstract] Theorem: Product Rule
> If $f : I \to \mathbb{R}$ and $g : I \to \mathbb{R}$ are both differentiable at $x_0$, so is $f \cdot g$.
> $$
> \frac{d}{dx} f(x) g(x) = f'(x) g(x) + f(x) g'(x)
> $$
>
> > [!Note]- Proof
> >
> > Let $x_n \to x_0$ with $x_n \in I / \{x_0\}$. Then, 
> > $$
> > \begin{align*}
> >     \lim_{x_n \to x_0} \frac{f(x_n) g(x_n) - f(x_0) g(x_0)}{x_n - x_0}  
> >     &=  \lim_{x_n \to x_0} \frac{f(x_n) g(x_n) - f(x_0) g(x_0) + f(x_n) g(x_0) - f(x_n) g(x_0)}{x_n - x_0} \\
> >     &= \lim_{x_n \to x_0} \frac{f(x_n) (g(x_n) - g(x_0)) + g(x_0) (f(x_n) - f(x_0))}{x_n - x_0} \\
> >     &= \lim_{x_n \to x_0} f(x_n) \frac{g(x_n) - g(x_0)}{x_n - x_0} + g(x_0) \frac{f(x_n) - f(x_0)}{x_n - x_0} \\
> >     &= f(x_0) g'(x_0) + g(x_0) f'(x_0)
> > \end{align*}
> > $$

> [!Abstract] Theorem: Chain Rule
> If $f : I \to \mathbb{R}$ and $g : I \to \mathbb{R}$ are both differentiable at $x_0$, so is $f(g(x))$.
> $$
> \frac{d}{dx} f(g(x)) = f'(g(x)) g'(x)
> $$


> [!Abstract] Theorem: Derivatives of Inverses
> Let $x_0 \in I$ and $f : I \to \mathbb{R}$ be a strictly monotone continuous function. Suppose $f'(x_0) \ne 0$ exists (to avoid division by 0). Then, we can find the derivative of $f$'s inverse as follows: 
> $$
> (f^{-1})'(x_0) = \frac{1}{f'(y_0)} = \frac{1}{f' (f^{-1}(x_0))}
> $$

> [!Example]- Example: Derivatives of Inverses
> Let $f(x) = x^2$, where $f : [0, \infty) \to \mathbb{R}$. Find $(f^{-1})' (4)$.
>
> We have $f'(x) = 2x$, and $f^{-1} (4) = 2$. Then,
> $$
> (f^{-1})' (4) = \frac{1}{2(2)} = \frac{1}{4}
> $$

## Mean-Value Theorem
### Definition and Proof
Let $f$ be a function continuous on $[a,b]$, and differentiable on $(a,b)$. Then $\exists c \in (a,b)$ such that
$$
f'(c) = \frac{f(b) - f(a)}{b - a}
$$
In other words, there exists a point where the derivative is equal to the average slope!

> [!Example]+ Example: Mean-Value Theorem Applications
> $\forall x$, let $|f'(x)| \le M$. Then, by mean value theorem,
> $$
> | f(x) - f(y) | = | f'(c) (x - y) | \le M |x - y|
> $$
> This proves an earlier theorem in uniform continuity!

We will prove this theorem; but first, we define a variety of lemmas that will be useful to us.

> [!Abstract] Lemma
> Let $I$ be an open interval containing $x_0$, and $f : I \to \mathbb{R}$. Suppose $f'(x_0)$ exists,
>
> If $f(x_0)$ is a max (or min), then $f'(x_0) = 0$.
>
> > [!Note]- Proof
> >
> > Without loss of generality, assume $f(x_0)$ is a max. We show that the limit of slopes on the left and right bound $f'(x_0)$, forcing $f'(x_0) = 0$.
> >
> > Define the interval $I = (x_0 - 1/n, x_0 + 1/n)$ sufficiently close to our maximum. We have
> > $$
> > \frac{f \left( x_0 + \frac{1}{n} \right) - f(x_0)}{\left(x + \frac{1}{n} \right) - x_0} \le 0
> > $$
> > Take this from $n \to \infty$ to get $f'(x_0) \le 0$.
> >
> > Similarly, we define the sequence $x_n = x_0 - 1/n$ to show that $f'(x_0) \ge 0$, which forces $f'(x_0)$ as $0 \le f'(x_0) \le 0$.

> [!Abstract] Theorem: Rolle's Lemma
> Let $f$ be continuous on $[a,b]$, differentiable on $(a,b)$, and $f(a) = f(b)$. Then, $\exists c \in (a,b)$ such that $f'(c) = 0$.
>
> > This is a special case of MVT, but we will use it to prove MVT!
>
> > [!Note]- Proof
> > 
> > By the extreme value theorem, we know that the maximum and minimum of $f$ exist. We do a case analysis:
> > 1. Suppose the max and min both occur at the endpoints. Then, the function is constant - we can choose any point in the interior whose derivative is 0.
> > 2. Suppose a max (or min) appears in $(a,b)$. Then, we apply our previous lemma to guarantee that $\exists c \in (a,b)$ such that $f'(c) = 0$.

We now prove MVT. The idea of this proof is to create a function from $f$ whose endpoints are the same, and applying Rolle's theorem.

> [!Note]+ Proof (Mean Value Theorem)
> 
> Let $f$ be a function continuous on $[a,b]$, and differentiable on $(a,b)$. Let $h(x) = f(x) - mx$ for some $m \in \mathbb{R}$. We can choose an $m$ such that $h(a) = h(b)$ in order to apply Rolle's theorem.
> $$
> f(a) + ma = f(b) + mb \Longrightarrow m = \frac{f(b) - f(a)}{b - a}
> $$
> By Rolle's lemma, $\exists c \in (a,b)$ such that $h'(c) = 0$! Plugging this in and solving for $f'(c)$, this gives us
> $$
> f'(c) = \frac{f(b) - f(a)}{b - a}
> $$

> [!Example]+ Example: Mean Value Theorem
> Prove that $5x + \sin(x) = 0$ does not have more than one solution.
>
> Note that $f'(x) = 5 + \cos(x) \le 4 > 0$. If there were two or more solutions, by Rolle's lemme, $f'(x) = 0$ at some point, which is a contradiction.

> [!Info] Corollary 1
> If $f : I \to \mathbb{R}$ is differentiable, then $f'(x) = 0$ for all $x$ is true if and only if $f$ is constant.
>
> > [!Note]-  Proof
> > 
> > #### Proof ($\leftarrow$)
> > We can use limit definition to easily show that the derivative is 0.
> >
> > #### Proof ($\rightarrow$)
> > By contrapositive, suppose that $f$ is not constant. Then there exists two separate points $a,b \in I$ such that $f(a) \ne f(b)$.
> > 
> > By MVT, there exists a derivative such that 
> > $$
> > f'(c) = \frac{f(b) - f(a)}{b - a} \ne 0
> > $$
> > 
> > We apply the contrapositive to obtain our corollary.

> [!Info] Corollary 2
> Let $I$ be an open interval, and $f,g$ differentiable on $I$. Then, for some constant $C$, $f'(x) = g'(x)$ if and only if $f(x) = g(x) + C$. 
> 
> > This will be really important in integration!

> [!Info] Corollary 3
> Let $f : I \to \mathbb{R}$ be differentiable on $I$. For all $x \in I$, if $f'(x) > 0$ at $x \in I$, then $f$ is strictly increasing on $I$.

### Cauchy MVT
Below, we discuss a generalization of the Mean Value Theorem onto parametric curves. 

> [!Abstract] Theorem: Cauchy Mean-Value Theorem
> Suppose $f$ and $g$ are continuous and differentiable on $(a,b)$, creating a parametric curve $(f(t), g(t))$. If $g'(t) \ne 0$, then $\forall t \in (a,b)$, $\exists t_0 \in (a,b)$ such that
> $$
> \frac{f'(t_0)}{g'(t_0)} = \frac{f(b) - f(a)}{g(b) - g(a)}
> $$

Note that this is a generalization, as we can set $g(t) = t$ for any suitable $f$ to prove the Mean Value Theorem on $f$.

> [!Note]- Proof (Sketch)
> Let $h(t) = f(t) - m g(t)$.
> 
> Choose $m$ such that $h(a) = h(b)$ in order to apply Rolle's theorem to $h(t)$. We then follow a similar process to the MVT theorem proof.

This theorem is quite important! It sets the stage for the Taylor series Lagrange remainder theorem.

> [!Abstract] Theorem: Remainder Theorem
> Let $I$ be an open interval, let $n \in \mathbb{N}$, and suppose we have a differentiable function $f : I \to \mathbb{R}$ which is $n$-times differentiable.
> 
> Suppose that at $x_0$
> $$
> f(x_0) = f'(x_0) = f''(x_0) = \dots = f^{n-1} (x_0) = 0
> $$ 
> Then $\forall x \in I / \{x_0\}$, there exists a $z$ between $x_0$ and $x$ such that 
> $$
> f(x) = \frac{f^n (z)}{n!} (x - x_0)^n
> $$
>
> > [!Note]- Proof
> > 
> > Let $g(x) = (x - x_0)^n$. We have
> > $$
> > \begin{align*}
> >     &g(x_0) = 0 \\
> >     &g'(x_0) = n (x - x_0)^{n-1} \vert_{x=x_0} = 0 \\
> >     &g''(x_0) = n (n - 1) (x - x_0)^{n-2} \vert_{x=x_0} = 0 \\
> >     &\vdots \\
> >     &g^{n-1} (x_0) = n! (x - x_0) \vert_{x=x_0} = 0 \\
> >     &g^n (x_0) = n! \\
> > \end{align*}
> > $$
> > 
> > Then, because $f(x_0) = g(x_0) = 0$, we take (continuously applying to the $n^{th}$ derivative)
> > $$
> > \begin{align*}
> >     \frac{f(x)}{g(x)} 
> >     &= \frac{f(x) - f(x_0)}{g(x) - g(x_0)} = \frac{f'(x_1)}{g'(x_1)} &x_1 \text{ between } x_0, x \\
> >     & \frac{f'(x_1) - f'(x_0)}{g'(x_1) - g'(x_0)} = \frac{f''f(x_2)}{g''(x_2)} \\
> >     &\vdots \\
> >     &\frac{f^n (z)}{n!}
> > \end{align*}
> > $$
> > 
> > So, we find 
> > $$
> > f(x) = g(x) \frac{f^n (z)}{n!} = \frac{f^n (z)}{n!} (x - x_0)^n
> > $$

> [!Example]+ Example: Remainder Theorem
> Let $f : \mathbb{R} \to \mathbb{R}$ and $f(2) = f'(2) = 0$, and $|f''(x)| \le 3$ for all $x$. Give a bound on $f(5)$.
>
> By the remainder theorem,
> $$
> \begin{align*}
> f(5) = \frac{f^2 (z)}{2!} (5 - 2)^2  \\
> |f(5)| \le \frac{3}{2} \cdot 9 \le \frac{27}{2}
> \end{align*}
> $$

# Limsup / Liminf
Consider a sequence that oscillates between $-1$ and $1$ as $n \to \infty$. While its limit does not exist, it does still have a "notion" of two different limits! This is the idea behind limsup (**limit superior**) and liminf (**limit inferior**) - they let us make claims about the limit for sequences, which may not necessarily converge to a single value!

Let $\{x_n\}$ be bounded. Then,
1. We say the **limit superior (limsup)**, is
   $$
   \limsup_{n\to\infty} x_n = \lim_{n\to\infty} \sup_{k \ge n} x_k
   $$
   Equivalent to the limit of the upper bound of $x_n$, for all $n$.
2. We say the **limit inferior (liminf)** is
   $$
   \liminf_{n\to\infty} x_n = \lim_{n\to\infty} \inf_{k \ge n} x_k
   $$
   Equivalent to the limit of the lower bound of $x_n$, for all $n$.
> Note that this can be extended to unbounded sequences too! We just won't cover them.

Note that by this definition, $\bar{x}_n = \sup_{k \ge n} x_k$ is a decreasing sequence! And furthermore, because this sequence is bounded and decreasing, by the MCT, it converges to the infimum.
> This similarly holds for the liminf.

So we can alternatively write the liminf and limsup as
$$
\begin{align*}
    \limsup_{n\to\infty} x_n = \inf_{n\ge 1} (\sup_{k \ge n} x_k) \\
    \liminf_{n\to\infty} x_n = \sup_{n\ge 1} (\inf_{k \ge n} x_k )
\end{align*}
$$

> [!Example]+ Example: Computing Limsup
> Suppose we have the sequence
> $$
> x_n = \frac{(-1)^n}{n}
> $$
> 
> We find the limsup as
> $$
> \bar{x}_n = \sup_{k \ge n} x_k = 
> \begin{cases}
>     (-1)^{n+1} / n+1 & \text{n odd} \\
>     (-1)^n / n & \text{n even}
> \end{cases}
> $$
> Taking the limit as $n \to \infty$, this converges to 0. So, our limsup is 0.
> > We can similarly show that the liminf is 0. 

> [!Example]- Example: Computing Limsup (2)
> Limsups are not always easy to prove! Consider
> $$
> \lim_{n\to\infty} \sin(n) = 1
> $$
> While it seems arbitrarily, this is difficult to prove! We need to prove that $\sin(n)$ for $n \in \mathbb{N}$ is dense in $[-1,1]$.

> [!Abstract] Theorem: Addition of Limsup / Liminf
> $$
> \begin{align*}
>     \limsup_{n\to\infty} (x_n + y_n) \le \limsup_{n\to\infty} x_n + \limsup_{n\to\infty} y_n \\
>     \liminf_{n\to\infty} (x_n + y_n) \ge \liminf_{n\to\infty} x_n + \liminf_{n\to\infty} y_n \\
> \end{align*}
> $$
>
> > [!Note]- Proof (Limsup)
> > 
> > By the upper bound nature of supremums,
> > $$
> > x_n + y_n \le \sup_{k \ge n} x_k + \sup_{k \ge n} y_k
> > $$
> > And furthermore, as the supremum of $x_n + y_n$ is the least upper bound,
> > $$
> > \sup_{k \ge n} (x_k + y_k) \le \sup_{k \ge n} x_k + \sup_{k \ge n} y_k
> > $$
> > We apply the limit on both sides to obtain our theorem.

The **limit set** of $\{x_n\}_{n=1}^\infty$ is
$$
\{ x \in \mathbb{R} | \exists x_{n_j} \to x \}
$$
As $j \to \infty$. In other words, its the set of all limits that $\{x_n\}$'s subsequences converge to.

> [!Example]+ Example: Limit Sets
> $$
> x_n =
> \begin{cases}
>     \frac{5}{n+1} & \text{n odd} \\
>     \frac{(-1)^n + n^2}{n^2} & \text{n even}
> \end{cases}
> $$ 
> 
> Then, our limit set is $S = \{ 0, 1 \}$. 

Interestingly enough, in the above example, our liminf is 0, and our limsup is 1! This is no coincidence - we can use limit sets to compute our liminf and limsup!

> [!Abstract] Theorem: Limit Sets and Liminf / Limsup
> Let $\{x_n\}$ be a bounded sequence, and let $S$ be the limit set.
>
> Then, 
> $$
> \begin{align*}
>     \limsup_{n\to\infty} x_n = \sup(S) \\
>     \liminf_{n\to\infty} x_n = \inf(S)
> \end{align*}
> $$
> > We omit the proof.

> [!Abstract] Theorem: Convergence and Limsup / Liminf
> $$
> \limsup x_n = \liminf x_n \iff \lim x_n = L \text{ exists}
> $$
> In which case, all 3 limits are equal to $L$.
>
> > [!Note]- Proof (Forward Direction)
> > 
> > #### Proof ($\rightarrow$)
> > Assume $\liminf x_n = \limsup x_n = L$. Then, for any $n$,
> > $$
> > \inf_{k \ge n} x_k \le x_n \le \sup_{k \ge n} x_k
> > $$
> > 
> > Taking the limit of both sides as $n \to \infty$, we get
> > $$
> > L \le \lim_{n\to\infty} x_n \le L
> > $$
> > Forcing our limit to be equal to $L$.


# Integration
## Darboux Integrals
Suppose we have a function $f: [a,b] \to \mathbb{R}$. In this section, we formally define what an **integral** is.
$$
\int_a^b f(x) dx
$$

> [!Info] Definition of an Integral
> Recall that in earlier calculus classes, we define an integral as the sum of progressionally smaller rectangles under the curve, known as a **Riemann Sum**.
> $$
> \int_a^b f(x) dx = \lim_{n\to\infty} \sum_{i=1}^n f(x_i) \Delta x_i
> $$

Consider the closed interval $[a,b]$, and partition it using $n + 1$ points $x_0, x_1, x_2, \dots x_{n} \in [a,b]$, where 
$$
x_0 = a \qquad x_i < x_{i+1}, \forall i \qquad x_n = b
$$

Let $f$ be bounded, and consider the interval between any two partition points $[x_{i-1}, x_i]$. By assumption, we can define the quantities $m_i$, the infimum of $f$ along this interval, and $M_i$, the supremum of $f$ along this interval.
$$
m_i = \inf_{x \in [x_{i-1}, x_i]} f(x) \qquad \qquad M_i = \sup_{x \in [x_{i-1}, x_i]} f(x)
$$
And use this to define the **lower ($L$) and upper ($U$) Darboux sums** of $f$,
$$
L(f,P) = \sum_{i=1}^n m_i \Delta x_i \qquad \qquad U(f,P) = \sum_{i=1}^n M_i \Delta x_i
$$
Where $\Delta x_i = x_i - x_{i-1}$.

> Note that as $\Delta x_i$ is the width of our interval, we are defining rectangles under $f$ (whose heights are either the infimum of supremum along the interval)! This is very similar to Riemann Sums.

> [!Abstract] Theorem: Darboux Sums
> Suppose $m \le f(x) \le M$ for all $x \in [a,b]$. Then,
> $$
> m(b - a) \le L(f,P) \le U(f,P) \le M(b-a)
> $$
>
> > [!Note]- Proof
> >
> > $P = \{x_0, \dots x_n\}$ be a partition of $[a,b]$, where $x_i$ is a subinterval, and let $m_i$, $M_i$ be the infimum and supremums along this subinterval. Then,
> > $$
> > \begin{align*}
> >     m \Delta x_i \le f(x) \Delta x_i \le M \Delta x_i \\
> >     \Delta x_i \le m_i \Delta x_i \le M_i \Delta x_i \le  M \Delta x_i
> > \end{align*}
> > $$
> > 
> > Summing this over all of the subintervals, we get
> > $$
> > m (b - a) \le L(f,P) \le U(f,P) \le M (b - a)
> > $$

Now let $P$ be a partition of $[a,b]$. Then, we say $P^*$ is a **refinement** of $P$ if $P^*$ contains all points of $P$, and possibly others.
> A refinement is essentially just a partition with more points inside it.

> [!Example]+ Example: Refinement
> $$
> \left\{ 0, \frac{1}{3}, \frac{1}{2}, 1 \right\} 
> $$
>
> The below is an example of a refinement of this partition
> $$
> \left\{ 0, \frac{1}{3}, \frac{1}{2}, \frac{3}{4}, 1 \right\}
> $$

Refinements are important, as they let us define finer and finer sums for $L$ and $U$!

> [!Abstract] Theorem: Refinements and Darboux Sums
> Let $P$ be a partition of $[a,b]$, and $P^*$ refine $P$. Then,
> $$
> \begin{align*}
>     L(f,P) \le L(f,P^*) \\
>     U(f,P) \ge U(f,P^*)
> \end{align*}
> $$
>
> > This should intuitively make sense! If we more finely divide up $[a,b]$, then the minimum of $f$ along our new subintervals can only increase, and the maximum of $f$ along these subintervals can only decrease!

> [!Abstract] Theorem: Partitions and Darboux Sums
> For any partitions $P_1$ and $P_2$ of $[a,b]$, lower sums are always less than upper sums.
> $$
> L(f, P_1) \le U(f, P_2)
> $$
>
> > [!Note]- Proof
> > 
> > Define the common refinement of $P_1$ and $P_2$, by combining them as $P^* = P_1 \cup P_2$. Then, we can apply our previous theorem to obtain
> > $$
> > L(f, P_1) \le L(f, P^*) \le U(f, P^*) \le U(f, P_2)
> > $$

We can use these theorems to define what an integral is!

Let $P$ be an arbitrary partition of $[a,b]$. Then, we define the **lower / upper (Darboux) integral** as
$$
\underline{\int_a^b} f = \sup_P \{ L(f,P) \} \qquad \overline{\int_a^b} f = \inf_P \{ U(f,P) \}
$$
Or in other words, the maximum lower sum, and the minimum upper sum over all possible partitions $P$.
> Note that the $P$ underneath the supremums and infimums is notation! We're essentially applying a "supremum / infimum" over all possible $L$ and $U$, where $P$ is arbitrary (like the $dx$ in an integral).

If these two integrals are equal, then we say $f$ is **integrable** (in terms of Darboux) and we write
$$
\int_a^b  f = \underline{\int_a^b} f = \overline{\int_a^b} f
$$
for the commmon value.

> [!Abstract] Theorem: Darboux Sums and Integrals
> Let $f: [a,b] \to \mathbb{R}$ be a function. Then,
>
> $$
> L(f,P) \le \underline{\int_a^b} f \le \overline{\int_a^b} f \le  U(f,P)
> $$
>
> > [!Note]- Proof
> > 
> > The first and last inequalities naturally hold by definition of infimums and supremums.
> >
> > We apply our theorem above. For any two arbitrary partitions $P_1, P_2$,
> > $$
> > L(f, P_1) \le U(f, P_2)
> > $$
> > 
> > Because $P_1$ and $P_2$ are arbitrary, we can apply our supremum on $P_1$ to obtain
> > $$
> > \sup_{P_1} L(f, P_1) \le U(f, P_2)
> > $$
> > We know that the supremum exists, as $L(f,P_1)$ is bounded above by $U$. 
> >
> > By the same idea, we apply our infimum on $P_2$ to obtain
> > $$
> > \sup_{P_1} L(f, P_1) \le \inf_{P_2} U(f, P_2)
> > $$
> > Which translates to our integrals by definition!

> [!Example]+ Example: Computing Darboux Integrals
> Consider the constant function over interval $[a,b]$, $f(x) = c$.
>
> We find our integral.
> $$
> \begin{align*}
>     &L(f,P) = \sum_{i=1}^n m_i \Delta x_i = \sum_{i=1}^n c \Delta x_i = c (b - a) \\
>     &U(f,P) = \sum_{i=1}^n M_i \Delta x_i = \sum_{i=1}^n c \Delta x_i = c (b - a) \\
>     &\sup_P L(f,P) = c(b - a) = \inf_P U(f,P) \\
>     &\int_a^b f = c (b - a)
> \end{align*}
> $$

> [!Example]- Example: Computing Darboux Integrals
> Consider the Dirichlet function
> $$
> f(x) = 
> \begin{cases}
>     0 & x \in \mathbb{Q} \\
>     1 & x \not\in \mathbb{Q}
> \end{cases}
> $$
> 
> Is $f$ integrable along $[0,1]$?
> 
> Because the rationals / irrationals are dense, any subinterval will always contain a rational and an irrational, so $f$ will always be both 0 and 1 at some point in the interval.
> $$
> \begin{align*}
>    &L(f,P) = \sum_{i=1} m_i \Delta x_i = \sum_{i=1} 0 \Delta x_i = 0 \\
>    &\sup_P L(f,P) = 0 \\
>    &U(f,P) = \sum_{i=1} M_i \Delta x_i = \sum_{i=1} 1 \Delta x_i = (1 - 0) \\
>    &\inf_P U(f,P) = 1 \\
>    &\sup_P L(f,P) \ne \inf_P U(f,P) 
> \end{align*}
> $$
> 
> As these are not equal, our function is not integrable along $[0,1]$ in the sense of the Riemann Darboux.

## Archimedes-Riemann Theorem
Computing these integrals can be annoying, especially as we need to compute infimums and supremums! The below theorem can help simplify our integral computations in specific cases.

> [!Abstract] Theorem: Archimedes-Riemann Theorem
> Let $f: [a,b] \to \mathbb{R}$ be bounded. Then, $f$ is integrable if and only if there exists a sequence of partitions $\{P_n\}$ such that
> $$
> \lim_{n \to \infty} ( U(f,P_n) - L(f,P_n) ) = 0
> $$
> In this case, we say that $\{P_n\}$ is **archimedian**.
> 
> Furthermore, in the case that it is integrable,
> $$
> \int_a^b f = \lim_{n\to\infty} U(f,P_n) = \lim_{n\to\infty} L(f,P_n)
> $$
>
> > [!Note]- Proof
> > 
> > #### Proof ($\leftarrow$)
> > Suppose there exists a sequence of partitions $\{P_n\}$ such that 
> > $$
> > \{ U(f,P_n) - L(f, P_n) \} \to 0
> > $$
> > 
> > We know that
> > $$
> > \begin{align*}
> >     \overline{\int_a^b} f \le U(f,P_n) \\
> >     \underline{\int_a^b} f \ge L(f, P_n)
> > \end{align*}
> > $$
> > 
> > So we use these to obtain
> > $$
> > 0 \le \overline{\int_a^b} - \underline{\int_a^b} f \le U(f,P_n) - L(f, P_n) \to 0
> > $$
> > So by squeeze theorem, 
> > $$
> > \overline{\int_a^b} f = \underline{\int_a^b} f
> > $$
> >
> > #### Proof ($\rightarrow$)
> > Suppose
> > $$
> > \overline{\int_a^b} f = \underline{\int_a^b} f = \int_a^b f
> > $$
> > 
> > By definition,
> > $$
> > \overline{\int_a^b} f = \inf_P U(f,P) \qquad \underline{\int_a^b} f = \sup_P L(f,P)
> > $$
> > 
> > So by the epsilon-definition of supremums, we know that $\forall \epsilon > 0$, there exists a $L(f,P)$, $U(f,P)$ such that
> > $$
> > L(f,P) < \inf_P U(f,P) + \epsilon \qquad \sup_P L(f,P) - \epsilon < U(f,P)
> > $$
> > We choose $\epsilon = 1/n$, and for all $n \in \mathbb{N}$ choose these $L$'s and $U$'s to find a sequence. Note that these sequences converge by squeeze theorem.
> > $$
> > \begin{align*}
> > \inf_P U(f,P) < L(f,P_n) < \inf_P U(f,P) + \frac{1}{n} \\
> > \sup_P L(f,P) - \frac{1}{n} < U(f,P'_n) < \sup_P L(f,P)
> > \end{align*}
> > $$ 
> > 
> > Our partitions are not guaranteed to be the same, so we can take the union of them, $P'_n \cup P_n = Q_n$
> > $$
> > \begin{align*}
> > \inf_P U(f,P) < L(f,Q_n) \le L(f,P_n) < \inf_P U(f,P) + \frac{1}{n} \\
> > \sup_P L(f,P) - \frac{1}{n} < U(f,P'_n) \le U(f, Q_n) < \sup_P L(f,P)
> > \end{align*}
> > $$ 
> > Finally,
> > $$
> > \begin{align*}
> >     0 
> >     &\le U(f, Q_n) - L(f,Q_n) \\
> >     &< \int_a^b f + \frac{1}{n} + \frac{1}{n} - \int_a^b f \\
> >     &= \frac{2}{n} \to 0
> > \end{align*}
> > $$
> > 
> > We apply squeeze theorem to obtain convergence.
> > 
> > 
> > We now show that
> > $$
> > \int_a^b f = \lim_{n\to\infty} U(f,P_n)
> > $$
> > To do this, we use the property of infimums that
> > $$
> > \begin{align*}
> >     \overline{\int_a^b} f \le U(f, P_n) \\
> >     0 \le U(f,P_n) - \overline{\int_a^b} f \le U(f,P_n) - L(f,P_n)
> > \end{align*}
> > $$
> > 
> > As $n \to 0$, we apply squeeze theorem.
> > $$
> > U(f,P_n) - \overline{\int_a^b} = 0 \Longrightarrow \overline{\int_a^b} = U(f,P_n)
> > $$
> > > We have similar argument for the limit of the lower sum!

This theorem is really important, and can be used to prove a lot! In fact, many of the below properties of integrals can be proven using the Archimedes-Riemann Theorem. See below.


## Properties of Integrals
Below, we discuss various useful properties of integrals.

### Monotonicity and Integrals
> [!Abstract] Theorem: Monotonicity and Integrability
> Any monotone function $f : [a,b] \to \mathbb{R}$ is integrable.
> > The monotonicity on $f$ and its restricted domain automatically implies boundedness!
>
> > [!Note]- Proof 
> > 
> > Let $P_n = \{ x_0, x_1, \dots x_n \}$ where $\Delta x_i = x_i - x_{i-1} = (b-a) / n$ is constant.
> > 
> > We show that $\{P_n\}$ is Archimedian, to apply the previous theorem.
> > $$
> > \begin{align*}
> >     0 &\le U(f,P_n) \Delta x - L(f, P_n) \\
> >       &= \sum_{i=1}^n M_i \Delta x - \sum_{i=1}^n m_i \Delta x \\
> >       &= \frac{b-a}{n} \left( \sum_{i=1}^n f(x_i) - \sum_{i=1}^n f(x_{i-1}) \right) \\
> >       &= \frac{b-a}{n} (f(x_n) - f(x_0)) \\
> >       &= \frac{b-a}{n} (f(b) - f(a)) \to 0 
> > \end{align*}
> > $$
> > 
> > Thus, we apply our above theorem to obtain integrability.

We can use a similar idea to show that any step function is integrable, though this is much more difficult.

> [!Abstract] Lemma
> Let $\{P_n\}$ be Archimedian for $f: [a,b] \to \mathbb{R}$. Then any refinement $\{P_n^*\}$ is also Archimedian.
>
> > [!Note]- Proof
> > 
> > By property of refinements, $U$ will get smaller, and $L$ will get larger, so
> > $$
> > \begin{align*}
> >     0 &\le U(f, P_n^*) - L(f, P_n^*) \\
> >     &\le U(f,P_n) - L(f,P_n) \to 0
> > \end{align*}
> > $$

> [!Abstract] Theorem: Monotonicity
> Let $f(x) \le g(x)$ for all $x \in [a,b]$. Then,
> $$
> \int_a^b f \le \int_a^b g
> $$
> 
> > [!Note]- Proof
> >
> > Let $\{P_n\}$ be Archimedian for $f$, and $\{P_n'\}$ for $g$. Let $Q_n = P_n \cup P_n'$, which is still Archimedian for $f$ and $g$!
> >
> > With a common refinement, we have $U(f, Q_n) \le U(g, Q_n)$. Then, as $n \to \infty$, by the Archimedian Riemann theorem, we are done.

### Additivity, Linearity, Absolute Value of Integrals
> [!Abstract] Theorem: Additivity of Integrals
> Let $f : [a,b] \to \mathbb{R}$ be an integrable function. Then, $\forall c \in (a,b)$,
> $$
> \int_a^b f = \int_a^c f + \int_c^b f
> $$
> 
> > [!Note]- Proof
> > 
> > Suppose there exists an Archimedian Sequence $\{P_n\}$ for $f$ on $[a,b]$. Without loss of generality, suppose $\{P_n\}$ contains $c$ (since any refinement is also Archimedian).
> > 
> > Split $\{P_n\}$ into mutually exclusive partitions $P_n'$ and $P_n''$ based on $c$. We want to show that both subsequences are Archimedian.
> > 
> > We have
> > $$
> > \begin{align*}
> >     &U(f,P_n) - L(f,P_n) \to 0 \\
> >     &(U(f,P_n') + U(f,P_n'')) - (L(f,P_n') + L(f,P_n'')) \to 0 \\
> >     &(U(f,P_n') - L(f,P_n')) + (U(f,P_n'') - L(f,P_n'')) \to 0
> > \end{align*}
> > $$
> > 
> > Because $U(f,P_n') - L(f,P_n')$ and $U(f,P_n'') - L(f,P_n'')$ are both non-negative for all $n$, for this sequence to converge it must be true that they both converge to 0.

> [!Abstract] Theorem: Linearity of Integrals
> Let $\alpha, \beta \in \mathbb{R}$, and $f,g : [a,b] \to \mathbb{R}$ be integrable. Then,
> $$
> \int_a^b (\alpha f + \beta g) = \alpha \int_a^b f + \beta \int_a^b g
> $$
> 
> > [!Note]- Proof (Half)
> > 
> > We show the first part of the proof.
> > $$
> > \int_a^b f + g = \int_a^b f + \int_a^b g
> > $$
> > 
> > Let $P_n$ be an Archimedian sequence for $f$ and $g$ on $[a,b]$, which is possible by common refinement.
> >    
> > We know that
> > $$
> > \begin{align*}
> >     f(x) + g(x) \le \sup f(x) + \sup g(x) \\
> >     \sup( f(x) + g(x) ) \le \sup f(x) + \sup g(x) \\
> >     U(f + g, P_n) \le U(f,P_n) + U(g,P_n)
> > \end{align*}
> > $$
> >    
> > Similarly, we can obtain
> > $$
> > L(f + g, P_n) \ge L(f,P_n) + L(g,P_n)
> > $$
> >    
> > Giving us
> > $$
> > \begin{align*}
> >     &L(f,P_n) + L(g,P_n) \le L(f + g, P_n) \le U(f + g, P_n) \le U(f,P_n) + U(g,P_n) \\
> >     &\int_a^b f + \int_a^b f \le \int_a^b f + g \int_a^b f + g \le \int_a^b f + \int_a^b g &n \to \infty \\
> >     &\int_a^b f + \int_a^b g = \int_a^b f + g
> > \end{align*}
> > $$

> [!Abstract] Theorem: Absolute Value and Integrals
> Let $f$ and $|f|$ be integrable on $[a,b]$. Then, 
> $$
> \left| \int_a^b f \right| \le \int_a^b |f|
> $$
> 
> > [!Note]- Proof
> > 
> > We know that
> > $$
> > -|f(x)| \le f(x) \le |f(x)|
> > $$
> > By monotonicity,
> > $$
> > -\int_a^b |f| \le \int_a^b f \le \int_a^b |f|
> > $$
> > But this is essentially an absolute value!
> > $$
> > \left| \int_a^b f \right| \le \int_a^b |f|
> > $$


### Continuity and Integrals
The follow theorems guarantee integrability for continuous functions.

> [!Abstract] Theorem: Continuity and Integrability
> Let $f$ be a continuous function on compact interval $[a,b]$. Then, its integral along this interval exists.
>
> > [!Note]- Proof
> >
> > Since we have a continuous function on a compact interval, we know $f$ is uniformly continuous. By definition, $\forall \epsilon > 0, \exists \delta > 0$ such that $\forall x,y \in [a,b]$,
> > $$
> > |x - y| < \delta \to |f(x) - f(y)| < \epsilon
> > $$
> >
> > For later convenience, take the constant $\frac{\epsilon}{b-a}$.
> >
> > Let $\{P_n\} = \{x_0, \dots, x_n\}$ be a uniform sequence of partitions for $[a,b]$, where $x_0 = a, x_n = b$. As the partition is uniform, we have that $\Delta x_i = \frac{b-a}{n}$. We wish to show that $\{P_n\}$ is Archimedian.
> > 
> > We know that by a theorem,
> > $$
> > \begin{align*}
> >     0 
> >     &\le U(f,P_n) - L(f,P_n) \\
> >     &\le \sum_{i=1}^n \left( \sup_{x \in [x_{i-1}, x_i]} f \right) \Delta x_i - \sum_{i=1}^n \left( \inf_{x \in [x_{i-1}, x_i]} f \right) \Delta x_i 
> > \end{align*}
> > $$
> > 
> > By the Extreme Value theorem, we know that for some $u_i, v_i \in [x_{i-1}, x_i]$,
> > $$
> > \sup_{x \in [x_{i-1}, x_i]} f = f(u_i) \qquad \inf_{x \in [x_{i-1}, x_i]} f = f(v_i)
> > $$
> > 
> > This gives us
> > $$
> > \begin{align*}
> >     0 &\le \sum_{i=1}^n \left( \sup_{x \in [x_{i-1}, x_i]} f \right) \Delta x_i - \sum_{i=1}^n \left( \inf_{x \in [x_{i-1}, x_i]} f \right) \Delta x_i  \\
> >     &\le \sum_{i=1}^n ( f(u_i) - f(v_i) ) \Delta x_i \\
> >     &\le \max_{1 \le i \le n} ( f(u_i) - f(v_i) ) \sum_{i=1}^n \Delta x_i \\
> >     &\le f(u_{i_0}) - f(v_{i_0}) (b - a)
> > \end{align*}
> > $$
> > 
> > Where $u_{i_0}, v_{i_0}$ is the greatest difference between the maximum and minimum.
> > 
> > If $|u_{i_0} - v_{i_0}| < \delta$, we can apply uniform continuity, we have
> > $$
> > f(u_{i_0}) - f(v_{i_0}) (b - a) < \frac{\epsilon}{b-a} (b - a) < \epsilon
> > $$
> > 
> > And since this holds for all $\epsilon$, we can let $\epsilon \to 0$ and apply squeeze theorem, to have
> > $$
> > \{ U(f,P_n) - L(f,P_n) \} \to 0
> > $$
> > 
> > To guarantee the $|u_{i_0} - v_{i_0}| < \delta$ condition, we choose $N$ large enough such that $\Delta x_i < \delta$, so that $\Delta x_i < \delta$ for all $n \ge N$.

> [!Abstract] Theorem: Continuity and Integrability
> Let $f$ be continuous on open $(a,b)$ and bounded on $[a,b]$. Then, $\int_a^b f$ exists and does NOT depend on $f(a)$ or $f(b)$.
> 
> > [!Note]- Proof (Sketch)
> > 
> > Create an interval $I_n = [a + \frac{1}{n}, b - \frac{1}{n}]$. For each $I_n$, choose a partition $\{P_n^*\}$ satisfying
> > 
> > $$
> > 0 \le U(f, P_n^*) - L(f,P_n^*) \le \frac{1}{n}
> > $$
> > Whose existence is guaranteed by our previous proof.
> > 
> > Let $P_n = P_n^* \cup \{a,b\}$. We show that $\{P_n\}$ is Archimedian for $[a,b]$ to show that $\int_a^b f$ exists, and then show that
> > $$
> > U(f,P_n^*) \to \int_a^b f
> > $$
> > 
> > Since $P_n^*$ doesn't depend on $a$ or $b$, it must be true that the integral also doesn't depend on $f(a)$ or $f(b)$!

> [!Example]+ Example: Continuity and Integrability
> $$
> f = \begin{cases}
>       \sin(1/x) & x \in (0,1) \\
>       0 & x = 0
>     \end{cases}
> $$
> 
> As $f$ is continuous on $(0,1)$, and bounded on $[0,1]$, its integral $\int_0^1 f$ exists.

## Fundmental Theorems of Calculus
> [!Abstract] Theorem: First Fundamental Theorem of Calculus
> Let $F$ be a continuous function on $[a,b]$, and $F'$ be bounded and continuous on $[a,b]$.
>
> Then,
> $$
> \int_a^b F'(x) dx = F(b) - F(a) 
> $$
>
> > [!Note]- Proof
> >
> > Since $F'$ is continuous and bounded, our integral $\int_a^b F'$ exists by a theorem.
> > 
> > Let $P = \{x_0, \dots, x_n\}$ be a partition. Because $F$ is continuous, we apply Mean Value Theorem on each subinterval $[x_{i-1}, x_i]$, we know that $\exists c_i$ such that
> > $$
> > F(x_i) - F(x_{i-1}) = F'(c_i) \Delta x_i
> > $$
> > 
> > Since $F'$ is bounded, we know that 
> > $$
> > \begin{align*}
> > \inf_{[x_{i-1}, x_i]} F'(x) \le &F'(c_i) \le \sup_{[x_{i-1}, x_i]} F'(x) \\
> > m_i \le &F'(c_i) \le M_i
> > \end{align*}
> > $$
> > 
> > So $m_i \Delta x_i \le F(x_i) - F(x_{i-1}) \le M_i \Delta x_i$. We take the sum over all the subintervals to get
> > $$
> > L(F',P) \le F(b) - F(a) \le U(F',P) \\
> > $$
> > 
> > As this holds for all lower sums, we have
> > $$
> > \begin{align*}
> >     \sup_P L(F',P) \le F(b) - F(a) \le \inf_P U(F',P) \\
> >     \underline{\int_a^b} F' \le F(b) - F(a) \le \overline{\int_a^b} F'
> > \end{align*}
> > $$
> > 
> > And as we assume integrability, this gives us
> > $$
> > \int_a^b F' \le F(b) - F(a) \le \int_a^b F' \Longrightarrow \int_a^b F' = F(b) - F(a)
> > $$

We need the below theorems to prove the second fundamental theorem.

> [!Abstract] Lemma
> If $a > b$, then
> $$
> \int_a^b f = - \int_b^a f
> $$

> [!Abstract] Theorem: Integral Mean Value Theorem
> If $f$ is a continuous function on $[a,b]$, then $\exists c \in [a,b]$ such that
> $$
> \int_a^b f = f(c) (b - a)
> $$
> 
> > [!Note]- Proof
> > 
> > By EVT, $f(x_\text{min}) \le f(x) \le f(x_\text{max})$. We integrate this to obtain
> > $$
> > \begin{align*}
> > f(x_\text{min}) (b - a) \le \int_a^b f \le f(x_\text{max}) (b - a) \\
> > f(x_\text{min}) \le \frac{1}{(b-a)} \int_a^b f \le f(x_\text{max})
> > \end{align*}
> > $$
> > 
> > Now, for all points between the minimum and maximum, we can find a $c$ by intermediate value theorem equal to $f$ at that point - finishing our proof.


> [!Abstract] Theorem: Second Fundamental Theorem of Calculus
> If $f$ is a continuous function on $[a,b]$, then for any $x \in (a,b)$, 
> $$
> \frac{d}{dx} \int_a^x f(t) dt = f(x)
> $$
>
> > [!Note]- Proof
> > 
> > Let $\{x_n\} \to x_0$, $\{x_n\} \in [a,b] / \{x_0\}$. By definition of derivative,
> > $$
> > \begin{align*}
> > \frac{\int_a^{x_n} f - \int_a^{x_0} f}{x_n - x_0} 
> > &= \frac{\int_{x_0}^{x_n} f}{x_n - x_0} \\
> > &= \frac{1}{x_n - x_0} f(C_n) \int_{x_0}^{x_n} 1 dx \\
> > &= f(C_n)
> > \end{align*}
> > $$
> > 
> > By the Integral Mean Value Theorem where $C_n$ is between $x_0$ and $x_n$. We evaluate this and take the limit to obtain $f(x_0)$.

## Extra Integral Properties
> [!Abstract] Theorem: Generalized Integral MVT
> Let $g$ be integrable and $g(x) > 0$, and let $f : [a,b] \to \mathbb{R}$ be continuous. Then, $\exists x_0 \in (a,b)$ such that
> $$
> \int_a^b fg = f(x_0) \int_a^b g
> $$
> 
> > Note that if $g = 1$, we have the Integral MVT!
> 
> > [!Note]- Proof
> > 
> > By assumption, we know that $f : [a,b] \to \mathbb{R}$. Thus, by the Extreme Value Theorem, $f$ has a minimum and maximum at $x_\text{min}, x_\text{max}$ (respectively). 
> > 
> > By property of minimums and maximums, we know that $\forall x \in [a,b]$,
> > $$
> > \begin{align*}
> > f(x_\text{min}) \le &f(x) \le f(x_\text{max}) &\text{Mins and Maxes} \\
> > f(x_\text{min}) g(x) \le &f(x) g(x) \le f(x_\text{max}) g(x) &g(x) \ge 0 \\
> > \int_a^b f(x_\text{min}) g(x) \le \int_a^b &f(x) g(x) \le \int_a^b f(x_\text{max}) g(x) &\text{Monotonicity} \\
> > f(x_\text{min}) \int_a^b g(x) \le \int_a^b &f(x) g(x) \le f(x_\text{max}) \int_a^b g(x) &\text{Constants} \\
> > f(x_\text{min}) \le &\frac{\int_a^b f(x) g(x)}{\int_a^b g(x)} \le f(x_\text{max})
> > \end{align*}
> > $$
> > 
> > Since this value is bounded by the minimum and maximum of $f$,by the Intermediate Value Theorem, we know that there exists a $x_0 \in (a,b)$ such that
> > $$
> > f(x_0) = \frac{\int_a^b f(x) g(x)}{\int_a^b g(x)} \\
> > \Longrightarrow \int_a^b f(x) g(x) = f(x_0) \int_a^b g(x)
> > $$


> [!Abstract] Theorem: Continuity of Integration
> Define $F(x) = \int_a^x f(t) dt$ where $f$ is integrable. Then $F(x)$ is a continuous function, and in fact is uniformly continuous!
> 
> > [!Note]- Proof (Sketch)
> > 
> > Let $F(x) = \int_a^x f(t) dt$. Without loss of generality, say $x > y$. We have
> > $$
> > \begin{align*}
> > |F(x) - F(y)| 
> > &= \left| \int_a^x f - \int_a^y \right| = \left| \int_y^x f \right| \\
> > &\le \int_y^x |f| &\text{Property of Absolute Values} \\
> > &\le \max_{a \le x \le b} |f| \cdot (x - y)
> > \end{align*}
> > $$
> >
> > Choose $\delta = \frac{1}{\max_{a \le x \le b} |f| \cdot (x - y)}$ to obtain uniform continuity.

> [!Abstract] Theorem: Fundamental Theorem of Calculus + Chain Rule
> $$
> \frac{d}{dx} \int_{a(x)}^{b(x)} f(t) dt = f(b(x)) \frac{db}{dx} - f(a(x)) \frac{da}{dx} 
> $$
>
> > We can easily prove this by splitting our integral along a middle $c$ value, and applying the second fundamental theorem.


