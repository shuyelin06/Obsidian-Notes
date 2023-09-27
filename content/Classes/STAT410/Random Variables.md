---
title: Random Variables
tags:
- stat410
- work-in-progress
---

We define a **random variable** $X: S \to \mathbb{R}$ as a real-valued function, which maps from a sample space $S$ to real numbers $\mathbb{R}$).

In these notes, we discuss random variables, how to use them, and commonly known distributions.

# Discrete Random Variables
## Introduction to Discrete Random Variables
Let $X$ be a random variable.

If $X$ takes on a finite or countable number of values, we say $X$ is a **discrete random variable**.

> [!Example]+ Example: Discrete Random Variables
> For example, suppose we have 100 red, 100 blue, and 100 white socks, and we choose 3 at once. Now suppose we define $X$ as the total number of red socks we can obtain, and note that $X$ can only be 0, 1, 2, or 3.

For a discrete random variable $X$, the **probability mass function / distribution function (pdf)** of $X$ is a function $p: \mathbb{R} \to \mathbb{R}$ such that $p(x)$ is the probability that $X$ takes on a value $x$. So, for any possible value of $x_i$,
$$
\begin{align*}
        &p(x_i) \ge 0 &i = 1, 2, \dots \\
        &p(x) = 0 &\text{all other values}
\end{align*}
$$
It naturally follows from this that
$$
        \sum_{i=1}^\infty p(x_i) = 1 
$$
In other words, the probabilities sum to 1.
> Sometimes, resources will ask us to "verify" a function is a probability mass function. This simply means to check that all $p(x_i)$ sum to 1.

> [!Example]+ Example: Probability Mass Function (1)
> Say we toss a coin twice. Let $X$ be the number of tails we get. Then,
> $$
> \begin{align*}
>       p(0) = P(\{HH\}) = \frac{1}{4} \\
>       p(1) = P(\{HT, TH\}) = \frac{1}{2} \\
>       p(2) = P(\{TT\}) = \frac{1}{4}
> \end{align*}
> $$

Note that by this definition, the pdf of $X$ lists the probability of $X$'s **outputs**, not necessarily the elements in the sample space $X$ chooses from. See the below example.

> [!Example]- Example: Probability Mass Function (2)
> Let $S = [5] = \{1,2,3,4,5\}$, and assume one value is chosen with an equal chance. Now let $X = X(i) = (i - 2)^2 - 1$, where $i$ denotes some element from the sample space. Then, we find the following outputs: 
> $$
> \begin{align*}
>       i = 1,3 &\to x = 0 \\
>       i = 2 &\to x = -1 \\
>       i = 4 &\to x = 3 \\
>       i = 5 &\to x = 8
> \end{align*}
> $$
>
> Using these, we find $p(x)$ as a function such that
> $$
> \begin{align*}
>       p(0) = 2 / 5 \\
>       p(-1) = 1 / 5 \\
>       p(3) = 1 / 5 \\
>       p(8) = 1 / 5
> \end{align*}
> $$
> Where all other $p(x_i) = 0$. 

A **cummulative distribution function (cdf)** of a random variable $X$, denoted $F_X (x) = p(X \le x)$. In other words, the value of $F_X$ is the cumulative probability of all values $p(x_i)$ such that $x_i \le x$.

> [!Abstract] Theorem: Cummulative Distribution Functions
> A function $F_X(x)$ is a cummulative distribution function if and only if
> 1. $0 \le F_X(x) \le 1$ for all $x$ that $X$ takes on.
> 2. $\lim_{x \to \infty} F_X(x) = 1$
> 3. $\lim_{x \to -\infty} F_X(x) = 0$
> 4. $F_X(x)$ is non-decreasing
> 5. $F_X(x)$ is right-continuous for all $x \in \mathbb{R}$. In other words,
>    $$
>       \lim_{x \to x_0^+} F_X(x) = F_X(x_0)
>    $$

For discrete random variables, cummulative distribution functions appear as progressively increasing step functions.

> [!Example]+ Example: Cummulative Distribution Functions
> Take our probability mass function from the previous example. Given this pmf, we find that:
> 1. For $-\infty < x < -1$, $F_X(x) = p(x < - 1) = 0$.
> 2. For $-1 \le x < 0$, $F_X(x) = p(x < 0) = p(x = -1) = 1 / 5$
> 3. For $0 \le x < 3$, $F_X(x) = p(x < 3) = p(x = 0) + p(x = -1) = 3 / 5$
> 4. For $3 \le x < 8$, $F_X(x) = p(x < 8) = p(x = 3) + p(x = 0) + p(x = -1) = 4 / 5$
> 5. For $x \ge 8$, $F_X(x) = 1$.

