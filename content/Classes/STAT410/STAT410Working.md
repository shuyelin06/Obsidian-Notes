---
title: STAT410Working
---

> [!Example] Example: Covariance
> Let the pdf of $X,Y$ be given as
> $$
> f(x,y) = \begin{cases}
>          2 & x > 0, y > 0, x + y < 1 \\
>          0 & \text{else}
>        \end{cases}
> $$
>
> Find $Cov(X,Y)$.
>
> We find
> $$
> \begin{align*}
>       &E(X) = \int_0^1 \int_0^{1-y} x \cdot 2 \; dx \; dy = \int_0^1 (1-y)^2 \; dy = \frac{1}{3} \\
>       &E(Y) = \int_0^1 \int_0^{1-y} y \cdot 2 \; dx \; dy = \int_0^1 2y (1 - y) \; dy = \frac{1}{3} \\
>       &E(XY) = \int_0^1 \int_0^{1-y} xy \cdot 2 \; dx \; dy = \int_0^1 y (1 - y)^2 \; dy = \frac{1}{12} \\
>       &Cov(XY) = E(XY) - E(X) E(Y) = \frac{1}{12} - \frac{1}{3} \cdot \frac{1}{3} = -1/36
> \end{align*}
> $$

> [!Abstract] Theorem: Covariance of Sums
> Let $X_1, \dots, X_n$ be random variables, and assume
> $$
> Y_1 = \sum_{i=1}^n a_i X_i \qquad Y_2 = \sum_{i=1}^n b_i X_i
> $$
>
> Then,
> $$
> Cov(Y_1, Y_2) = \sum_{i=1}^n a_i b_i V(X_i) + 2 \sum_{i < j} a_i b_j Cov(X_i, X_j)
> $$
>
> > [!Info] Corollary
> > 
> > If $Y = X_1 + X_2 + \dots + X_n$, then
> > $$
> > Cov(Y,Y) = V(Y) = \sum_{i=1}^n V(X_i) + 2 \sum_{i < j} Cov(X_i, X_j)
> > $$
> > In particular, if $X_1, \dots, X_n$ are independent, then $V(Y)$ is the sum of the variances of $X_i$!
> > $$
> > V(Y) = \sum_{i=1}^n V(X_i)
> > $$

> [!Example]
> Let the joint pdf of $X,Y$ be given as
> $$
> f(x,y) = \begin{cases}
>          \frac{1}{3} (x + y) & 0 < x < 1, 0 < y < 2 \\
>          0 & \text{else}
>        \end{cases}
> $$
>
> Find $V(Z)$, where $Z = 3X + 4Y - 5$.
>
> We can apply our theorem for $Z = 3X + 4Y - 5$. Note that because the variance of a constant is 0, we see that
> $$
> Cov(X,5) = Cov(Y,5) = 0
> $$
>
> We can now calculate
> $$
> V(3X + 4Y) = V(3X) + V(4Y) + 2 Cov(X,Y) = 9 V(X) + 16 V(X) + 2(3)(4) Cov(X,Y)
> $$
>
> We find $V(X) = 13/162$, $V(Y) = 23/81$, and $Cov(X,Y) = -1/81$ to find $V(3X + 9Y) = 805 / 162$.

> [!Example]
> Suppose we have 10 chips, 4 red, 6 blue. Let $Y$ be the number of successes, where each draw of equal chance of gettinng a red chip, without replacement.
>
> Find $E(Y)$ in 3 trials.
>
> Let $X_i$ be the random variable denoting 1 if we get a red chip on trial $i$, and 0 if we do not. We want
> $$
> \begin{align*}
> E(Y) = E( \sum_{i=1}^3 X_i ) = \sum_{i=1}^3 E(X_i) = \dots = 12/10 \\
> V(Y) = V( \sum X_i ) = \frac{18}{25}
> \end{align*}
> $$
>
> Recall that $Y \sim \text{Hypergeometric} (n,m,k)$ on $n$.
>
> In our example, $n = 10, m = 4, k = 3$. Let
> $$
> X_i = \begin{cases}
>       1 & \text{chip i drawn is red} \\
>       0 & \text{else}
>     \end{cases}
> $$
>
> What is $E (X_1)$? We find it to be $\frac{4}{10}$.
>
> What about $E (X_2)$? We find it to be
> $$
> E(X_2) = 1 P(X_2 = 1) + 0 P(X_2 = 0) = P (X_2 = 1) = (4/10) (3/9) + (6/10) (4/9) = 4/10
> $$
> > We find $E(X_3)$ to be the same.
>
> Key observation: expected values are the same with or without replacement!

---

