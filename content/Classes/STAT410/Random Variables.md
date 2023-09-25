---
title: Random Variables
tags:
- stat410
- work-in-progress
---

# Section 4.1: Random Variables
We define a **random variable** $X: S \to \mathbb{R}$ as a real-valued function, which maps from a sample space $S$ to real numbers $\mathbb{R}$).

If $X$ takes on a finite or countable number of values, we say $X$ is a **discrete random variable**.

> [!Example] Example: Discrete Random Variables
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

> [!Example] Probability Mass Function
> Say we toss a coin twice, and let $X$ be the number of tails we get. Then,
> $$
> \begin{align*}
>       p(0) = P(\{HH\}) = \frac{1}{4} \\
>       p(1) = P(\{HT, TH\}) = \frac{1}{2} \\
>       p(2) = P(\{TT\}) = \frac{1}{4}
> \end{align*}
> $$

> [!Example]
> Let $S = [5] = \{1,2,3,4,5\}$, and assume one value is chosen with an equal chance.
>
> Let $X = X(i) = (i - 2)^2 - 1$, where $i$ denotes some element from the sample space. To find $p(x)$, we need to first evaluate the outputs of $X$, as by definition, $p(x)$ lists the probability of $X$'s **outputs**, not necessarily the elements from the sample space.
> $$
> \begin{align*}
>       i = 1,3 &\to x = 0 \\
>       i = 2 &\to x = -1 \\
>       i = 4 &\to x = 3 \\
>       i = 5 &\to x = 8
> \end{align*}
> $$
>
> Thus, our function $p(x)$ is a function such that
> $$
> \begin{align*}
>       p(0) = 2 / 5 \\
>       p(-1) = 1 / 5 \\
>       p(3) = 1 / 5 \\
>       p(8) = 1 / 5
> \end{align*}
> $$
> Where all other $p(x_i) = 0$. We can plot this to see the distribution, which will simply just be 4 points on the $xy$-plane.

A **cummulative distribution function (cdf)** of a random variable $X$, denoted $F_X (x) = p(X \le x)$. In other words, the value of $F_X$ is the cumulative probability of all values $p(x_i)$ such that $x_i \le x$.

> [!Example] Last Example
> From the last examle, for $-\infty < x < -1$, $F_X(x) = p(x < - 1) = 0$.
>
> For $-1 \le x < 0$, $F_X(x) = p(x < 0) = p(x = -1) = 1 / 5$
>
> For $0 \le x < 3$, $F_X(x) = p(x < 3) = p(x = 0) + p(x = -1) = 3 / 5$
>
> For $3 \le x < 8$, $F_X(x) = p(x < 8) = p(x = 3) + p(x = 0) + p(x = -1) = 4 / 5$
>
> For $x \ge 8$, $F_X(x) = 1$.
>
> Plotting our cdf, we obtain a step function.

> [!Example] CDFs
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
> - $p(2 < x \le 3) = F_X(3) - F_X(2) = 2 / 10$
> - $p(3 \le x \le 5) = F_X(5) - F_X(3) + p(x = 3)$. We have to re-add $x = 3$, as subtracting $F_X(3)$ removes that $3$ from our interval. Note that $p(x = 3) = F_X(3) - F_X(2)$, as this will get rid of everything right before $x = 3$.

> [!Abstract] Theorem
> If a discrete random variable takes on values $x_1, x_2, \dots, x_n$ such that
> $$
> x_1 < x_2 < x_3 < \dots < x_n
> $$
> Then $p(x = x_1) = F_X(x_1)$, and $p(x = x_i) = F_X(x_i) - F_X(x_{i-1})$ for $i = 2, \dots, n$.
>
> Moreover,
> - $p(a < x \le b) = F_X(b) - F_X(a)$
> - $p(a < x < b) = F_X(b) - F_X(a) - p(x = b)$
> DO BELOW - NOT DONE
> - $p(a \le x \le b) = F_X(b) - F_X(a) + p(a = b)$
> - $p(a \le x < b) = F_X(b) - F_X(x = b)

> [!Abstract] Cumulative Distribution Functions
> A function $F_X(x)$ is a cdf if and only if
> 1. $0 \le F_X(x) \le 1$ for al $x$ that $X$ takes on.
> 2. $\lim_{x \to \infty} F_X(x) = 1$
> 3. $\lim_{x \to -\infty} F_X(x) = 0$
> 4. $F_X(x)$ is non-decreasing
> 5. $F_X(x)$ is right-continuous for all $x \in \mathbb{R}$. In other words,
>    $$
>       \lim_{x \to x_0^+} F_X(x) = F_X(x_0)
>    $$