While we typically create cdfs from pdfs, we can also derive pdfs from cdfs. This is given in the below theorem.

> [!Abstract] Theorem: Deriving PDFs from CDFs
> If a discrete random variable takes on values $x_1, x_2, \dots, x_n$ such that
> $$
> x_1 < x_2 < x_3 < \dots < x_n
> $$
> Then $p(x = x_1) = F_X(x_1)$, and $p(x = x_i) = F_X(x_i) - F_X(x_{i-1})$ for $i = 2, \dots, n$.
>
> Moreover,
> - $p(a < x \le b) = F_X(b) - F_X(a)$
> - $p(a < x < b) = F_X(b) - F_X(a) - p(x = b)$
> - $p(a \le x \le b) = F_X(b) - F_X(a) + p(x = b)$
> - $p(a \le x < b) = F_X(b) - F_X(a) + p(x = a) - p(x = b) $

> [!Example]+ Example: Deriving PDFs from CDFs
> Let the cdf of a discrete random variable be given as
> $$
> F_X(x) = \begin{cases}
>          0 & x < 1 \\
>          3 / 10 & 1 \le x < 2 \\
>          6 / 10 & 2 \le x < 3 \\
>          8 / 10 & 3 \le x < 5 \\
>          1 & x \ge 5
>        \end{cases}
> $$
>
> Given this cdf, determine what $p(2 < x \le 3)$ and $p(3 \le x \le 5)$ are.
>
> We find that
> $$
> p(2 < x \le 3) = F_X(3) - F_X(2) = 2 / 10
> $$
> 
> Additionally, we find that
> $$
> p(3 \le x \le 5) = F_X(5) - F_X(3) + p(x = 3)
> $$
> Note that we have to re-add $x = 3$, as subtracting $F_X(3)$ removes that $3$ from our interval. Additionally, note that $p(x = 3) = F_X(3) - F_X(2)$, as this will get rid of everything right before $x = 3$.

## Expectation and Variance
If $X$ is a discrete random variable with pmf $p(x)$, then the **expected value of $X$** is given as
$$
E(X) = \sum_x x p(x) = \sum_x x p(X = x)
$$
provided that the sum $\sum_x \vert x \vert p(x)$ does NOT diverge.

Similarly, the expected value of a function $g(X)$ is given as
$$
E(g(X)) = \sum_x g(x) p(x) = \sum_x g(x) p(X = x)
$$
provided $\sum_x \vert g(x) \vert p(x)$ does NOT diverge.
> Note that when passing $X$ into a function, the output is **not** passed into $p(x)$.

If $g(x) = x^n$, then $E(g(x)) = E(x^n)$ is the **$n^{th}$ moment of $X$**.

> [!Example]+ Example: Expected Value
> A coin is tossed until you see tails. If you end on toss $i$, you win $(-2)^{i-1}$ dollars. What are your expected winnings?
>
> Let $X$ is a random variable denoting our possible winnings. Then, $X = 1, -2, 4, -8, \dots$.
>
> The probability we end on round $i$ is given as
> $$
> p(x) = (1/2)^i
> $$
> Because we must only get heads before hitting a tail to end on round $i$.
>
> Then the expected value of $X$ is
> $$
> E(X) = 1 \frac{1}{2} - 2 \frac{1}{4} + 4 \frac{1}{8} - 8 \frac{1}{16} + \dots
> $$
> This sum diverges, so we cannot possibly have an expected value. This makes sense, as we cannot possibly expect to get "0" money.

The **variance** of a random variable $X$ is given by
$$
\text{Var}(X) = E\left((X - E(X))^2\right)
$$

Furthermore, we have the following properties of expected value and variance.