# 8.3: The Weak and Strong Law of Large Numbers
Let $X_1, X_2, \dots$ be an infinite sequence of random variables defined on sample space $S$.

The sequence **converges in probability** to random variable $X$ if
$$
\forall \epsilon > 0, \lim_{n\to\infty} P ( |X_n - X| < \epsilon ) = 1
$$
We can reexpress this as
$$
\delta > 0, \exists N : | P( |X_n - X| < \epsilon ) - 1 | < \delta \quad n > N
$$
When this occurs, we write $X_n \to^P X$ to denote this convergence.

Denote our interval of convergence as
$$
C_{n,\epsilon} = \{ s \in S : |X_n(x) - X(S)| < \epsilon \}
$$
If the sequence converges in probability, then the this interval of convergence should eventually encompass our entire sample space as $n \to \infty$. In other words,
$$
\lim_{n\to\infty} P(C_{n,\epsilon}) = 1 \qquad \forall \epsilon > 0
$$


> [!Example]
> Let $S = [0, \infty)$ and $f(x)$ be a continuous pdf. Define
> $$
> X_n =
> \begin{cases}
>         1 & s \in (n, \infty) \\
>         0 & \text{else}
> \end{cases}
> $$
> 
> We claim $X_n$ converges in probability to the 0 random variable.
> > This should intuitively make sense, as when $n \to \infty$, the "presence of 1 in $X_n$" should get smaller and smaller (so eventually, it will disappear altogether).
> 
> Here, we have
> $$
> C_{n,\epsilon} = \{ s \in S : |X_n(s) - 0| < \epsilon \}
> $$
> 
> We see that for $s > n$, choosing any $\epsilon < 1$ will fail as $X_n(s) = 1$. Thus, our interval of convergence is $[0,n]$.
>
> $$
> \lim_{n \to \infty} P( C_{n,\epsilon} ) = \lim_{n \to \infty} \int_0^n f(x) \; dx = \int_0^\infty f(x) \; dx = 1
> $$


Let $X_1, X_2, \dots$ be an infinite sequence of random variables. We say the sequence **converges almost surely**, if for all $\epsilon > 0$,
$$
P( \lim_{n\to\infty} |X_n - X| < \epsilon ) = 1
$$
> Note that the limit is inside our probability here.

When this happens, we write $X_n \to^{a.s} X$.

> [!Info]
> Almost surely convergence implies convergence in probability.


> [!Example]
Define a random variable $X_n$ so 2 occurs more often as n gets larger. For example, we could have for various $X_i$,
$$
2, 2, 1, 2, 2, 2, 2 , 1, 2, 2, 2, 2, 2 \dots
$$

Convergence in probability? Suppose the limiting random variable is $X = 2$. We need
$$
\lim_{n\to\infty} P( |X_n - 2| < \epsilon ) = 1
$$
This is telling us that the **probability that the difference between the random variables is less than epsilon** should be equal to 1, as $n \to \infty$.

This is true, as in other words, nearly all values $X_n = 2$ as $n \to \infty$, so the chance that $|X_n - 2| < \epsilon$ will approach 100%.
$$
\lim_{n\to\infty} P(|X_n - 2| < \epsilon) = 1
$$
And thus, $X_n \to^P X$.

In the case of almost surely convergence, we want to know if
$$
P( \lim_{n\to\infty} |X_n - X| < \epsilon ) = 1
$$
In other words, we want to know if the difference between the two random variables is less than epsilon for $n \to \infty$, and want to know if the probability of this occuring is equal to 1. However, this is NOT true, as
$$
\lim_{n\to\infty} |X_n - X| < \epsilon
$$
there will always be some $X_n = 1$, meaning $|X_n - 2|$ will not be less than $\epsilon$.

---

Let $X_1, X_2, \dots$ be a sequence of independent, and identically distributed (denoted i.i.d) (same probability distribution). Assume $E(X_i)  = \mu$, and $V(X_i) = \sigma^2$.

Denote
$$
\bar{X}_n = \frac{x_1 + x_2 + \dots + x_n}{n}
$$
Observe that $E(\bar{X}_n) = \frac{1}{n} (E(X_1) + \dots + E(X_n)) = \frac{1}{n} (n \mu) = \mu$. In other words, the average expected value is the same!

However, this does not hold with the variances!
$$
V(\bar{X}_n) = \frac{1}{n^2} (V(X_1) + V(X_2) + \dots + V(X_n)) = \frac{1}{n^2} (n \sigma^2) = \frac{\sigma^2}{n}
$$
which is different.

We will show that $\bar{X}_n \to^P \mu$. In other words, the sequence should converge to the mean?
> Weak law of large numbers