> [!Example] Example: Common Random Variable (1)
> The Bernoulli random variable is defined as
> $$
>       X = \begin{cases} 1 & \text{Success} \\ 0 & \text{Fail} \end{cases}
> $$
> Where the probability of success is $p$, and failure $1 - p$.

> [!Info] Common Random Variables: Binomial Random Variable
> The **Binomial random variable**, denoted $X\sim\text{Bin}(n,p)$, denoting the number of successes given an experiment which is done $n$ times, each with a probability of success $p$ (failure $1 - p$). 
>
> This variable will take on values $0, 1, 2, \dots, n$. Let's find its pmf.
>
> Let us have $n$ positions, and we want $x \in X$ of them to be successes. With the remaining positions, we want them to be failures.
> $$
> p(i) = p(X = i) = \binom{n}{i} p^i (1 - p)^{n - i}
> $$
>
> Let's verify this is a pmf. Observe that
> $$
> \sum_{i=0}^n p(i) = \sum_{i=0}^n \binom{n}{i} p^i (1 - p)^{n-i} = (1 + (1 - p))^n = 1
> $$
> satisfying the pmf. Note that the conversion is an application of the binomial theorem
>
> We also see that the cdf is
> $$
> F_X(i) = P(X \le i) = \sum_{j=0}^i \binom{i}{j} p^j (1 - p)^{i-j}
> $$

# Section 4.2: Expectation
If $X$ is a discrete random variable with pmf $p(x)$, then the **expected value of $X$ is given as
$$
E(X) = \sum_x x p(x) = \sum_x x p(X = x)
$$
provided that the sum $\sum_x \vert x \vert p(x)$ does NOT diverge.

Similarly, the expected value of a function $g(X)$ is given as
$$
E(g(X)) = \sum_x g(x) p(x) = \sum_x g(x) p(X = x)
$$
provided $\sum_x \vert g(x) \vert p(x)$ does NOT diverge.