> [!Abstract] Theorem: Properties of Expected Value and Variance
> For random variable $X$, we have
> 1. $E(aX + b) = a E(X) + b$ for $a, b \in \mathbb{R}$
> 2. For $g_1(x), g_2(x)$, $E(g_1(x) + g_2(x)) = E(g_1(x)) + E(g_2(x))$. This generalizes to $n$ as well.
> 3. $\text{Var}(X) = E(x^2) - (E(x))^2$
> 4. $\text{Var}(aX + b) = a^2 V(X)$
>
> > [!Note]- Proofs
> >
> > The proof for property (1) is given below.
> > $$
> > \begin{align*}
> >       E(aX + b) &= \sum_x (ax + b) p(x) \\
> >            &= a \sum_x x p(x) + b \sum_x p(x) \\
> >            &= a E(X) + b (1) \\
> >            &= a E(X) + b
> > \end{align*}
> > $$
> >
> > The proof for property (2) is given below.
> > $$
> > \begin{align*}
> >       E(g_1(x) + g_2(x)) &= \sum_x (g_1(x) + g_2(x)) p(x) \\
> >                &= \sum_x g_1(x) p(x) + \sum_x g_2(x) p(x) \\
> >                &= E(g_1(x)) + E(g_2(x))
> > \end{align*}
> > $$
> >
> > The proof for property (3) is given below.
> > $$
> > \begin{align*}
> >       \text{Var}(X) = V(X) &= E( (X - E(X))^2 ) \\
> >                     &= E(X^2 - 2X E(X) + E(X)^2) \\
> >                     &= E(X^2) - E(2X E(X)) + E(E(X)^2) &\text{ By (2)} \\
> >                     &= E(X^2) - 2 E(X) E(X) + E(X)^2 &\text{ Extract Constants} \\
> >                     &= E(X^2) - E(X)^2
> > \end{align*}
> > $$
> > > Note that we can take out the $E(X)$ because the expected value of $X$ is already a predetermined constant, so we can treat it as so.
> > 
> > The proof for property (4) is given below.
> > $$
> > \begin{align*}
> >       V(aX + b) &= E( (aX + b)^2 ) - \left( E(aX + b)^2 \right) \\
> >            &= E(a^2 X^2 + 2 aXb + b^2 ) - a^2 E(X)^2 - 2 aE(X) b - b^2 \\
> >            &= a^2 E(X^2) + 2ab E(X) + b^2 - a^2 E(X)^2 - 2 ab E(X) - b^2 \\
> >            &= a^2 E(X^2) - a^2 E(X)^2 \\
> >            &= a^2 \left( E(X^2) - E(X)^2 \right) = a^2 V(x) 
> > \end{align*}
> > $$

> [!Example]+ Example: Variance
> Consider rolling a 4-sided die once, and let $X$ be the value the die takes on. Find $V(X)$.
>
> We find the expected value of $X$, $E(X)$ as
> $$
> \begin{align*}
>       &E(X) = \frac{1}{4} 1 + \frac{1}{4} 2 + \frac{1}{4} 3 + \frac{1}{4} 4 = \frac{5}{2} \\
>       &E(X^2) = \frac{1}{4} 1^2 + \frac{1}{4} 2^2 + \frac{1}{4} 3^2 + \frac{1}{4} 4^2 = \frac{30}{4}
> \end{align*}
> $$
> 
> Using this, we can calculate the variance
> $$
> V(X) = E(X^2) - E(X)^2 = \frac{30}{4} - \frac{5}{2}^2 = \frac{5}{4}
> $$
>
> Note that if $V(X)$ is large, then so is $X - E(X)$ (by definition). We can intuitively think of this variance as telling us how "far" the values of $X$ are away from the "average" expected value $E(X)$.

## Common Discrete Random Variables
In this section, we discuss some common discrete random variables.

### Uniform Discrete Random Variable
The **Discrete Uniform Distribution**, is the random variable with uniform spacing elements, all with equal chance of occurring.

The pmf of the Uniform Distribution is given as follows:
$$
p(x) =
\begin{cases}
      1/n & \text{for} \; x = 1, 2, \dots, n  \\
      0 & \text{otherwise}
\end{cases}
$$
> The $x = 1, 2, \dots, n$ merely indicates that elements of the random variable must have uniform spacing from one another.

We find the expected value as
$$
E(X) = \frac{n+1}{2}
$$

> [!Note]- Expected Value Derivation: Uniform Distribution
> $$
> \begin{align*}
>       E(X) &= \sum_{i=1}^n i p(i) \\
>            &= \sum_{i=1}^n i \frac{1}{n} = \frac{1}{n} \sum_{i=1}^n i &\text{Constant Probability} \\
>            &= \frac{1}{n} \frac{n(n+1)}{2} = \frac{n+1}{2}
> \end{align*}
> $$

We find the variance as
$$
V(X) = \frac{(n+1)(n-1)}{12}
$$

> [!Note]- Variance Derivative: Uniform Distribution
> $$
> \begin{align*}
>       V(X) &= E(X^2) - E(X)^2 \\
>            &= \sum_{i=1}^n i^2 p(i) + \left( \frac{n+1}{2} \right)^2 &\text{Expected Value Definition} \\
>            &= \frac{1}{n} \frac{n(n+1)(2n+1)}{6} - \left( \frac{n+1}{2} \right)^2 &\text{Sum of Squares} \\
>            &= \frac{n^2 - 1}{12}
> \end{align*}
> $$
   
### Bernoulli Distribution
The **Bernoulli Distribution**, often denoted $X \sim \text{Bernoulli}(p)$, tracks the probability of a success (given as 1), given probability of success $p$.
$$
X =
\begin{cases}
        1 & \text{Success} \\
        0 & \text{Failure}
