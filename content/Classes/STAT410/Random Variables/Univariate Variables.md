---
title: Random Variables (Univariate)
tags:
- stat410
---

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
The **Poisson Distribution**, denoted $X\sim\text{Poisson}(\lambda)$, tracks the probability of some event occurring $x$ times, over some period of time, where $\lambda$ is the expected occurrence of the event over this time.
$$
p(x) = \frac{\lambda^x}{x!} e^{-\lambda}
$$
Thus, the Poisson distribution, denoted has a pmf given as
$$
p(x) = \frac{\lambda^x}{x!} e^{-\lambda} \qquad x = 0, 1, \dots
$$
> We don't really apply this distribution too much, though for sufficiently large values $n$ its a good approximation of the binomial distribution.


> [!Note]- PDF Derivation
> Consider a fixed period of time, with occurrences of some event $E$ over that period of time. How can we find the probability of $E$ occurring $x$ times?
>
> To do this, we can break the time interval up $n$ subintervals small enoguh such that for any subinterval, $E$ occurs at most once. We can then average the occurrences of the event for every subinterval to find a probability of $E$ occurring for any subinterval $p$. 
>
> Now, assuming our subintervals are independent, we can find the occurrences of $E$ using a binomial distribution! However, note that as our number of subintervals $n$ increases, our average and thus probability $p$ will decrease, giving us inconsistent results. Thus, we will assume that the ratio of subintervals to probability, $\lambda$, is constant.
> $$
> np = \lambda
> $$
>
> Now, recall that the binomial distribution has pdf given by
> $$
> p(x) = \binom{n}{x} p^x (1 - p)^{n-x}
> $$
>
> We can use this pdf to find the probability of our event $E$ occurring. Letting $p = \lambda / n$, we find
> $$
> \begin{align*}
>       p(x) &= \binom{n}{x} \left( \frac{\lambda}{n} \right)^x \left( 1 - \frac{\lambda}{n} \right)^{n-x} \\
>       &= \frac{n!}{x! (n-x)!} \left( \frac{\lambda}{n} \right)^x \left(1 - \frac{\lambda}{n} \right)^{n-x} \\
>       &= \frac{n(n-1)\dots(n-x+1)}{x!} \left( \frac{1}{n^x} \right) \lambda^x \left( 1 - \frac{\lambda}{n} \right)^{n-x} \\
>       &= \frac{1 (1 - 1/n) \dots (1 - (x-1)/n )}{x!} \lambda^x \left( 1 - \frac{\lambda}{n} \right)^{n} \left( 1 - \frac{\lambda}{n} \right)^{-x}
> \end{align*}
> $$
>
> Now observe that the number of subintervals $n \to \infty$, we find
>
> $$
> \lim_{n \to \infty} p(x) = \frac{1}{x!} \lambda^x e^{-\lambda} (1)
> $$
>
> Giving us our pdf.

We now find the expected value as
$$
E(X) = \lambda
$$

and variance as
$$
V(X) = \lambda
$$

> The proof is omitted, though to do it, note that
> $$
> \sum_{n=0}^\infty x^n / n! = e^x
> $$


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

If $X$ is a continuous random variable with pdf $f(x)$, then the **cummulative distribution function (cdf)** is
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


## Common Continuous Random Variables
In this section, we discuss some common continuous random variables below.

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
                1 & x \ge \beta
     \end{cases}
$$
> While this looks scary, the cdf is really just a line.

Finally, we have expected value and variance given as 
$$
E(X) = \frac{\alpha + \beta}{2} \qquad V(X) = \frac{(\beta - \alpha)^2}{12}
$$

These can easily be derived using the definitions for $E(X)$ and $V(X)$, so we omit the derivations below.


### Normal Distribution
The **Normal Distribution**, denoted $X \sim N(\mu, \sigma)$ is the distribution with pdf given as follows:
$$
f(x, \mu, \sigma) = \frac{1}{\sigma \sqrt{2 \pi}} e^{-\frac{1}{2} \left( \frac{x - \mu}{\sigma} \right)^2}
$$
> The curve created by this pdf is sometimes referred to as the **bell curve**.