If $g(x) = x^n$, then $E(g(x)) = E(x^n$ is the **n^{th} moment of $X$**.

> [!Example]
> A coin is tossed until you see tails. If you end on toss $i$, you win $(-2)^{i-1}$ dollars. What are your expected winnings?
>
> If $X$ is a random variable denoting our possible winnings, then $X$ takes on $1, -2, 4, -8, \dots$.
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
> This diverges, so we cannot possibly have an expected value (?). This makes sense, as we cannot possibly expect to get "0" money.
>
> What if we change this to winning $i$ dollars on round $i$ (instead of $2^{i-1}$)?
>
> Recall the geometric series for $\vert a \vert < 1$, telling us the $n^{th}$ sum is
> $$
> s_n = \sum_{i=0}^n a^i = \frac{1 - a^{n+1}}{1 - a}
> $$
> If the sum is infinite, we get
> $$
> \lim_{n\to\infty} \frac{1 - a^{n+1}}{1 - a} = \frac{1}{1 - a}
> $$
> Thus, in our problem, we have
> $$
> E(X) = \sum_{i=0}^\infty i \frac{1}{2}^i = 0 + 1 \frac{1}{2} + 2 \frac{1}{2}^2 + 3 \frac{1}{2}^3 + \dots
> $$
> This is a geometric series with $a = \frac{1}{2}$!
> $$
> \frac{1}{1 - a} \to \frac{1}{1 / 2} - 1 = 1
> $$
> (factor out $i = 0$ term)

The **variance** of a random variable $X$ is given by
$$
\text{Var}(X) = E\left((X - E(X))^2\right)
$$

> [!Abstract] Theorem: Expected Value and Variance
> For random variable $X$, we have
> 1. $E(aX + b) = a E(X) + b$ for $a, b \in \mathbb{R}$
> 2. For $g_1(x), g_2(x)$, $E(g_1(x) + g_2(x)) = E(g_1(x)) + E(g_2(x))$. This generalizes to $n$ as well.
> 3. $\text{Var}(X) = E(x^2) - (E(x))^2$
> 4. $\text{Var}(aX + b) = a^2 V(X)$ (variance of a constant is 0).

> [!Note] Proof (1)
> $$
> \begin{align*}
>       E(aX + b) &= \sum_x (ax + b) p(x) \\
>            &= a \sum_x x p(x) + b \sum_x p(x) \\
>            &= a E(X) + b (1) \\
>            &= a E(X) + b
> \end{align*}
> $$

> [!Note] Proof (2)
> $$
> \begin{align*}
>       E(g_1(x) + g_2(x)) &= \sum_x (g_1(x) + g_2(x)) p(x) \\
>                &= \sum_x g_1(x) p(x) + \sum_x g_2(x) p(x) \\
>                &= E(g_1(x)) + E(g_2(x))
> \end{align*}
> $$

> [!Note] Proof (3)
> $$
> \begin{align*}
>       \text{Var}(X) = V(X) &= E( (X - E(X))^2 ) \\
>                     &= E(X^2 - 2X E(X) + E(X)^2) \\
>                     &= E(X^2) - E(2X E(X)) + E(E(X)^2) &\text{ By (2)} \\
>                     &= E(X^2) - 2 E(X) E(X) + E(X)^2 &\text{ Extract Constants} \\
>                     &= E(X^2) - E(X)^2
> \end{align*}
> $$
> Note that we can take out the $E(X)$ because the expected value of $X$ is already a predetermined constant, so we can treat it as so.

> [!Note] Proof(4)
> $$
> \begin{align*}
>       V(aX + b) &= E( (aX + b)^2 ) - \left( E(aX + b)^2 \right) \\
>            &= E(a^2 X^2 + 2 aXb + b^2 ) - a^2 E(X)^2 - 2 aE(X) b - b^2 \\
>            &= a^2 E(X^2) + 2ab E(X) + b^2 - a^2 E(X)^2 - 2 ab E(X) - b^@ \\
>            &= a^2 E(X^2) - a^2 E(X)^2 \\
>            &= a^2 \left( E(X^2) - E(X)^2 \right) = a^2 V(x) 
> \end{align*}
> $$

> [!Example] Example
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
> Alternatively, we can compute $(X - E(X))^2$ per variance's actual definition.
> $$
> (X - E(X))^2 =
> \begin{cases}
>       9/4 & x = 1,4 \\
>       1/4 & x = 2,3
> \end{cases}
> $$
> Then, we'll compute the variance from these values as $V(X) = E( (X - E(X))^2 )$.
>
> Note that if $V(X)$ is large, then so is $X - E(X)$ (by definition). We can intuitively think of this variance as telling us how "far" the values of $X$ are away from the "average" expected value $E(X)$.


# Section 4.3: Examples of Discrete Random Variables
In this section, we discuss some common discrete random variables.

## Uniform Discrete Random Variable
A random variable has a **discrete uniform distribution** with parameter $n$ if any only if the pmf is given as
$$
p(x) =
\begin{cases}
      1/n & \text{for} \; x = 1, 2, \dots, n  \\
      0 & \text{otherwise}
\end{cases}
$$
> The $x = 1, 2, \dots, n$ merely indicates that elements of the random variable must have uniform spacing from one another.

Some properties of the uniform discrete random variable are given below. We use the fact that the probability is constant for all $x_i$ to make these derivations.
1. We can find our expected value as $E(X) = \frac{n+1}{2}$.
   $$
   E(X) = \sum_{i=1}^n i p(i) = \frac{1}{n} \sum_{i=1}^n = \frac{1}{n} \frac{n(n+1)}{2} = \frac{n+1}{2}
   $$
2. We can find our variance as $V(X) = \frac{(n+1)(n-1)}{12}$
   $$
   V(X) = E(X^2) - E(X)^2 = \sum_{i=1}^n i^2 \frac{1}{n} - \left( \frac{n+1}{2} \right)^2 = \frac{(n+1)(n-1)}{12}
   $$

## Bernoulli Distribution
The **Bernoulli Distribution**, often denoted $X \sim \text{Bernoulli}(p)$, returns 1 on success, and 0 on failure given some probability $p$.
$$
X =
\begin{cases}
        1 & \text{success} \\
        0 & \text{failure}
\end{cases}
$$

Here, the pmf is given as
$$
p(1) = p \qquad p(0) = 1 - p
$$

We additionally have the following properties:
1. We can find our expected value as $E(X) = p$
   $$
   E(X) = 0 (1-p) + 1(p) = p
   $$
2. We can find our variance as $V(X) = p - p^2$
   $$
   V(X) = E(X^2) - E(X)^2 = p - p^2
   $$

## Geometric Distribution
We have the **Geometric Distribution**, often denoted $X\sim\text{geom}(p)$, returns $x$ number of trials.

It's pmf gives the probability of the first success after $x$ trials, where $p$ is the probability for a success.
$$
p(x) = (1 - p)^{x-1} p \qquad \text{for} \; x = 1, 2, \dots
$$

We can confirm this pmf is valid.
$$
\sum_{x=1}^\infty = p (1-p)^{x-1} = p \sum_{x=1}^\infty (1-p)^{x-1} = p \frac{1}{1 - (1 - p)} = 1
$$

We have the following properties:
- We can find our expected value as
  $$
  E(X) = \sum_{x=1}^\infty x p (1-p)^{x-1} = p \sum_{x=1}^\infty x (1-p)^{x-1}
  $$
  Let $q = (1 - p)$ to obtain $x q^{x-1}$. We can see this as the derivative as $q^x$.
  $$
  p \frac{d}{dx} \sum_{x=1}^\infty q^x = p \frac{d}{dx} \frac{1}{1-q} = p \frac{1}{(1-q)^2} = \frac{1}{p^2}
  $$

- We now find our variance $V(X) = E(X^2) - E(X)^2$.
  $$
  \begin{align*}
  E(X^2) &= \sum_x x^2 p(x) \\
         &= \sum_{x=1}^\infty x^2 p q^{x-1} \\
         &= \sum_{x=1}^\infty (x(x-1) + x) q^{x-1} p \\
         &= \sum_{x=1}^\infty x(x-1)q^{x-1} p + \sum_{x=1}^\infty x q^{x-1} p \\
         &= pq \sum_{x=1}^\infty x(x-1)q^{x-2} + E(X) \\
         &= pq \left( \frac{d^2}{dq^2} \sum q^x \right) + \frac{1}{p} \\
         &= pq \left( \frac{2}{(1-q)^3} \right) + \frac{1}{p} = \frac{2-p}{p^2}
  \end{align*}
  $$
  Thus, $V(X) = E(X^2) - E(X)^2 = \frac{2-p}{p^2} - \frac{1}{p^2} = \frac{1-p}{p^2}$


## Binomial Distribution
The **Binomial Distribution**, denoted $X\sim\text{Binom}(n,p)$, tracks the probability of $x$ successes given $n$ trials, each with a probability of $p$. Each trial is independent of one another, so the success/failure of one does not influence the success/failure of another.

The pmf of the Binomial Distribution is given as follows:
$$
p(x) = \binom{n}{x} p^x (1-p)^{n-x}
$$

We find the expected value as
$$
\begin{align*}
        E(X) = \sum_{x=0}^n x \frac{n}{x} p^x (1-p)^{n-x} &= \sum_{x=1}^n x \frac{n!}{x!(n-x)!} p^x (1-p)^{n-x} \\
        &= np \sum_{x=1}^n \frac{(n-1)!}{(x-1)!(n-x)!} p^{x-1} (1-p)^{n-x}
\end{align*}
$$
Let $y = x-1$. Then,
$$
\begin{align*}
        E(X) = \dots &= np \sum_{x=1}^n \frac{(n-1)!}{(x-1)! ((n-1) - y))!} p^y (1-p)^{(n-1) - y)} \\
             &=np \sum_{y=0}^{n-1} \binom{n-1}{y} p^y (1-p)^{n-1-y} = np (p + (1-p))^{n-1} = np