---
Big Picture: The observed mean ("sample mean") converges to the expected value as the number of trials increase.

> [!Example]
> Flip a coin. If it has heads, place a blue chip in a box. Otherwise, place a red chip in the box. Let $X_i$ be the random variable of the number of blue chips added to the box for trial $i$, namely,
> $$
> X_i =
> \begin{cases}
>         1 & \text{heads} \\
>         0 & \text{tails}
> \end{cases} 
> $$
> 
> Clearly, we know that $\mu = 1/2$. However, if we test, say 4 times, we may not get this expected value! As we increase the number of tests, we should naturally expect this average to converge to the expected value.

The law of large number is broken up into two distinct cases - the **weak law** and the **strong law** of large numbers.

> [!Abstract] Theorem: Weak Law of Large Numbers (WLLN)
> If $X_1, X_2, \dots X_n$ are independent, identically distributed random variables, then
> $$
> \lim_{n\to\infty} P( |\bar{X}_n - \mu | < \epsilon) = 1
> $$
> 
> In other words, $X_n$ converges in probability to $\mu$.
>
> > [!Note] Proof
> >
> > We will show that
> > $$
> > \lim_{n\to\infty} P(|\bar{X}_n - \mu| > \epsilon) = 0
> > $$
> > to show that the contrapositive is true.
> > 
> > $$
> > \lim_{n\to\infty} P(|\bar{X}_n - \mu| > \epsilon) = \lim_{n\to\infty} P(|\bar{X}_n - \mu|^2 > \epsilon^2)
> > $$
> > 
> > Applying Markov's Inequality, we obtain
> > $$
> > \begin{align*}
> >         \lim_{n\to\infty} P(|\bar{X}_n - \mu|^2 > \epsilon^2)
> >         &\le \lim_{n\to\infty} \frac{E(|\bar{X}_n - \mu|^2)}{\epsilon^2} \\
> >         &\le \lim_{n\to\infty} \frac{V(\bar{X}_n)}{\epsilon^2} \\
> >         &\le \lim_{n\to\infty} \frac{\sigma^2}{n} \frac{1}{\epsilon^2} = 0
> > \end{align*}
> > $$

> [!Example]
> Let $X$ be the Bernoulli random variable
> $$
> X =
> \begin{cases}
>         1 & \text{Success} \\
>         0 & \text{Failure}
> \end{cases}
> $$
> 
> Let $X_i$ be the value of $X$ at trial $i$, and $\bar{X}_n$ be the "average successes".
> $$
> \bar{X}_n = \frac{X_1 + X_2 + \dots + X_n}{n}
> $$
> 
> By the Weak Law of Large Numbers, we know that $\bar{X}_n \to^P E(X)$, and we know by the Bernoulli Distribution, $E(X) = p$. Thus, the rate at which we see a success will gradually approach the probability of a success (which makes sense!).

> [!Example]
> Using the Weak Law of Large Numbers, we can prove the following theorem.
> 
> > [!Abstract] Theorem: Bernstein's Theorem
> > 
> > If $f(x)$ is continuous on $[a,b]$, then for any $\epsilon > 0$, there exists a polynomial $h(x)$ such that
> > $$
> > |f(t) - h(t)| < \epsilon 
> > $$
> > for all $t \in [a,b]$.
> >
> > In other words, we can approximate any continuous function (on an interval) with a polynomial.


> [!Abstract] Theorem: Strong Law of Large Numbers (SLLN)
> If $X_1, X_2, \dots X_n$ are independent, identically distributed random variables, then
> $$
> P \left( \lim_{n\to\infty} | \bar{X}_n - \mu | < \epsilon \right) = 1
> $$
>
> In other words, $\bar{X}_n$ converges almost surely to $\mu$.
> > Note that the Strong Law of Large Numbers also implies the Weak Law!


# 8.4: Sampling and the Central Limit Theorem
A sequence of random variables $X_1, X_2 \dots X_n$ **converges in distribution** to random variable $X$, denoted $X_n \to^d X$, if the cdfs satisfy
$$
\lim_{n\to\infty} F_{X_n} (x) = F_X (x)
$$
for all $x$ where $x$ is continuous.

> [!Example] Example: Convergence of Distributions
> $$
> X_n =
> \begin{cases}
>         1 & s = 1 \\
>         0 & s = 0
> \end{cases} \qquad
> X =
> \begin{cases}
>         1 & s = 0 \\
>         0 & s = 1
> \end{cases}
> $$
> 
> Now, because
> $$
> \lim_{n\to\infty} P( |X_n - X| < \epsilon ) \ne 1
> $$
> we know that $X_n \not\to^P X$.
> 
> However, assuming that the probability of $s$ occurring is uniformly distributed, we see that
> $$
> F_{X_n} =
> \begin{cases}
>         1/2 & 0 \le x < 1 \\
>         1 & x \ge 1
> \end{cases} = F_X
> $$
> Thus, $X_n \to^d X$.