> [!Note]- PDF Verification
> Let us verify the pdf of the normal distribution below. In other words, we must show that
>
> $$
> \int_{-\infty}^\infty f(x) dx = 1
> $$
>
> Now, let 
> $$
> k = \int_{-\infty}^\infty f(x) dx \qquad z = \frac{x - \mu}{\sigma} \to dz = \frac{1}{\sigma} dx
> $$
>
> Using these variables, we can convert our integral to a double integral as so:
> $$
> \begin{align*}
>       k &= \int_{-\infty}^\infty f(x) dx = \int_{-\infty}^\infty \frac{1}{\sqrt{2\pi}} e^{-\frac{1}{2} z^2} dz \\
>       k \sqrt{2\pi} &= \int_{-\infty}^\infty e^{-\frac{1}{2} z^2} dz \\
>       k^2 2 \pi &= \int_{-\infty}^\infty e^{-\frac{1}{2} w^2} dw \int_{-\infty}^\infty e^{-\frac{1}{2} z^2} dz = \int_{-\infty}^\infty \int_{-\infty}^\infty e^{-\frac{1}{2} (z^2 + w^2)} dw dz      
> \end{align*}
> $$
> 
> Now, if we let $w = x$ and $z = y$, we find that we have a double integral spanning the entire $xy$-plane. Furthermore, as our $x$ and $y$ terms in the integral are given in the form ($x^2 + y^2$), we will convert to polar coordinates to simplify our integral.
> $$
> w = r \cos(\theta) \qquad z = r \sin(\theta) \quad \to \quad w^2 + z^2 = 1
> $$
>
> Accounting for the Jacobian as well, we perform a change of variables to obtain the integral 
> $$
> \begin{align*}
>       k^2 2 \pi &= \int_0^\infty \int_0^{2\pi} e^{\frac{-r^2}{2}} r d\theta dr \\
>             &= \int_0^\infty 2\pi r e^{\frac{-r^2}{2}} \bigg\vert_0^{2\pi} dr \\
>             &= - 2 \pi \left( \lim_{r\to\infty} e^{\frac{-r^2}{2}} - 1 \right) \\
>             &= 2\pi
> \end{align*}
> $$
> Thus, we find $k^2 2 \pi = 2 \pi \to k = 1$. We have verified our pdf.

The expected value and variance for the normal distribution are given as
$$
E(X) = \mu \qquad V(X) = \sigma^2 
$$
> Note that $\sigma = \sqrt{V(X)}$ is often called the **standard deviation**, whereas $\mu = E(X)$ is often called the **mean**.

---

The normal distribution on $X \sim N(0,1)$ is called the **standard normal distribution**. In this special case, our pdf simplifies down to
$$
f(x) = \frac{1}{\sqrt{2\pi}} e^{-x^2 / 2} 
$$
And we find the expected value and variance as
$$
E(X) = 0 \qquad V(X) = 1
$$
> To find the expected value, we can use the fact that the function we're integrating is odd. 

Given a random variable representing a normal distribution, we can perform a transformation on the random variable to obtain the standard normal distribution. This transformation is known as **standardization**.

> [!Abstract] Theorem: Standardizing Normal Distributions
> If $X \sim N(\mu, \sigma)$, then the transformation
> $$
> z = \frac{X - \mu}{\sigma}
> $$
> will yield the standard normal distribution.
>
> This transformation essentially has the effect of shifting our values by $\mu$, then bringing them closer together / further apart by dividing by $\sigma$. 
>
> Note that the cdf of the standard normal distribution is often denoted $\Phi(x)$.

Standardizing normal distributions is often helpful in the real world, as the standard normal distribution is much easier to use in data analysis! Using the standard normal distribution, we can find the probability of obtaining any value between $x_1$, $x_2$ as
$$
P(x_1 \le X \le x_2) = P\left( \frac{x_1 - \mu}{\sigma} \le z \le \frac{x_2 - \mu}{\sigma} \right)
$$

Which can easily be evaluated using commonly known tables for the standard distribution. 
> These books may represent tables of values for $x$ for both $-\infty \to x$, or $0 \to x$! Be sure you know which type of table you're using.

Some examples of this are given below.

> [!Example]+ Example: Standardizing Normal Distributions (1)
> The height of students obey a normal distribution with $\mu = 67$ inches, $\sigma = 3$ inches. What percent of students have heights between 64 and 70 inches?
>
> To calculate this, we will first standardize this distribution. Let's define $Z$ as
> $$
> Z = \frac{X - \mu}{\sigma}
> $$
>
> Then, we can calculate the probability as
> $$
> \begin{align*} 
> P(64 < X < 70) &= P\left( \frac{64 - 67}{3} < z < \frac{70 - 67}{3}  \right) \\
>      &= P(-1 < z < 1) = \int_{-\infty}^1 p(x) - \int_{-\infty}^{-1} \\
>      &= F(1) - F(-1)
> \end{align*}
> $$
>
> We can then use a table of values (or a calculator) to find our result. Note that if we have a table that only tells us $F(1)$, we can find $F(-1) = 1 - F(1)$ by virtue of the normal distribution's symmetry.