\end{align*}
$$

We now find the variance, by finding $E(X^2)$.
$$
\begin{align*}
        E(X^2) &= \sum_{x=0}^n x^2 \binom{n}{x} p^x (1-p)^{n-x} \\
        &= \sum_{x=0}^n x \frac{n!}{(x-1)! (n-x)!} p^x (1-p)^{n-x}
\end{align*}
$$
Let $x = k + 1$. Then,
$$
\begin{align*}
        E(X^2) = \dots &= \sum_{k=0}^{n-1} np (k+1) \frac{(n-1)!}{k! (n-1-k)!} p^k (1-p)^{n-k-1} \\
        &= np \left[ \sum_{k=0}^{n-1} k \binom{n-1}{k} p^k (1-p)^{n-k-1} + \sum_{k=0}^{n-1} \binom{n-1}{k} p^k (1-p)^{n-k-1} \right] \\
        &= np ((n-1)p) + np
\end{align*}
$$
> Note the left side is $E(X)$ on $X\sim(n-1,p)$, and the right side evaluates to 1.

We use this to find $V(X)$ as
$$
        V(X) = np(1-p)
$$


## Hypergeometric Distribution
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
\begin{align*}
        E(X) &= \sum_{x=0}^k x \frac{\binom{m}{x} \binom{n-m}{k-x}}{\binom{n}{x}} \\
        &= m \sum_{x=1}^k \frac{(m-1)!}{(x-1)!(m-x)!} \frac{\binom{n-m}{k-x}}{\binom{n}{k}} \\
        &= \frac{m}{\binom{n}{k}} \sum_{x=1}^k \binom{m-1}{x-1} \binom{n-m}{k-x} = \frac{m}{\binom{n}{k}} \binom{n-1}{k-1} = \frac{km}{n}