\end{cases}
$$

The pmf of the Bernoulli Distribution is given as
$$
p(1) = p \qquad p(0) = 1 - p
$$

We find the expected value as
$$
E(X) = p
$$

We find the variance as
$$
V(X) = p - p^2
$$

### Geometric Distribution
The **Geometric Distribution**, often denoted $X\sim\text{geom}(p)$, tracks the probability of the first success after $x$ trials, where $p$ is the probability of success for any trial.

The pmf of the Geometric Distribution is given as follows:
$$
p(x) = (1 - p)^{x-1} p \qquad \text{for} \; x = 1, 2, \dots
$$
> We can intuitively understand this as getting $x-1$ failures, then a single success.

We find the expected value as
$$
E(X) = \frac{1}{p}
$$

> [!Note]- Expected Value Derivation: Geometric Distribution
> $$
> \begin{align*}
>       E(X) &= \sum_{x=1}^\infty x p (1-p)^{x-1} \\
>            &= p \sum_{x=1}^\infty x (1-p)^{x-1}
> \end{align*}
> $$
>
> Let $q = 1 - p$ to obtain
> $$
> p \sum_{x=1}^\infty x q^{x-1}
> $$
>
> Observe how $\frac{d}{dq} q = x q^{x-1}$. We can use this to solve our summation.
> $$
> \begin{align*}
>       E(X) &= p \sum_{x=1} \frac{d}{dq} q^x &\text{Derivative of q} \\
>            &= p \frac{d}{dq} \sum_{x=1} q^x \\
>            &= p \frac{d}{dq} \frac{1}{1-q} &\text{Ratio Sum} \\
>            &= p \frac{1}{(1-q)^2} &\text{Derivation} \\
>            &= \frac{p}{p^2} = \frac{1}{p} &\text{Sub for q}
> \end{align*}
> $$

We find the variance as
$$
V(X) = \frac{1-p}{p^2}
$$

> [!Note]- Variance Derivation: Geometric Distribution
> We need to find
> $$
> V(X) = E(X^2) - E(X)^2
> $$
>
> Because we already know what $E(X)$ is, we need to find $E(X^2)$. Let $q = 1 - p$. 
> $$
> \begin{align*}
>       E(X^2) &= \sum_{x=1}^\infty x^2 q^{x-1} p &\text{Expected Value Definition} \\
>              &= \sum_{x=1}^\infty (x(x-1)+x) q^{x-1} p \\
>              &= \sum_{x=1}^\infty x(x-1) q^{x-1} p + \sum_{x=1}^\infty x q^{x-1} p \\
> \end{align*}
> $$
> We use the same derivation idea as with the expected value derivation, but with a second derivative.
> $$
> \begin{align*}
>       E(X^2) &= \sum_{x=1}^\infty x(x-1) q^{x-1} p + \sum_{x=1}^\infty x q^{x-1} p \\
>              &= pq \sum_{x=1}^\infty x (x-1) q^{x-2} + E(X) \\
>              &= pq \frac{d^2}{dq^2} \sum_{x=1}^\infty q^x + E(X) \\
>              &= pq \frac{d^2}{dq^2} \left( \frac{1}{1-q} \right) + E(X) \\
>              &= pq \frac{2}{(1-q)^3} + \frac{1}{p} \\
>              &= \frac{2 - p}{p^2}
> \end{align*}
> $$

### Binomial Distribution
The **Binomial Distribution**, denoted $X\sim\text{binom}(n,p)$, tracks the probability of $x$ successes given $n$ trials, each with a probability of $p$. Each trial is independent of one another, so the success/failure of one does not influence the success/failure of another.

The pmf of the Binomial Distribution is given as follows:
$$
p(x) = \binom{n}{x} p^x (1-p)^{n-x}
$$
> We can intuitively think of this as choosing $x$ positions out of $n$ trials for success, and leaving the rest as failures.

We find the expected value as
$$
E(X) = np
$$

> [!Note]- Expected Value Derivation: Binomial Distribution
> $$
> \begin{align*}
>       E(X) &= \sum_{x=0}^n x \binom{n}{x} p^x (1-p)^{n-x} \\
>            &= \sum_{x=1}^n x \frac{n!}{x! (n-x)!} p^x (1 - p)^{n-x} \\
>            &= \sum_{x=1} \frac{n!}{(x-1)! (n-x)!} p^x (1-p)^{n-x} \\
>            &= n p \sum_{x=1}^\infty \frac{(n-1)!}{(x-1)! (n-1 - (x-1))!} p^{x-1} (1-p)^{n-1 - (x-1)}
> \end{align*}
> $$
> > Note that we make the summation start from $x=0$ to $x=1$ because the $x=0$ term evaluates to 0.
>
> Let $y = x - 1$. Then, we see our summation becomes
> $$
> \begin{align*}
>       E(X) &= np \sum_{y = 0}^\infty \frac{(n-1)!}{y! (n-1-y)!} p^y (1-p)^{n-1-y} \\
>            &= np \sum_{y=0}^\infty \binom{n-1}{y} p^y (1 - p)^{n-1-y}
> \end{align*}
> $$
> Applying the **binomial theorem**, we find that
> $$
> \sum_{y=0}^\infty \binom{n-1}{y} p^y (1-p)^{n-1-y} = (p + (1-p))^{n-1} = 1
> $$
> Thus, we find our expected value to be
> $$
> E(X) = np (1) = np
> $$