If $X_1, X_2, \dots X_n$ are independent, identically distributed random variables, we say they constitute a **random sample** from an **infinite** population.

A **statistic** is a value calculated using this random sample (not the population). The process of calculating these statistics is known as **statistical inference**!

If $X_1, X_2, \dots X_n$ is a random sample, the **sample mean** and **sample variance** are respectively defined as
$$
\bar{X} = \frac{1}{n} \sum_{i=1}^n X_i \qquad s^2 = \frac{1}{n-1} \sum_{i=1}^n (X_i - \bar{X})^2
$$
> The unintuitive $n - 1$ in the sample variance is known as **Bessel's Correction**, and occurs as a sort of a "correction" as $X_i - \bar{X}$ is smaller than $X_i - \mu$.


> [!Abstract] Theorem:
> If $X_1, X_2 \dots X_n$ is a random sample from an infinite population with mean $\mu$ and variance $\sigma^2$, then
> $$
> E(\bar{X}) = \mu \qquad V(\bar{X}) = \frac{\sigma^2}{n}
> $$

Now, given a statistic from a sample of size $n$, we are essentially defining a function for it given the random variables $X_1, \dots X_n$. 
$$
Y = g(X_1, \dots X_n)
$$
We can thus think of this function $Y$ as its own random variable!

We then ask, what is the distribution of $Y$?

> [!Example]
> Let $X_i \sim \text{Gamma}(\alpha, \beta)$, and consider the statistic
> $$
> T = \sum_{i=1}^n X_i
> $$
>
> We showed in a previous example that $T \sim \text{Gamma}(n\alpha, \beta)$. Moreover, to find the distribution of $\bar{X} = \frac{T}{n}$, we find
> $$
> M_{\bar{X}} (t) = M_T \left( \frac{T}{n} \right) = \left( \frac{\beta}{1 - \beta t / \alpha} \right)^{n\alpha} \to \bar{X} \sim \text{Gamma}(n \alpha, \beta / n)
> $$
> But given a small manipulation in this random variable, our distribution quickly becomes a mess! For example, it's difficult to find the distribution of $Y = \bar{X} + a$, as its moment generating function doesn't match any commonly known distribution!

The **Central Limit Theorem** provides a convenient way to approximate some of the above distributions!

> [!Abstract] Theorem: Central Limit Theorem
> Let $X_1, X_2, \dots X_n$ be a sequence of independent, identically distributed random variables with mean $\mu$, variance $\sigma^2$ and moment generating function $M_x (t)$.
> 
> Then, if we define the distribution of their averages $\bar{X}$,
> $$
> \bar{X} = \frac{X_1 + X_2 + \dots + X_n}{n}
> $$
> Then the distribution $\bar{X}$ converges in distribution to the standard normal distribution! 
> $$
> \frac{(\bar{X} - \mu)}{\sigma / \sqrt{n}} \to^d N(0,1)
> $$
>
> Equivalently,
> $$
> \lim_{n\to\infty} P \left( \frac{\bar{X} - \mu}{\sigma / \sqrt{n}} < a \right) = \int_{-\infty}^a \frac{1}{\sqrt{2\pi}} e^{-x^2 / 2} \; dx
> $$
> Or in other words, 
> $$
> \lim_{n\to\infty} P \left( \frac{X_1 + X_2 + \dots + X_n - n \mu}{\sigma \sqrt{n}} < a \right) = \int_{-\infty}^a \frac{1}{\sqrt{2\pi}} e^{-x^2 / 2} \; dx
> $$
>
> > [!Note] Proof
> >
> > For the sake of simplicity, we will assume the variance is finite and use moment generating functions - however, there exist generalizations for non-fininte variances too!
> > ...

Given a statistic, the Central Limit Theorem tells us that its averages (given our sample size is sufficiently large) will become the normal distribution!

> [!Example]
> From the earlier example, $Y = \bar{X} + a$ had a moment generating function given as
> $$
> M_Y (t) = e^{at} \left( \frac{1}{1 - \beta t / n} \right)^{n \alpha}
> $$
> If we know that $\bar{X}$ is approximately the normal distribution, then we can find that $\bar{X} + a$ is approximately
> $$
> N \left(\mu + a, \frac{\sigma^2}{n} \right)
> $$