> [!Example]- Example: Standardizing Normal Distributions (2)
> Radiation Exposure in an area takes on a normal distribution with mean $\mu = 4.35$ mrem and standard distribution $\sigma = 0.59$ mrem. What is the probability a person is exposed to more than $5.2$ mrem?
>
> Using our standardization of $z = (X - \mu) / \sigma$, we want
> $$
> \begin{align*}
>       P(X > 5.2) &= 1 - P(X < 5.2) \\
>           &= 1 - P\left( z < \frac{5.2 - 4.35}{0.59} \right) \\
>           &= 1 - F(1.44) = 0.0749 
> \end{align*}
> $$


### Gamma Distribution
The **Gamma Distribution**, denoted $X \sim \Gamma(\alpha, \beta)$ is the distribution whose pdf is given as
$$
f(x, \alpha, \beta) = \frac{\beta^\alpha x^{\alpha - 1} e^{-\beta x}}{\Gamma(\alpha)} \qquad x, \alpha, \beta > 0
$$

where $\Gamma(\alpha)$ is the **gamma function**.
$$
\Gamma(\alpha) = \int_0^\infty t^{\alpha - 1} e^{-t} dt
$$
> This complicated looking expression is essentially just scaling a function $x^t e^{-t}$ so that it becomes a valid pdf.

> [!Abstract] Theorem: Gamma Function
> Given the Gamma function, we have the following properties.
> 1. For $\alpha \ge 2$, $\Gamma(\alpha) = (\alpha - 1) \Gamma(\alpha - 1)$. If $\alpha$ is a positive integer, then $\Gamma(\alpha) = (\alpha - 1)!$
> 2. We have $\Gamma(1/2) = \sqrt{\pi}$.
>
> > [!Note]- Proof (Property 1)
> >
> > We can easily prove (1) by applying integration by parts on $u = e^{-t}, dv = t^{\alpha - 1}$. We can then use this to find
> > 
> > $$
> > \Gamma(\alpha) = (\alpha - 1) \Gamma(\alpha - 1) = (\alpha - 1)(\alpha - 2) \Gamma(\alpha - 2) = (\alpha - 1) \dots 2 \cdot \Gamma(1)
> > $$
> >
> > Furthermore, we see that
> > $$
> > \Gamma(1) = \int_0^\infty e^{-t} dt = 1
> > $$
>
> > [!Note]- Proof (Property 2)
> >
> > $$
> > \begin{align*}
> >     \Gamma(1/2) &= \int_0^\infty t^{1/2 - 1} e^{-t} dt \\
> >                 &= \int_0^\infty t^{-1/2} e^{-t} dt \\
> >                 &= \int_0^\infty u^{-1} e^{u^2} 2u du &\leftarrow t = u^2 \\
> >                 &= \int_0^\infty e^{-u^2} du \\
> >                 &= \sqrt{\pi}
> > \end{align*}
> > $$

Conceptually, the Gamma distribution is fairly similar to the Poisson distribution in the discrete case.

If the Poisson distribution measures the probability of $x$ successes in some time interval $t$, then the Gamma distribution is measuring the probability of "waiting" a certain amount of time $x$ for $\alpha$ successes, where $\beta$ is our average rate of success.

We can find the expected value and variance of the Gamma Distribution as so:
$$
E(X) = \frac{\alpha}{\beta} \qquad V(X) = \frac{\alpha}{\beta}
$$

> [!Note]- Derivation for Expected Value
> $$
> \begin{align*}
>     E(X) &= \frac{1}{\Gamma(\alpha)} \int_0^\infty \beta^\alpha x^\alpha e^{-\beta x} dx \\
>          &= \frac{1}{\Gamma(\alpha)} \int_0^\infty y^\alpha e^{-y} \frac{1}{\beta} dx &y = \beta x \\
>          &= \frac{1}{\beta} \frac{\Gamma(\alpha + 1)}{\Gamma(\alpha)} &\Gamma(\alpha + 1) = \int_0^\infty t^\alpha e^{-t} dt\\
>          &= \frac{\alpha}{\beta} \frac{\Gamma(\alpha)}{\Gamma(\alpha)} &\Gamma(\alpha + 1) = \alpha \Gamma(\alpha) \\
>          &= \frac{\alpha}{\beta}
> \end{align*}
> $$
> The derivation for variance follows similarly.