We find the variance as
$$
V(X) = np (1-p)
$$

> [!Note]- Variance Derivation: Binomial Distribution
> To find $V(X)$, we need to find $E(X^2)$. We do that below.
>
> $$
> \begin{align*}
>       E(X) &= \sum_{x=0}^n x^2 \binom{n}{x} p^x (1-p)^{n-x} \\
>            &= \sum_{x=1}^n x^2 \frac{n!}{x! (n-x)!} p^x (1-p)^{n-x} \\
>            &= \sum_{x=1}^n x \frac{n!}{(x-1)! (n-x)!} p^x (1-p)^{n-x} 
> \end{align*}
> $$
>
> Let $x = k + 1$. Then, we find
> $$
> \begin{align*}
>       E(X) &= \sum_{k=0}^{n-1} x \frac{n!}{(x-1)! (n-x)!} p^x (1-p)^{n-x} \\
>            &= \sum_{k=0}^{n-1} (k+1) \frac{n!}{k! (n-1-k)!} p^{k+1} (1-p)^{n-1-k} \\
>            &= np \left[ \sum_{k=0}^{n-1} k \frac{(n-1)!}{k! (n-1-k)!} p^k (1-p)^{n-1-k} + \sum_{k=0}^{n-1} \frac{(n-1)!}{k! (n-1-k)!} p^k (1-p)^{n-1-k} \right] \\
>            &= np \left[ \sum_{k=0}^{n-1} k \binom{n-1}{k} p^k (1-p)^{n-1-k} + \sum_{k=0}^{n-1} \binom{n-1}{k} p^k (1-p)^{n-1-k} \right] \\
> \end{align*}
> $$
> Notice that in this combination, the left term is equivalent to our expected value (for $n-1$), and the right term was found before in our expected value derivation.
>
> $$
> \begin{align*}
> E(X) &= np \left[ \sum_{k=0}^{n-1} k \binom{n-1}{k} p^k (1-p)^{n-1-k} + \sum_{k=0}^{n-1} \binom{n-1}{k} p^k (1-p)^{n-1-k} \right] \\
> &= np \left[ (n-1)p + 1 \right]
> \end{align*}
> $$
>
> We now use $E(X^2)$ to find $V(X)$.
> $$
> V(X) = E(X^2) - E(X)^2 = np \left[ (n-1)p + 1 \right] - (np^2) = np (1-p)
> $$

### Hypergeometric Distribution
The **Hypergeometric Distribution**, denoted $X\sim\text{Hypergeometric}(n,m,k)$, tracks the probability of $x$ successes, given $k$ trials from total sample of $n$ elements with $m$ successes (no replacement).

> [!Example] Example: Hypergeometric Distribution
> 6 trucks of 100 are inspected. We know 4 of the 100 have issues. What is the probablility that 5 trucks pass?
>
> Given this scenario, we have
> $$
> \begin{cases} n = 100 \\ m = 96 \\ k = 6 \end{cases}
> $$
>
> Note that $m = 96$, because we want to know the number of trucks that **pass**, not fail.

The pmf of the Hypergeometric Distribution is given as follows:
$$
p(x) = \frac{\binom{m}{x} \binom{n-m}{k-x}}{\binom{n}{k}}
$$

We now find our expected value and variance. To aid us in this, we use the following lemma:

> [!Abstract] Lemma
> $$
> \sum_{i=0}^k \binom{a}{i} \binom{b}{k-i} = \binom{a+b}{k} 
> $$

We find our expected value as
$$
E(X) = \frac{km}{n}
$$