\end{align*}
$$

We find the variance as
$$
V(X) = \frac{km (n-m) (n-k) }{n^2 (n-1) }
$$
The proof is ommitted due to how complex the calculation is.

> [!Info] Remark
> Let $p,q$ be the proportions of the successes and failures, respectively. In other words,
> $$
> p = \frac{m}{n} \qquad q = 1 - p
> $$
>
> Then, the pmf is
> $$
> p(x) = \binom{np}{x} \binom{nq}{k - x} = \binom{k}{x} p(p - \frac{1}{n}) (p - \frac{2}{n}) \dots (p - \frac{x-1}{n}) q (q - \frac{1}{n})
> $$
> Note that as $n \to \infty$, (the population gets larger), we find
> $$
> p(x) = \binom{k}{x} p^x q^{k-x}
> $$
> In other words, the binomial distribution! So, for large $n$, even though we're drawing without replacements, we'll get about the same answer as if we treated everything as independent!

## Negative Binomial
The **Negative Binomial Distribution**, denoted $X\sim\text{Negative Binomial}(r,p)$, tracks the probability of obtaining the $r^{th}$ success after $x$ trials, given that every trial has a probability of success $p$.

$$
p(x) = \binom{x-1}{r-1} p^r (1-p)^{x-r} \qquad x=r, r+1, \dots
$$

> [!Example] Negative Binomial Distribution
> If a person is exposed to a disease, 30% show symptoms, What is the probability that the $100^{th}$ person exposed is the $7^{th}$ person to show symptoms?
>
> We have a negative binomial distribution with $r = 7$ and $p = 0.3$. To find our probability, we check for $x = 100$.


Let's verify the pmf.
> Let $k = x - r$ be the number of failures. We find the probability of $k$ to be
> $$
> p(k) = \binom{k+r-1}{r-1} (1-p)^k p^r
> $$
> We can expand the following
> $$
> \binom{k+r-1}{r-1} = \frac{(k+r-1)(k+r-2) \dots (r)}{k!} = \frac{(-1)^k (-r) (-r-1) (-r-2) \dots (-r-k+1)}{(-1)^k \binom{-r}{k} k!}
> $$
>
> We have
> $$
> p^{-r} = (1 - q)^{-r} = \sum_{k=0}^\infty \binom{-r}{k} (-q)^k (1)^{-r-k} = \sum_{k=0}^\infty q^k  (-1)^k \binom{-r}{k} = \sum_{k=0}^\infty q^k \binom{r+k-1}{r-1}
> $$

We then have
$$
\sum_{k=0}^\infty p(k) = \sum_{k=0}^\infty \binom{k+r-1}{r-1} (1-p)^k p^r
$$
$$
\sum_{k=0}^\infty = p^{-r} p^{r} = 1
$$
> confirming we have a pmf?


---

We find our expected value and variance as
$$
E(X) = \frac{r}{p} \qquad V(X) = r \frac{1-p}{p^2}
$$

If our pmf is expressed in terms of $k = x - r$ the number of failures, we have
$$
E(X) = \frac{r}{p} - r \qquad V(X) = r \frac{1-p}{p^2} 
$$

## Poisson Distribution
> [!Info] Intuition

Consider a time period of 1 week, and $X$ is the number of car accidents.

We can break up this time interval into $n$ subintervals, so that for any subinterval, at most 1 accident occurs. In other words, in any subinterval, there is a probability $p$ of exactly 1 accident happening.

If each subinterval is independent, this is basically just the binomial distribution!

Thus, we can expect that as the number of subintervals increase ($n$ increases), our probability of seeing an accident in a subinterval gets smaller.

We assume here that the ratio of subintervals to probability, $np = \lambda$ is constant. Because for sufficient size $n$, we have a binomial distribution, we find $p(x)$ using the binomial distribution's pmf.

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

END OF DISCRETE RANDOM VARIABLES

above is ALL discrete random variables.



---

# Continuous Random Variables
A **continuous random variable** $X: S \to \mathbb{R}$ is a function that takes on uncountably many elements. In other words, we say $X$ is continuous if there is a non-negative function $f(x)$ such that $f(x)$ is defined for all $\mathbb{R}$ and
$$
P(X \in B) = \int_B f(x) dx
$$
where $B$ is a set of values in $\mathbb{R}$.

This gives us smooth probability curves, which can be integrated along to find probabilities.