---

The Gamma distribution has many use cases. Below, we list some of the of most common cases.

The Gamma distribution on $X \sim \Gamma(1, \beta)$ is known as the **exponential distribution**. In this distribution, we're measuring the probability of the first success at some time.
$$
f(x, \beta) = \beta e^{-\beta x}
$$

> [!Example]+ Example: Exponential Distribution
> Suppose the total cars exceeding the speed limit in half an hour is a random variable with a Poisson distribution with $\lambda = 8.4$.
>
> What is the probability the wait time is at most 5 minutes between cars exceeding the speed limit?
>
> Here, we define $t = 1$ as "one unit of 30 min". So, we can expect an average of $\lambda \cdot t = 8.4$ cars exceeding the speed limit in a 30 minute period. We find the probability that our wait time is at most 5 minutes using the Gamma distribution, with $\alpha = 1, \beta = 8.4$.
> $$
> \int_0^{5/30} 8.4^1 e^{-8.4 x} x^0 dx \approx 0.75
> $$


The Gamma distribution on $Y \sim \Gamma(v/2, 1/2)$ is known as the **chi-squared distribution**, where $v$ denotes the degrees of freedom. 
$$
f(x, v) = \frac{1}{2^{v/2} \Gamma(v/2)} x^{\frac{v-2}{2}} e^{-\frac{x}{2}}
$$
This distribution is used a lot in sampling and statistical theory!
> This distribution has expected value $E(Y) = v$, and variance $V(Y) = 2v$.

### Cauchy Distribution
The **Cauchy Distribution**, denoted $X \sim \text{Cauchy} (\theta)$, is the distribution with pdf:

$$
f(x, \theta) = \frac{1}{\pi} \cdot \frac{1}{(x - \theta)^2 + 1} \qquad -\infty < x < \infty
$$

This distribution commonly finds a use case in optics problems!
> The cauchy distribution looks similar to the normal distribution's bell curve, but with slower decreasing sides.

> [!Note] PDF Verification
> Let's verify the pdf of the Cauchy distribution for $\theta = 0$.
>
> $$
> \begin{align*}
> \int_{-\infty}^\infty f(x,0) dx
>               &= \frac{1}{\pi} \int_{-\infty}^\infty \frac{1}{x^2 + 1} dx \\
>               &= \frac{1}{\pi} \left( \lim_{t\to\infty} \tan^{-1}(t) - \lim_{s\to-\infty} \tan^{-1} (s) \right) \\
>               &= \frac{1}{\pi} \left( \frac{\pi}{2} + \frac{\pi}{2} \right) = 1
> \end{align*}
> $$

Surprisingly, we find that the cauchy distribution does not have any expected value or variance.
$$
E(X) = \frac{1}{\pi} \int_{-\infty}^\infty \frac{ \vert x \vert }{1 + x^2} dx = \frac{2}{\pi} \int_0^\infty \frac{x}{1+x^2} dx
     = \frac{1}{\pi} \lim_{t\to\infty} \ln(1 + u) \bigg\vert_0^t = \infty
$$


### Beta Distribution
The **Beta Distribution**, denoted $X \sim \text{Beta} (\alpha, \beta)$, is the distribution with pdf given as
$$
f(x, \alpha, \beta) = \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha) \Gamma(\beta)} x^{\alpha - 1} (1 - x)^{\beta - 1} \qquad 0 < x < 1, \alpha, \beta > 0
$$

