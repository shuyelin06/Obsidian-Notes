---
title: Random Variables
tags:
- work-in-progress
- stat410
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
\text{Var}(X) = E((X - E(X)^2)
$$

> [!Abstract]
> For random variable $X$, we have
> 1. $E(aX + b) = a E(X) + b$ for $a, b \in \mathbb{R}$
> 2. For $g_1(x), g_2(x)$, $E(g_1(x) + g_2(x)) = E(g_1(x)) + E(g_2(x))$. This generalizes to $n$ as well.
> 3. $\text{Var}(X) = E(x^2) - (E(x))^2$
> 4. $\text{Var}(aX + b) = a^2 V(X)$ (variance of a constant is 0).