> [!Note]- Expected Value: Derivation
> $$
> \begin{align*}
>         E(X) &= \sum_{x=0}^k x \frac{\binom{m}{x} \binom{n-m}{k-x}}{\binom{n}{x}} = \sum_{x=0}^k x \binom{m}{x} \frac{\binom{n-m}{k-x}}{\binom{n}{x}} \\
>         &= \sum_{x=1}^k x \frac{m!}{x!(m-x)!} \frac{\binom{n-m}{k-x}}{\binom{n}{k}} \\
>         &= m \sum_{x=1}^k \frac{(m-1)!}{(x-1)!(m-x)!} \frac{\binom{n-m}{k-x}}{\binom{n}{k}} \\
>         &= \frac{m}{\binom{n}{k}} \sum_{x=1}^k \binom{m-1}{x-1} \binom{n-m}{k-x} \\
>         &= \frac{m}{\binom{n}{k}} \binom{n-1}{k-1} = \frac{km}{n}
> \end{align*}
> $$

We find the variance as
$$
V(X) = \frac{km (n-m) (n-k) }{n^2 (n-1) }
$$
The proof is ommitted due to how complex the calculation is.

> [!Info] Hypergeomtric Distribution and Binomial Distribution
> Let $p,q$ be the proportions of the successes and failures, respectively. In other words,
> $$
> p = \frac{m}{n} \qquad q = 1 - p
> $$
>
> Then, the pmf is
> $$
> p(x) = \binom{np}{x} \binom{nq}{k - x} = \binom{k}{x} p \left(p - \frac{1}{n} \right) \left(p - \frac{2}{n} \right) \dots \left(p - \frac{x-1}{n} \right) q \left(q - \frac{1}{n} \right)
> $$
> Note that as $n \to \infty$, (the population gets larger), we find
> $$
> p(x) = \binom{k}{x} p^x q^{k-x}
> $$
> In other words, the binomial distribution! So, for large $n$, even though we're drawing without replacements, we'll get about the same answer as if we treated everything as independent!

### Negative Binomial
The **Negative Binomial Distribution**, denoted $X\sim\text{Negative Binomial}(r,p)$, tracks the probability of obtaining the $r^{th}$ success after $x$ trials, given that every trial has a probability of success $p$.

$$
p(x) = \binom{x-1}{r-1} p^r (1-p)^{x-r} \qquad x=r, r+1, \dots
$$

> [!Example] Negative Binomial Distribution
> If a person is exposed to a disease, 30% show symptoms, What is the probability that the $100^{th}$ person exposed is the $7^{th}$ person to show symptoms?
>
> We have a negative binomial distribution with $r = 7$ and $p = 0.3$. To find our probability, we check for $x = 100$.

To understand why we call this the Negative Binomial Distribution, let's verify the pmf. Note that we can verify our pmf using the concept of "negative binomials".

> [!Note]- Negative Binomial: PMF Verification
> Let $k = x - r$ be the number of failures. We find the probability of $k$ to be
> $$
> p(k) = \binom{(k+r)-1}{r-1} p^r (1-p)^{(k+r)-r}
> $$
>
> We can expand the binomial coefficient as
> $$
> \begin{align*}
>       \binom{k+r-1}{r-1} &= \frac{(k+r-1)!}{(r-1)! (k+r-1 - (r-1))!} \\
>       &= \frac{(k+r-1)(k+r-2)(k+r-3) \dots (r) (r-1)!}{(r-1)! k!} \\
>       &= \frac{(k+r-1)(k+r-2)(k+r-3) \dots (r)}{k!} \\
>       &= \frac{r(r+1)(r+2) \dots (r+k-1)}{k!} \\
>       &= \frac{(-1)(-r)(-1)(-r-1)(-1)(-r-2) \dots (-r-(k-1))}{k!} \\
>       &= \frac{(-1)^k (-r) (-r-1) (-r-2) \dots (-r - (k-1))}{k!} \\ 
>       &= (-1)^k \binom{-r}{k}
> \end{align*}
> $$
> > Note: We can do negative binomial coefficients, in a similar way we do positive ones.
>
> Let $q = 1 - p$. Note that we can expand $p^{-r}$ using the binomial theorem, to obtain the following:
> $$
> \begin{align*}
>       p^{-r} &= (1-q)^{-r} \\
>       &= \sum_{k=0}^\infty \binom{-r}{k} (-q)^k (1)^{-r-k} \\
>       &= \sum_{k=0}^\infty q^k (-1)^k \binom{-r}{k} \\
>       &= \sum_{k=0}^\infty q^k \binom{k+r-1}{r-1}
> \end{align*}
> $$
>
> Now, summing our pmf to verify it, we find
> $$
> \sum_{k=0}^\infty p(k) = p^r \sum_{k=0}^\infty \binom{k+r-1}{r-1} (1-p)^k = p^{-r} p^r  = 1
> $$

We find our expected value and variance as
$$
E(X) = \frac{r}{p} \qquad V(X) = r \frac{1-p}{p^2}
$$