> [!Note]- PDF Verification
> We verify the pdf of the beta distribution. Recall the gamma function
> $$
> \Gamma(\alpha) = \int_0^\infty t^{\alpha - 1} e^{-t} dt
> $$
>
> Now, letting $\alpha = a + 1, \beta = b + 1$, we obtain
> $$
> \Gamma(\alpha) \cdot \Gamma(\beta) = \int_0^\infty x^a e^{-x} dx \int_0^\infty y^b e^{-y} dy = \int_0^\infty \int_0^\infty x^a e^{-x} y^b e^{-y} dx dy
> $$
>
> We can manipulate this double integral and show it is equal to $\Gamma(\alpha + \beta)$.
>
> Let's define the change of variables $x = uv$, $y = (1-u)v$. Then,
> $$
> u = \frac{x}{x + y} \qquad v = \frac{y}{1 - u}
> $$
> > Note that as $x \to \infty, u \to 1$.
>
> We use this fact to perform a change of variables on our double integral. 
> $$
> \begin{align*}
>       \int_0^\infty \int_0^\infty x^a e^{-x} y^b e^{-y} dx dy 
>                     &= \int_0^\infty \int_0^\infty (uv)^a e^{-(uv)} ( (1-u) \cdot v)^b e^{-(1 - u) v} dx dy \\
>                     &= \int_0^\infty \int_0^1 u^a (1-u)^b v^{a+b+1} e^{-v} du dv
> \end{align*}
> $$
> > There is no Jacobian in this change of variables, as it evaluates to 1.
> 
> We can pull a $\Gamma(a + b + 2)$ out of this double integral to obtain
> $$
> \Gamma(a + b + 2) \int_0^1 u^a (1 - u)^b du = \Gamma(\alpha + \beta) x^{\alpha - 1} (1-u)^{\beta - 1}
> $$
> Which will divide our beta pdf to give us 1.

We find the expected value and variance of the beta distribution as follows.
$$
E(X) = \frac{\alpha}{\alpha + \beta} \qquad V(X) = \frac{\alpha \beta}{(\alpha + \beta)^2 (\alpha + \beta + 1)}
$$

> [!Note] Beta Distribution: Derivation for Expected Value
> $$
> \begin{align*}
> E(X) &= \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha) \Gamma(\beta)} \int_0^1 x \cdot x^{\alpha - 1} (1 - x)^{\beta - 1} dx \\
>      &= \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha) \Gamma(\beta)} \frac{\Gamma (\alpha + 1) \Gamma(\beta)}{\Gamma(\alpha + 1 + \beta)} \frac{\Gamma(\alpha + 1 + \beta)}{\Gamma(\alpha + 1) \Gamma(\beta)} \int_0^1 x^\alpha (1-x)^{\beta - 1} dx
> \end{align*}
> $$
> Looking at the last two terms, notice that we are really just integrating $\text{Beta}(\alpha + 1, \beta)$. Note that because of this, we eliminate terms by definition of the beta distribution's pdf.
>
> $$
> \begin{align*}
>  \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha) \Gamma(\beta)} \frac{\Gamma (\alpha + 1) \Gamma(\beta)}{\Gamma(\alpha + 1 + \beta)} (1) &= \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha) \Gamma(\beta)} \frac{\alpha \Gamma (\alpha) \Gamma(\beta)}{\Gamma(\alpha + \beta) (\alpha + \beta)} \\
> &= \frac{\alpha}{\alpha + \beta}
> \end{align*}
> $$
>
> The derivation for the variance follows quite similarly.


# Transformations of Random Variables (Univariate)
Suppose we have a random variable $X$, and define random variable $Y$ such that it is given in terms of $X$. 
$$
Y = g(X)
$$

Then, the probability of some value $y$, $P(Y = y)$, is asking for the cumulative probability $y$ over all possibilities $x \in X$ satisfying $g(x) = y$. 

Given some random variable $Y = g(X)$, how do we find it's pmf?

## Discrete Case
In the discrete case, if $g(X)$ is a one-to-one function, we can find the pmf of $Y$ using the inverse function $X = g^{-1} (y)$. Plugging this function into the pmf of $X$ as $x$ will yield us the pmf of $Y$.

Consider the following example.

> [!Example]+ Example: Transforming Discrete Random Variables
> Let $X \sim \text{Binomial} (n,p)$, and find the pmf of $Y = 2X + 3$.
>
> We find the pmf of $Y$ by solving for $X$, and subbing this into our binomial pdf.
> $$
> P(Y = y) = P(2X + 3 = y) = P \left(X = \frac{y - 3}{2} \right)
> $$
> This tells us that if $\frac{y-3}{2} \ne 0, 1, \dots, n$, then $P(Y) = 0$ as it is "unreachable" from $X$.
>
> Now, subbing this into our distribution as $X$, we find pmf
> $$
> f_Y(y) = \begin{cases}
>        \binom{n}{(y-3)/2} p^{(y-3)/2} (1-p)^{n-(y-3)/2} & y = 3, 5, \dots, 2n + 3 \\
>        0 & \text{otherwise}
> \end{cases}
> $$