If our pmf is instead expressed as the number of failures $k = x - r$ (as it sometimes is), we have
$$
E(X) = \frac{r}{p} - r \qquad V(X) = r \frac{1-p}{p^2} 
$$

### Poisson Distribution
Consider a period of time, with occurrences of some event over that period of time.

We can break this time interval up into $n$ subintervals, so that for any subinterval, the event occurs at most once. Averaging the occurrences of the event for every subinterval, we can find a probability of the event occurring for any subinterval $p$.

Notice that if our subintervals are independent, we essentially have a binomial distribution!

We can expect that as the number of subintervals increase ($n$ increases), our probability of seeing an accident in a subinterval gets smaller. To account for this, we assume here that the ratio of subintervals to probability, $\lambda$, is constant.
$$
np = \lambda
$$

Now, assuming independent subintervals, we can derive the pmf for the Poisson Distribution using the Binomial Distribution. 

Observe the binomial distribution has pmf
$$
p(x) = \binom{n}{x} p^x (1-p)^{n-x}
$$
Subbing in $p = \lambda / n$, we find
$$
p(x) = \binom{n}{x} \left( \frac{\lambda}{n} \right)^x \left( 1 - \frac{\lambda}{n} \right)^{n-x} = \frac{n(n-1)\dots(n-x+1)}{x!} \left( \frac{\lambda}{n} \right)^x \left( 1 - \frac{\lambda}{n} \right)^{n-x}
$$
Taking the $n^x$ in the denominator, we divide every term in the binomial coefficient to find
$$
= \frac{1 (1 - 1/n) \dots (1 - \frac{x-1}{n}}{x!} \lambda^x \left[ (1 - \frac{\lambda}{n})^{\frac{-n}{\lambda}} \right]^{-\lambda} (1 - \frac{\lambda}{n})^{-x}
$$
Observe now that as $n \to \infty$,
$$
\lim_{n \to \infty} p(x) = \frac{1}{x!} \lambda^x e^{-\lambda} (1)
$$
> Remember that
> $$
> \lim_{x \to \infty} (1 - 1 /x)^{-x} = e
> $$

Thus, the Poisson distribution, denoted $X \sim \text{Poisson}(\lambda)$ has a pmf given as
$$
p(x) = \frac{\lambda^x}{x!} e^{-\lambda} \qquad x = 0, 1, \dots
$$
> We don't really apply this distribution too much, though for sufficiently large values $n$ its a good approximation of the binomial distribution.

We now find the expected value and variance as
$$
E(X) = \sum_x x p(x) = \sum_{x=0}^\infty x \frac{\lambda^x}{x!} e^{-\lambda} = \sum_{x=1}^\infty \frac{\lambda^x}{(x-1)!} e^{-\lambda} = \lambda e^{-\lambda} \sum_{x=1}^\infty \frac{\lambda^{x-1}}{(x-1)!} = \lambda e^{-\lambda} e^\lambda = \lambda
$$
> Note that
> $$
> \sum_{n=0}^\infty x^n / n! = e^x
> $$

We now find $E(X^2)$
$$
E(X^2) = \sum_{x=0}^\infty x^2 \frac{\lambda^x}{x!} e^{-\lambda} = \lambda e^{-\lambda} \sum_{x=1}^\infty x \frac{\lambda^{x-1}}{(x-1)!}
$$
Let $x = i + 1$.
$$
= \lambda e^{-\lambda} \sum_{i=0}^\infty (i+1) \frac{\lambda^i}{(i)!} = \lambda e^{-\lambda} \left[ \sum_{i=1}^\infty \frac{\lambda^i}{(i-1)!} + \sum_{i=0}^\infty \frac{\lambda^i}{(i)!} \right] = \lambda e^{-\lambda} (\lambda e^\lambda + e^\lambda) = \lambda^2 + \lambda
$$
> Note we bring the summation to $i = 1$ bc we don't want to deal with negative factorials.

We find our variance as
$$
V(X) = E(X^2) - E(X)^2 = \lambda^2 + \lambda - \lambda^2 = \lambda
$$


# Continuous Random Variables
## Introduction to Continuous Random Variables
A **continuous random variable** $X: S \to \mathbb{R}$ is a function that takes on uncountably many elements. In other words, we say $X$ is continuous if there is a non-negative function $f(x)$ such that $f(x)$ is defined for all $\mathbb{R}$ and
$$
P(X \in B) = \int_B f(x) dx
$$
where $B$ is a set of values in $\mathbb{R}$.

This gives us smooth probability curves, which can be integrated along to find probabilities along an interval. 

The probability mass function of a contiuous random variable has the following properties:
1. $f(x) \ge 0$ for all $x$
2. $\int_{-\infty}^\infty f(x) = 1$
3. $P(a \le x \le b) = \int_a^b f(x) dx$
4. $P(X = a) = 0$
5. $P(a \le x \le b) = P(a < x < b)$.

Property (4) occurs because as we have uncountably many values, we cannot examine the probability of any singular value. (5) naturally follows from this fact.
> To "verify" the pdf, we check that property (2) holds.

> [!Example]+ Example: PDFs of Contiuous Random Variables
> Let $X$ have pdf given by
> $$
> f(x) = \begin{cases}
>               k e^{-3x} & x > 0 \\
>               0 & x \le 0
>      \end{cases}
> $$
>
> Find $k$.
>
> We find $k$ by choosing a value such that we have a valid pdf.
> $$
> 1 = \int_{-\infty}^\infty f(x) dx = \int_0^\infty ke^{-3x} = k \lim_{t \to \infty} \frac{e^{-3x}}{-3x} \bigg\vert^t_0 = \frac{k}{3} \to k = 3
> $$

If $X$ is a contiuous random variable with pdf $f(x)$, then the **cummulative distribution function (cdf)** is
$$
F_X(x) = P(X \le x) = \int_{-\infty}^x f(t) dt
$$
> We can intuitively understand this as summing (integrating) all values up to some point $x$ - just like our discrete case!

The properties of cummulative distribution functions follow similarly to that of the discrete case.
$$
F(\infty) = 1 \qquad F(-\infty) = 0
$$

Just like in the discrete case, we can find the pdf from the cdf, and vice versa.

> [!Abstract] Theorem: CDF and PDF Conversions
> If $f(x)$, $F(x)$ are the pdf and cdf of a contiuous random variable $X$, then
> $$
> P(a \le X \le b) = F(b) - F(a)
> $$
>
> Moreover, we can find our pdf by taking the derivative of the cdf, assuming $F(x)$ is differentiable.
> $$
> f(x) = \frac{d}{dx} F(x)
> $$

> [!Example]+ Example: CDF and PDF Conversions
> Consider the last example, with pdf given as
> $$
> f(x) = \begin{cases}
>               k e^{-3x} & x > 0 \\
>               0 & x \le 0
>      \end{cases}
> $$
>
> We find the cdf as
> $$
> F(x) = \begin{cases}
>               \int_{0}^t f(t) dt = 1 - e^{-3x} & x > 0 \\
>               0 & x \le 0
>        \end{cases}
> $$

## Expectation and Variance
If $X$ is a continuous random variable with pdf given by $f(x)$, then the expected value is
$$
E(X) = \int_{-\infty}^\infty x f(x) dx
$$
and the variance is given as
$$
V(X) = E( (X - E(X))^2 ) = \int_{-\infty}^\infty \left( x - E(X) \right)^2 f(x) dx 
$$

However, just like in the discrete case, we will often just use the form
$$
V(X) = E(X^2) - (E(X))^2 = \int_{-\infty}^\infty x^2 f(x) dx - \left( \int_{-\infty}^\infty x f(x) dx \right)^2
$$
> All of this is directly analogous to the discrete case.

The properties of expected value and variance are given below. Note that they are virtually the same (and can be proven the same) as the discrete case.
1. $E(aX + b) = a E(X) + b$
2. $V(aX + b) = a^2 V(X)$
3. $E(g(x)) = \int_{-\infty}^\infty g(x) f(x) dx$

> [!Example]+ Example: Expectation and Variance
> If $X$ has pdf given by
> $$
> f(x) = \begin{cases}
>      e^{-x} & x > 0 \\
>      0 & x < 0 \\
>      \end{cases}
> $$
> 
> Then we can find $E(e^{3x/4})$ as
> $$
> E(e^{\frac{3x}{4}}) = \int_{-\infty}^\infty g(x) f(x) dx = \int_0^\infty e^{3x}{4} e^{-x} dx = \int_0^\infty e^{\frac{-x}{4}}
> $$

End of Exam 1 Content
---

## Common Continuous Random Variables
In this section, we discuss some common continuous random variables.

### Uniform Distribution
The **Continuous Uniform Distribution**, denoted $X \sim u(\alpha, \beta)$, is the random variable over interval $(\alpha, \beta)$, with a uniform probability throughout.

The pdf of the Uniform Distribution is given as follows:
$$
f(x) = \begin{cases}
     \frac{1}{\beta - \alpha} & \alpha < x < \beta \\
     0 & \text{Otherwise}
     \end{cases}
$$

Moreover, we have a cdf which can easily be derived as
$$
F(x) = \begin{cases}
                0 & x \le \alpha \\
                \frac{x-\alpha}{\beta - \alpha} & \alpha < x > \beta \\
                0 & x \ge \beta
     \end{cases}
$$
> While this looks scary, the cdf is really just a line.