## Continuous Case
In the continuous case, it is often the case that we can find the pdf of $Y$ by first finding its cdf (which can be easier to do). Consider the following examples.

> [!Example]+ Example: Transforming Continuous Random Variables
> Let $X \sim \text{Uniform} (0,4)$. Find the pdf of $Y = \sqrt{x}$.
>
> We can find the pdf of $Y$ using its cdf.
> $$
> F_Y (y) = P(Y \le y) = P( \sqrt{x} \le y ) = P ( x \le y^2 )
> $$
> 
> We can use $P(x \le y^2)$ to find the cdf of $Y$, and differentiate this cdf to find our desired pdf.
> $$
> \begin{align*}
>       F_Y (y) &= P(x \le y^2) \\
>               &= \int_{-\infty}^{y^2} f_X (x) \; dx \\
>               &= \int_{-\infty}^{y^2} \frac{1}{4} \; dx = \frac{1}{4} y^2 \\
>       f_Y (y) &= \frac{d}{dy} F_Y (y) =  \frac{1}{2} y \qquad 0 \le y \le 2
> \end{align*}
> $$

> [!Example]- Example: Transforming Continuous Random Variables (2)
> Let $X \sim N(0,1)$ be the standard normal distribution. Find the pdf of $Y = X^2$.
>
> Note that $y = x^2 \to x = \vert \sqrt{y} \vert$. We can use this to find the cdf of $Y$.
> $$
> \begin{align*}
>       F_Y(y) &= P(Y \le y) \\
>              &= P(x^2 \le y) \\
>              &= P( -\sqrt{y} \le x \le \sqrt{y} ) \\
>              &= F_X(\sqrt{y}) - F_X (-\sqrt{y})
> \end{align*}
> $$
>
> We can differentiate this expression to find the pdf of $Y$ as
> $$
> \begin{align*}
>       f_y (Y) &= \frac{d}{dy} F_Y (y) \\
>               &= f_x (\sqrt{y}) \frac{1}{2} y^{-1/2} + f_x (-\sqrt{y}) \frac{1}{2} y^{-1/2} \\
>               &= f_x (\sqrt{y}) y^{-1/2}
> \end{align*}
> $$
> For $y > 0$.

Alternatively, given that $Y = g(X)$  is strictly increasing (or decreasing), we can apply the following theorem:

> [!Abstract] Theorem: Transforming Random Variables, Continuous
> Let $f_x(x)$ be the pdf of a continuous random variable, and suppose $y = g(X)$ is strictly increasing or decreasing.
>
> Then, the pdf of $Y = g(x)$ is given as
> $$
> \begin{align*}
> f_Y(y) = \begin{cases}
>               f_x ( g^{-1} (y)) \left \vert \frac{d}{dy} g^{-1} (y) \right \vert & y = g(x) \text{ for some } x \\
>               0 & \text{otherwise}
>        \end{cases}
> \end{align*}
> $$
> Provided $\frac{d}{dy} g^{-1} (y)$ exists.
>
> > [!Note]- Proof
> > 
> > Assume $y = g(x)$ is increasing. We know $x = g^{-1} (y)$ and $dx = \frac{d}{dy} \left( g^{-1} (y) \right)$.
> >
> > We can use these facts to find this to find $P(a < Y < b)$ as
> > $$
> > \begin{align*}
> > P(a < Y < b) &= P(g^{-1} (a) < X < g^{-1} (b) ) \\
> >     &= \int_{g^{-1}(a)}^{g^{-1}(b)} f_X (x) dx \\
> >     &= \int_a^b f_X ( g^{-1} (y) ) \frac{d}{dy} g^{-1} (y) dy \\
> >     &= \text{CDF of Y} \\
> >     &= \int_a^b f_Y (y) dy
> > \end{align*}
> > $$

Consider the following examples.

> [!Example]+ Example: Transforming Continuous Random Variables (3)
> Let the pdf of $X$ be given as
> $$
> f_X (x) = \begin{cases}
>         e^{-x} & x > 0 \\
>         0 & \text{else}
>     \end{cases}
> $$
> Find the pdf of $Y = \sqrt{x}$.
>
> Because our pdf is always decreasing, using the theorem, we can find
> $$
> y = \sqrt{x} \to x = g^{-1} (y) = y^2
> $$
> 
> And use this to find the pdf as
> $$
> f_Y (y) = \begin{cases}
>         2y e^{-y^2} & y > 0 \\
>         0 & \text{else}
>     \end{cases}
> $$
