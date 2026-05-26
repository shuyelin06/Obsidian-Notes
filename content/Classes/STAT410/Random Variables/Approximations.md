---
title: Approximations of Random Variables
tags:
- stat410
---

While we can do lots of powerful analysis with random variables, in practice, we often will not know the exact probability distribution we're working with. However, even in these cases, we can still make estimates for our distribution!

In this section, we discuss various approximations we can make, even if we do not know the exact distribution we're working with.

# Holder and Minkowski's Inequality
Below, we define inequalities relating expected values of random variables and their combinations (products and sums). These inequalities can be used to find a bound for expected values, even when the joint pdf of two random variables is unknown.

## Holder's Inequality 
**Holder's Inequality** establishes a relationship between the expected values of a random variable product as follows:

> [!Abstract] Theorem: Holder's Inequality
> Let $X$ and $Y$ be random variables, and $p > 1$ such that
> $$
> \frac{1}{p} + \frac{1}{q} = 1
> $$
>
> Then
> $$
> \begin{align*}
> \vert E(XY) \vert \le E( \vert X Y \vert ) \le \left( E( \vert X \vert^p ) \right)^{\frac{1}{p}}  \left( E ( \vert Y \vert^q) \right)^{\frac{1}{q}}
> \end{align*}
> $$
>
> The proof will be discussed later.

We can use Holder's Inequality to derive a variety of other inequalities! Consider the following.

> [!Abstract] Theorem: Cauchy-Schwarz and Lyapunov's Inequality
> Consider Holder's Inequality, and let $p = 2$. Then we get
> $$
> \vert E(XY) \vert \le \left( E(\vert X \vert^2) \right)^{\frac{1}{2}} \left( E(\vert Y \vert^2) \right)^{\frac{1}{2}}
> $$
>
> This is known as the Cauchy-Schwarz Inequality!
>
> Now, let $X = |Z|^r$ where $r$ is a value such that $1 < r < p$, and $Y = 1$. Then, we obtain the following.
> $$
> \begin{align*}
>       \vert E(XY) \vert
>       &\le E( \vert Z \vert^r ) &\text{Holder's Inequality} \\
>       &\le \left( E( \vert Z \vert^{rp} ) \right)^\frac{1}{p} &\text{Let} \; s = pr \\
>       &\le ( E(\vert Z \vert^s) )^{\frac{r}{s}} &\text{Take} \; r^{th} \; \text{Root} \\
>       E(|Z|^r)^\frac{1}{r} &\le (E(|Z|^s))^\frac{1}{s} &1 < r < s
> \end{align*}
> $$
>
> This is known as **Lyapunov's Inequality**!

Consider the below examples.

> [!Example]+ Example: Cauchy-Schwarz Inequality
> Let $X$ and $Y$ be normal distributions such that $X \sim N(\mu_1, 1)$ and $Y \sim N(\mu_2, 1)$. Assume that we know what $E(X), V(X), E(Y), V(Y)$ are.
> 
> As we do not know the joint pdf $f_{X,Y} (x,y)$, nor do we know if $X$ and $Y$ are independnet, we have no way of calculating $E(XY)$!
> 
> We do know, however, that
> $$
> V(X) = E(X^2) - E(X)^2 \Longrightarrow E(X^2) = 1 + E(X)^2
> $$
> > Variance is 1, as standard deviation is 1 (by assumption).
> 
> Thus, using the Cauchy-Schwarz Inequality, we can find that
> $$
> \begin{align*}
>         \vert E(XY) \vert
>               &\le E(X^2)^\frac{1}{2} E(Y^2)^\frac{1}{2} \\
>               &\le (1 + E(X)^2)^\frac{1}{2} (1 + E(Y)^2)^\frac{1}{2}
> \end{align*}
> $$
>
> Giving us an upper bound on $E(XY)$ without knowing the joint pdf!

> [!Example]- Example: Cauchy-Schwarz Inequality and Power Coefficient
> Suppose $Z_1 = X - E(X)$, and $Z_2 = Y - E(Y)$. We can see that
> $$
> \vert E(z_1 z_2) \vert = \vert E( (X - E(X)) (Y - E(Y)) ) \vert = \vert \text{Cov}(x,y) \vert
> $$
> 
> Then, applying the Cauchy-Scwarz Inequality,
> $$
> \begin{align*}
>         \vert E(z_1 z_2) \vert
>         &\le E(|Z_1|^2)^\frac{1}{2} E(|Z_2|^2)^\frac{1}{2} \\
>         &\le E( \vert X - E(X) \vert^2 )^\frac{1}{2} E( \vert Y - E(Y) \vert^2 )^{\frac{1}{2}} \\
>         &\le \sqrt{ V(X) } \sqrt{ V(Y) } \\
> \end{align*}
> $$
>
> Bringing these two expressions together, we obtain
> $$
> \left\vert \frac{\text{Cov}(X,Y)}{\sqrt{V(X)} \sqrt{V(Y)}} \right\vert \le 1
> $$
> 
> Proving that the correlation coefficient satisfies the condition
> $$
> \vert \mathcal{P}_{X,Y} \vert \le 1
> $$


## Minkowski's Inequality
**Minkowski's Inequality** is similar to Holder's Inequality, but it establishes a relationship between the expected values of a random variable sum, instead of a product.

> [!Abstract] Theorem: Minkowksi's Inequality
> Let $p \ge 1$. Then,
> $$
> E( \vert X + Y \vert^p)^\frac{1}{p} \le E(|X|^p)^\frac{1}{p} + E(|Y|^p)^\frac{1}{p}
> $$
>
> > [!Note]- Proof
> >
> > Applying the triangle inequality, we can find the left hand side of the expression (without the $1/p$ power) as
> > $$
> > \begin{align*}
> >     E(|X+Y|^p)
> >     &= E(|X+Y| \cdot |X+Y|^{p-1}) \\
> >     &\le E( (|X| + |Y| ) \cdot |X + Y|^{p-1} ) \\
> >     &\le E(|X| \cdot |X+Y|^{p-1} + |Y| \cdot |X+Y|^{p-1} ) \\
> >     &\le E(|X| \cdot |X+Y|^{p-1}) + E(|Y| \cdot |X+Y|^{p-1})
> > \end{align*}
> > $$
> >
> > Now, we see that in both terms, we have an expected value of a product, meaning we can apply Holder's Inequality to obtain
> > $$
> > \begin{align*}
> >     E(|X| \cdot |X+Y|^{p-1}) \le E(|X|^p)^\frac{1}{p} E(|X+Y|^{q(p-1)} )^\frac{1}{q} \\
> >     E(|Y| \cdot |X+Y|^{p-1}) \le E(|Y|^p)^\frac{1}{p} E(|X+Y|^{q(p-1)} )^\frac{1}{q}
> > \end{align*}
> > $$
> >
> > We apply this back to our initial expression to find
> > $$
> > \begin{align*}
> > E(|X+Y|^p) \le \left[ E(|X|^p)^\frac{1}{p} + E(|Y|^p)^\frac{1}{p} \right] E(|X+Y|^{q(p-1)})^\frac{1}{q}
> > \end{align*}
> > $$
> >
> > Since by Holder's Inequality, $1/p + 1/q = 1$, we have
> > $$
> > q = \frac{p}{p-1}
> > $$
> >
> > Subbing this in, we get
> > $$
> > E(|X+Y|^p) \le \left[ E(|X|^p)^\frac{1}{p} + E(|Y|^p)^\frac{1}{p} \right] E(|X+Y|^{p})^\frac{1}{q}
> > $$
> >
> > Now, dividing by $E( \vert X + Y \vert^p )^\frac{1}{q}$, we get
> > $$
> > E(\vert X + Y \vert^p)^{1 - \frac{1}{q}} = E( \vert X + Y \vert^p )^\frac{1}{p} \le E(|X|^p)^\frac{1}{p} + E(|Y|^p)^\frac{1}{p}
> > $$

Consider the below example.

> [!Example]+ Example: Minkowski's Inequality
> Let $X,Y$ both be random variables such that $X,Y \sim \text{Gamma}(\alpha,\beta)$. We know that for this distribution
> $$
> V(X) = \alpha \beta^2 \qquad E(X) = (\alpha \beta)^2 \quad \to \quad E(X^2) = V(X) + E(X)^2
> $$
> 
> For $p = 2$ in Minkowski's Inequality, the left hand side would normally yield
> $$
> E(|X+Y|^2)^\frac{1}{2} = E(|X|^2 + 2|XY| + |Y|^2)
> $$
> But this requires we know the joint distribution! Instead, we can apply our inequality to at least gain an idea of what our expected value evaluates to be.
> $$
> E(|X+Y|^2)^\frac{1}{2} \le 2 (\alpha \beta^2 + (\alpha \beta)^2)^\frac{1}{2}
> $$


# Markov and Chebyshev's Inequality
Below, we define inequalities that may be useful to obtain bounds for the probability of some portion of the probability distribution. These bounds are derived in terms of the random variable's expected value and variance.

## Markov's Inequality
**Markov's Inequality** establishes a bound for the probability of values in any distribution, and the distribution's expected value.

> [!Abstract] Theorem: Markov's Inequality
> Let $X$ be a random variable that takes on non-negative values. Then for any $a > 0$,
> $$
> P(X \ge a) \le \frac{E(X)}{a}
> $$
>
> > [!Note]- Proof
> >
> > Assume that $X$ only takes on non-negative values. Then,
> > $$
> > \begin{align*}
> >         E(X)
> >         &= \sum_{x \ge a} x P(X = x) + \sum_{x < a} x P(X = x) \\
> >         &\ge \sum_{x \ge a} x P(X = x) + 0 \\
> >         &\ge \sum_{x \ge a} a P(X = x) \\
> >         &\ge a P(X \ge a) \\
> > \end{align*}
> > $$
> >
> > Rearranging our terms, we obtain Markov's Inequality.

This inequality is generally not considered to be very useful, as it doesn't tend to give the best approximations. Plus, if we know the distribution to find the expected value, we could just calculate the exact probabilities ourselves.

Consider the below examples.

> [!Example]+ Example: Markov's Inequality
> An exam average is 75%. If we let $a = 80$, and $X$ is the random variable denoting the score on the exam, then
> $$
> P(X \ge 80) \le \frac{75}{80} \approx 0.9375
> $$
>
> Telling us that the proportion of students scoring less than 80% can be at most 93.75%.

> [!Example]- Example: Markov's Inequality (2)
> Let $X \sim \text{Binomial} (10, \frac{1}{2})$, giving us $E(X) = 5$.
> 
> If $a = 11$, we get $P(X \ge 11) \le \frac{5}{11}$, even though the probability is clearly 0.


## Chebyshev's Inequality
**Chebyshev's Inequality** establishes a bound for the probability of values within some distance from the distribution's mean.

> [!Abstract] Theorem: Chebyshev's Inequality
> Let $X$ be a random variable, and define the expected value and variance as
> $$
> \mu = E(X) \qquad \sigma^2 = V(X)
> $$
> > Note that we call $\sigma$ the **standard deviation**.
> 
> Then, for any $k > 0$,
> $$
> P(|X - \mu| \ge k) \le \frac{\sigma^2}{k^2}
> $$
> 
> In the case that $k = c \sigma$ where $c$ is a positive constant, then we can write this as
> $$
> P(|X - \mu| < c \sigma) \ge 1 - \frac{1}{c^2}
> $$
> 
> This inequality establishes a bound for the proportion of values in our distribution within some number of standard deviations from the mean.
> 
> > [!Note]- Proof
> >
> > We have
> > $$
> > \begin{align*}
> >         \sigma^2
> >         &= V(X) = E( (X - \mu)^2 ) \\
> >         &= \int_{-\infty}^\infty (x - \mu)^2 f(x) \; dx \\
> >         &= \int_{-\infty}^{\mu - k} (x - \mu)^2 f(x) \; dx + \int_{\mu - k}^{\mu + k} (x - \mu)^2 f(x) \; dx + \int_{\mu + k}^\infty (x - \mu)^2 f(x) \; dx \\
> >         &\ge \int_{-\infty}^{\mu - k} (x - \mu)^2 f(x) \; dx + 0 + \int_{\mu + k}^\infty (x - \mu)^2 f(x) \; dx 
> > \end{align*}
> > $$
> > 
> > We know that if $x - \mu \le -k$ or $x - \mu \ge k$, then $(x - \mu)^2 \ge k^2$. So, given our integral bounds, we have
> > $$
> > \begin{align*}
> >         &\ge \int_{-\infty}^{\mu - k} (x - \mu)^2 f(x) \; dx + \int_{\mu + k}^\infty (x - \mu)^2 f(x) \; dx \\
> >         &\ge \int_{-\infty}^{\mu - k} k^2 f(x) \; dx + \int_{\mu + k}^\infty k^2 f(x) \; dx \\
> >         &\ge k^2 \left( \int_{-\infty}^{\mu - k} f(x) \; dx + \int_{\mu + k}^\infty f(x) \; dx \right) \\
> >         &\ge k^2 P(|X - \mu| \ge k)
> > \end{align*}
> > $$
> > 
> > Giving us
> > $$
> > P(|X - \mu| \ge k) \le \frac{\sigma^2}{k^2}
> > $$


> [!Example]+ Example: Chebyshev's Inequality
> Let the pdf of $X$ be given as
> $$
> f(x) =
> \begin{cases}
>         630x^4 (1 - x)^4 & 0 < x < 1 \\
>         0 & \text{else}
> \end{cases}
> $$
> 
> Integrating for the expected value and standard deviation yields the following values.
> $$
> \mu = E(X) = \frac{1}{2} \qquad \sigma = \sqrt{\frac{1}{44}} \approx 0.15
> $$
> 
> Using these values, by Chebyshev's Inequality, the probability that $X$ will take on values within 2 standard deviations of the mean is 
> $$
> \begin{align*}
>       P(|X - \mu| < c \sigma) \ge 1 - \frac{1}{c^2} \\
>       P(|X - \mu| < 2\sigma) \ge \frac{3}{4}
> \end{align*}
> $$

> [!Example]- Example: Chebyshev's Inequality (2)
> An IQ test has mean of 100 and standard deviation of 16. Show that the probability a person has an IQ of at least 148 or at most 52 is at most $\frac{1}{9}$.
> 
> We apply Chebyshev's theorem. Here, we want $X \ge 148$ and $X \le 52$
> $$
> |X-100| \ge 48
> $$
> 
> By Chebyshev's, we have
> $$
> P(|X-100| \ge 48) = \frac{16^2}{48^2}
> $$


# The Weak and Strong Law of Large Numbers
## Convergence in Probability
Let $X_1, X_2, \dots$ be an infinite sequence of random variables defined on sample space $S$.

Then, this sequence of random variables **converges in probability** (denoted $X_n \to^P X$) to random variable $X$ if
$$
\forall \epsilon > 0, \lim_{n\to\infty} P ( |X_n - X| < \epsilon ) = 1
$$
In other words, if the sequence converges in probability, then the probability that as $n \to \infty$, the next $X_n$ in the sequence equals $X$ should approach 1.

Given a random variable from the sequence $X_n$, and $X$, we define the interval in which they are equal to one another as their **interval of convergence**, denoted $C_{n,\epsilon}$.
$$
C_{n,\epsilon} = \{ s \in S : |X_n(x) - X(S)| < \epsilon \}
$$

If the sequence converges in probability, then the this interval of convergence should eventually encompass our entire sample space as $n \to \infty$. This is formally expressed as
$$
\lim_{n\to\infty} P(C_{n,\epsilon}) = 1 \qquad \forall \epsilon > 0
$$
In other words, the probability that as $n \to \infty$, any $x \in S$ we select in our sample space is within our interval of convergence should approach 1.

We can use the idea of interval of convergence to show that the sequence does indeed converge in probability. Consider the following example.

> [!Example]+ Example: Convergence in Probability
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
> We see that for $s > n$, $X_n(s) = 1$, which would fail to satisfy the interval of convergence (choose any $\epsilon < 1$). Thus, our interval of convergence is $[0,n]$.
>
> Now, taking this as $n \to \infty$, we can see that our interval of convergence will encompass our entire space. We can alternatively express this as follows:
>
> $$
> \lim_{n \to \infty} P( C_{n,\epsilon} ) = \lim_{n \to \infty} \int_0^n f(x) \; dx = \int_0^\infty f(x) \; dx = 1
> $$
>
> In other words, the probability any $x \in S$ we choose is inside our interval approaches 1 as $n \to \infty$.

## Almost Sure Convergence
Like before, let $X_1, X_2, \dots$ be an infinite sequence of random variables.

We say the sequence **converges almost surely** (denoted $X_n \to^{a.s} X$), if for all $\epsilon > 0$,
$$
P \left( \lim_{n\to\infty} |X_n - X| < \epsilon \right) = 1
$$
In other words, as $n \to \infty$, a random variable from our sequence $X_n$ should equal random variable $X$.
> Note that unlike our definition of convergence in probability, the limit is inside our probability now.

Note that if a sequence almost surely converges to $X$, then it must also converge in probability to $X$. However, the converse is not necessarily true! Consider the following example.

> [!Example]+ Example: Almost Sure Convergence vs Convergence in Probability
> Define a random variable $X_n$ so 2 occurs more often as n gets larger. For example, we could have for various $X_i$,
> $$
> 2, 2, 1, 2, 2, 2, 2 , 1, 2, 2, 2, 2, 2 \dots
> $$
> 
> As $n \to \infty$, we see that the probability that the next random variable in the sequence is $X_n = 2$ approaches 1, as $X_n = 2$ becomes more and more frequent. In other words, the sequence converges in probability.
>
> More formally, we know that
> $$
> \lim_{n\to\infty} P( |X_n - 2| < \epsilon ) = 1
> $$
> Showing that $X_n \to^P X$.
>
> However, as there will always be occurrences of $X_n = 1$ as $n \to \infty$, so the sequence does not converge almost surely to $X$. More formally, we know that the condition
> $$
> P( \lim_{n\to\infty} |X_n - X| < \epsilon ) = 1
> $$
> will not be satisfied, so $X_n \not\to^{a.s.} X$.

## Weak and Strong Law of Large Numbers
Suppose that $X_1, X_2, \dots$ are a sequence of independent and identically distributed (denoted i.i.d) random variables (i.e. they have the exact same probability distribution). Assume that for any random variable in the sequence $X_i$, that $E(X_i)  = \mu$, and $V(X_i) = \sigma^2$.

Now, denote a new random variable as the average of these sequences, such that
$$
\bar{X}_n = \frac{x_1 + x_2 + \dots + x_n}{n}
$$

We observe that
$$
E(\bar{X}_n) = \frac{E(X_1) + \dots + E(X_n)}{n} = \frac{n \mu}{n} = \mu = E(X_i)
$$
In other words, the average expected value is the same as any individual expected value!

However, this property does not hold with the variances!
$$
V(\bar{X}_n) = \frac{V(X_1) + V(X_2) + \dots + V(X_n)}{n^2} = \frac{n \sigma^2}{n^2} = \frac{\sigma^2}{n}
$$

Thus, we can see that as $n \to \infty$, the variance of $\bar{X}_n$ drops to 0, whereas it's expected value converges to $\mu$. In other words, as $n \to \infty$, $\bar{X}_n$ will converge to $\mu$!.

In practice, this means that if we have an experiment, as the number of trials increase (where each trial is represented by its own random variable $X_i$), the observed mean will converge to the actual expected mean! Such an observation is extremely important, and is formalized in what is known as the **Law of Large Numbers**.

> [!Example]+ Example: Law of Large Numbers (Intuition)
> Flip a coin. If it has heads, place a blue chip in a box. Otherwise, place a red chip in the box. Let $X_i$ be the random variable of the number of blue chips added to the box for trial $i$, namely,
> $$
> X_i =
> \begin{cases}
>         1 & \text{heads} \\
>         0 & \text{tails}
> \end{cases} 
> $$
> 
> Clearly, we know that $\mu = 1/2$. However, if we test, say 4 times, we may not get this expected value, by virtue of randomness!
>
> However, as we increase the number of tests, we should naturally expect this average to converge to the expected value. This is the premise behind the Law of Large Numbers!

The Law of Large Numbers is split into two distinct cases, known as the **Weak Law** and the **Strong Law** of Large Numbers.

Let's now look at the **Weak Law of Large Numbers**.

> [!Abstract] Theorem: Weak Law of Large Numbers (WLLN)
> Let $X_1, X_2, \dots X_n$ are independent, identically distributed random variables, such that $E(X_i) = \mu$, and define their average as $\bar{X}_n$.
> $$
> \bar{X}_n = \frac{X_1 + X_2 + \dots X_n}{n}
> $$
>
> Then,  $X_n$ converges in probability to $\mu$.
> $$
> \lim_{n\to\infty} P( |\bar{X}_n - \mu | < \epsilon) = 1
> $$
> In other words, as $n \to \infty$, the probability that the next $X_n = \mu$ will approach 1.
>
> > [!Note]- Proof
> >
> > By way of contrapositive, we wish to show that
> > $$
> > \lim_{n\to\infty} P(|\bar{X}_n - \mu| \ge \epsilon) = 0
> > $$
> > to show that the contrapositive is true.
> > 
> > $$
> > \lim_{n\to\infty} P(|\bar{X}_n - \mu| \ge \epsilon) = \lim_{n\to\infty} P(|\bar{X}_n - \mu|^2 \ge \epsilon^2)
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

Consider the below examples of Weak Law of Large Numbers.

> [!Example]+ Example: Weak Law of Large Numbers (1)
> Let $X$ be the Bernoulli random variable.
> $$
> X =
> \begin{cases}
>         1 & \text{Success} \\
>         0 & \text{Failure}
> \end{cases}
> $$
> 
> Now let $X_i$ denote the value of $X$ at trial $i$, and $\bar{X}_n$ be the "average number of successes".
> $$
> \bar{X}_n = \frac{X_1 + X_2 + \dots + X_n}{n}
> $$
> 
> By the Weak Law of Large Numbers, we know that $\bar{X}_n \to^P E(X)$, and furthermore, we know by the Bernoulli Distribution, $E(X) = p$.
>
> Thus, the rate at which we see a success will gradually approach the probability of a success, which makes intuitive sense!

Interestingly enough, we can use the Weak Law of Large Numbers to prove the following theorem, though we will not cover its uses.

> [!Abstract] Theorem: Bernstein's Theorem
> If $f(x)$ is continuous on $[a,b]$, then for any $\epsilon > 0$, there exists a polynomial $h(x)$ such that
> $$
> |f(t) - h(t)| < \epsilon 
> $$
> for all $t \in [a,b]$.
>
> In other words, we can approximate any continuous function (on an interval) with a polynomial.

Let's now look at the **Strong Law of Large Numbers**, which is much stronger.

> [!Abstract] Theorem: Strong Law of Large Numbers (SLLN)
> Let $X_1, X_2, \dots X_n$ are independent, identically distributed random variables, such that $E(X_i) = \mu$, and define their average as $\bar{X}_n$.
> $$
> \bar{X}_n = \frac{X_1 + X_2 + \dots X_n}{n}
> $$
>
> Then, $\bar{X}_n$ converges almost surely to $\mu$.
> $$
> P \left( \lim_{n\to\infty} | \bar{X}_n - \mu | < \epsilon \right) = 1
> $$
>
> In other words, as $n \to \infty$, our $\bar{X}_n$ will gradually approach our expected value $\mu$.
>
> > Note that the Strong Law of Large Numbers also implies the Weak Law!


# The Central Limit Theorem
## Sampling
Suppose we have a sequence of random variables $X_1, X_2 \dots X_n$.

This sequence **converges in distribution** to random variable $X$, denoted $X_n \to^d X$, if their cdfs satisfy
$$
\lim_{n\to\infty} F_{X_n} (x) = F_X (x)
$$
for all $x$ where $x$ is continuous. In other words, as $n \to \infty$, their cdfs converge to that of $X$.

Note that convergence in distributions is distinct from convergence in probability (from the previous section). See the following example.

> [!Example]+ Example: Convergence of Distributions
> $$
> X_n =
> \begin{cases}
>         1 & s = 1 \\
>         0 & s = 0
> \end{cases} \qquad
> X =
> \begin{cases}
>         0 & s = 1 \\
>         1 & s = 0 \\
> \end{cases}
> $$
> 
> Now, because $X_n$ will never equal $X$ as $n \to \infty$, we know that $X_n$ doesn't converge in probability to $X$.
> 
> However, if we assume that the probability of $s$ occurring is uniformly distributed, we see that
> $$
> F_{X_n} =
> \begin{cases}
>         1/2 & 0 \le x < 1 \\
>         1 & x \ge 1
> \end{cases} = F_X
> $$
> As we have a 50% chance of obtaining a 0, and a 50% chance of obtaining a 1. Thus, $X_n \to^d X$. 

If $X_1, X_2, \dots X_n$ are independent, identically distributed random variables, we say they constitute a **random sample** from an **infinite** population.

A **statistic** denotes any value calculated using this random sample (not the population). The process of calculating these statistics is known as **statistical inference**!

If $X_1, X_2, \dots X_n$ is a random sample, the **sample mean** and **sample variance** is respectively defined as
$$
\bar{x} = \frac{1}{n} \sum_{i=1}^n X_i \qquad s^2 = \frac{1}{n-1} \sum_{i=1}^n (X_i - \bar{X})^2
$$
> The unintuitive $n - 1$ in the sample variance is known as **Bessel's Correction**, and occurs as a sort of a "correction" as $X_i - \bar{X}$ is smaller than $X_i - \mu$.


> [!Abstract] Theorem: Convergence of Statistics
> If $X_1, X_2 \dots X_n$ is a random sample from an infinite population with mean $\mu$ and variance $\sigma^2$, then
> $$
> E(\bar{X}) = \mu \qquad V(\bar{X}) = \frac{\sigma^2}{n}
> $$

Given a statistic from a sample of size $n$, we are essentially defining a function for it, given the random variables $X_1, \dots X_n$. 
$$
Y = g(X_1, \dots X_n)
$$
Thus, we can actually think of this function $Y$ as its own random variable! If this is the case, then what is the distribution of $Y$?

This question can be pretty difficult to answer, and even small manipulations in our function can make the problem really difficult! Consider the following example.

> [!Example]+ Example: Distributions of Statistics
> Let $X_i \sim \text{Gamma}(\alpha, \beta)$, and consider the statistic
> $$
> T = \sum_{i=1}^n X_i
> $$
>
> We showed in a previous example that $T \sim \text{Gamma}(n\alpha, \beta)$. Moreover, to find the distribution of $\bar{X} = T/n$, we can find
> $$
> M_{\bar{X}} (t) = M_T \left( \frac{T}{n} \right) = \left( \frac{\beta}{1 - \beta t / \alpha} \right)^{n\alpha} \to \bar{X} \sim \text{Gamma}(n \alpha, \beta / n)
> $$
> But given a small manipulation in this random variable, our distribution quickly becomes a mess! For example, it's difficult to find the distribution of $Y = \bar{X} + a$, as its moment generating function doesn't match any commonly known distribution!

To work around that, we can use what's known as the **Central Limit Theorem**, which provides a convenient way to approximate some of the above distributions!

> [!Abstract] Theorem: Central Limit Theorem
> Let $X_1, X_2, \dots X_n$ be a sequence of independent, identically distributed random variables with mean $\mu$, variance $\sigma^2$ and moment generating function $M_x (t)$. Furthermore, let $\bar{X}$ be the distribution of their averages.
> $$
> \bar{X} = \frac{X_1 + X_2 + \dots + X_n}{n}
> $$
> Then, the distribution $\bar{X}$ converges in distribution to the standard normal distribution! 
> $$
> \frac{(\bar{X} - \mu)}{\sigma / \sqrt{n}} \to^d N(0,1)
> $$
> 
> Equivalently, we can express this as 
> $$
> \begin{align*}
>       &\lim_{n\to\infty} P \left( \frac{\bar{X} - \mu}{\sigma / \sqrt{n}} < a \right) = \int_{-\infty}^a \frac{1}{\sqrt{2\pi}} e^{-x^2 / 2} \; dx \quad \Longrightarrow \\
>       &\lim_{n\to\infty} P \left( \frac{X_1 + X_2 + \dots + X_n - n \mu}{\sigma \sqrt{n}} < a \right) = \int_{-\infty}^a \frac{1}{\sqrt{2\pi}} e^{-x^2 / 2} \; dx
> \end{align*}
> $$
>
> Which is often a more useful definition to use, as we are more often interested in some probability from the summation $X_1 \dots X_n$ itself, rather than their average.
>
> > [!Note]- Proof
> >
> > For the sake of simplicity, we will assume the variance is finite and use moment generating functions - however, there exist generalizations for non-fininte variances too!
> > 
> > > [!Abstract] Lemma
> > >
> > > Let $F(x), F_1 (x), F_2 (x), \dots$ be the cdfs of random variables $X, X_1, X_2, \dots$ (respectively) with moment generating functions given by $M(t), M_1 (t), M_2(t), \dots$. Then, if
> > > $$
> > > \lim_{n\to\infty} M_{X_n} (t) = M_X (t)
> > > $$
> > > then $X_n \to^d X$.
> > 
> > > [!Abstract] Theorem (Taylor)
> > >
> > > Let $P_n (x)$ be the $n^{th}$ degree Taylor polynomial centered around "a". Then,
> > > $$
> > > P_n (x) = \sum_{k=0}^n \frac{f^k (a)}{k!} (x - a)^k
> > > $$
> > > Furthermore, there is a $c \in (a,x)$ such that
> > > $$
> > > f(x) = P_n(x) + \frac{f^{n+1} (c)}{(n+1)!} (x - c)^{n+1}
> > > $$
> > 
> > To prove the Central Limit Theorem, if $Z_n = \frac{\bar{X} - \mu}{\sigma / \sqrt{n}}$, it suffices to show that $M_{Z_n} (t) \to e^{-t^2 / 2}$, the mgf of the standard normal distribution.
> > 
> > We have
> > $$
> > \begin{align*}
> >         Z_n
> >         &= \frac{\bar{X} - \mu}{\sigma / \sqrt{n}} \\
> >         &= \frac{\frac{1}{n} \sum X_i - \mu}{\sigma / \sqrt{n}} \\
> >         &= \frac{1}{n} \sum_{i=1}^n \frac{X_i - \mu}{\sigma} \\
> >         &= \frac{1}{n} \sum_{i=1}^n Y_i
> > \end{align*}
> > $$
> > 
> > Now observe that
> > $$
> > \begin{align*}
> >         E(Y_i)
> >         &= E \left( \frac{X_i - \mu}{\sigma} \right) \\
> >         &= \frac{1}{\sigma} E(X_i - \mu) = 0 \\
> >         V(Y_i)
> >         &= V \left( \frac{X_i - \mu}{\sigma} \right) \\
> >         &= \frac{1}{\sigma^2} V(X_i) = 1
> > \end{align*}
> > $$
> > 
> > Recall that if $M_X (t)$ is an mgf, then $M_X^r (0) = \mu_r' = E(X^r)$. Above, we just found that
> > $$
> > \begin{align*}
> >         M_{Y_i} (0) = E(1) = 1 \\
> >         M_{Y_i}' (0) = E(Y_i) = 0 \\
> >         M_{Y_i}'' (0) = V(Y_i) = 1
> > \end{align*}
> > $$
> > 
> > Now, applying Taylor's theorem, we can approximate the mgf $M_{Y_i} (t)$ as
> > $$
> > \begin{align*}
> >         M_{Y_i} (t)
> >         &= M_{Y_i} (0) + M_{Y_i}' (0) \frac{t}{1} + M_{Y_i}'' (c) \frac{t^2}{2!} \qquad 0<c<t \\
> >         &= 1 + M_{Y_i}'' (c) \frac{t^2}{2} \\
> >         &= 1 + \frac{t^2}{2} + \frac{1}{2} (M_{Y_i}'' (c) - 1) t^2
> > \end{align*}
> > $$
> > 
> > Recall the following properties of mgfs
> > 1. $M_{bX} (t) = M_X (tb)$
> > 2. The mgf of the sum of random variables equals the product of the mgfs
> > 
> > $$
> > \begin{align*}
> >         M_{Z_n} (t)
> >         &= M_{\frac{1}{\sqrt{n}} Y_i} (t)^n \\
> >         &= M_{Y_i} (t / \sqrt{n})^n \\
> >         &= \left[ 1 + \frac{1}{2} \left( \frac{t}{\sqrt{n}} \right)^2 + \frac{1}{2} (M_{Y_i}'' (c) - 1) \left( \frac{t}{\sqrt{n}} \right)^2 \right]^n \quad 0 < c < \frac{t}{\sqrt{n}} \\
> > \end{align*}
> > $$
> > 
> > Now, notices that as $n \to \infty$, $\frac{t}{\sqrt{n}} \to 0$ forcing $c \to 0$. Thus, we obtain
> > $$
> > \begin{align*}
> > &\lim_{n\to\infty} \left[ 1 + \frac{1}{2} \left( \frac{t}{\sqrt{n}} \right)^2 + \frac{1}{2} (M_{Y_i}'' (c) - 1) \left( \frac{t}{\sqrt{n}} \right)^2 \right]^n \\
> > &= \lim_{n\to\infty} \left[ 1 + \frac{t^2 / 2}{n} \right]^n \\
> > &= e^{t^2/2}
> > \end{align*}
> > $$
> > 
> > Which is the moment generating function of $N(0,1)$! Thus, $Z_n$ converges in distribution to the standard normal distribution.

Given a statistic, the Central Limit Theorem tells us that the distribution of its averages (given our sample size is sufficiently large) will become the normal distribution! This is extremely useful in approximating what the probability of a statistic occurring.

> [!Example]+ Example: Central Limit Theorem (1)
> The amount of nicotine in a cigarette can be expressed by a random variable  with mean $\mu = 0.8$ mg, and standard deviation $\sigma = 0.1$ mg. Suppose there are 20 cigarettes in one pack. 
> 
> If a person smokes 5 packs of cigarettes a week, what is the probability the total nicotine consumed in a week is at least 82 mg?
> 
> Because we have 20 cigarettes over 5 packs, we find that the person smokes a total of 100 cigarettes per week. Let $X_i$ denote the amount of nicotine in cigarette $i$. If
> $$
> X = \sum_{i=1}^{100} X_i
> $$
> 
> We want $P(X \ge 82)$. Applying our theorem, we find
> $$
> \begin{align*}
>         P(X \ge 82)
>         &= P \left( \frac{X - 100(0.8)}{0.1 \sqrt{100}} \ge \frac{82 - 100(0.8)}{0.1 \sqrt{100}} \right) \\
>         &= P(z \ge 2) \\
>         &= 1 - \Phi(2)
> \end{align*}
> $$

> [!Example]- Example: Central Limit Theorem (2)
> In a sample of 25 people, their height is measured. We find $\bar{X} = 67.64$ inches (note that this is the sample mean). Now suppose the population variance is $\sigma^2 = 9$.
> 
> Use the Central Limit Theorem to find the probability that $\mu$ exceeds 70 inches.
> 
> Here, if $\mu = 70$, we see that
> $$
> Z = \frac{\bar{X} - \mu}{\sigma / \sqrt{n}} = \frac{67.64 - 70}{3 / \sqrt{25}} \approx -3.266
> $$
> As $\mu$ increases, this will only become more negative, so we want to know the probability that
> $$
> P(Z < -3.266) = \Phi(-3.266) = 0.00056
> $$

Observe that in many situations, we start with a discrete random variable, and approximate it with $N(0,1)$, a continuous random variable. Under this conversion from discrete to continuous, it's most ideal to use a **continuity correction** to account for any error from this conversion, where
$$
P(X = i) \approx P(i - 1/2 < X < i + 1/2)
$$
> Note that this correction is applied on $X$, and is most particularly effective for integers. 

> [!Example]+ Example: Continuity Correction
> 10 dice are rolled. Determine the probability the sum is between 30 and 40, inclusive.
> 
> Let's use the Central Limit Theorem. Let $X_i$ e the value rolled on die $i$, with mean $\frac{7}{2}$, and variance $\sigma^2 = \frac{35}{12}$. Define $X$ as the sum of all $X_i$'s,
> $$
> X = \sum_{i=1}^{10} X_i
> $$
> 
> As we are attempting to convert a discrete random variable into the continuous normal distribution, we will use a continuity correction and check for the probabilty
> $$
> \begin{align*}
>         P (29.5 \le X \le 40.5)
>         &= P \left( \frac{29.5 - 35}{\sqrt{\frac{35}{12}} \sqrt{10}} \le \frac{X - 35}{\sqrt{\frac{35}{12}} \sqrt{10}} \le \frac{40.5 - 35}{\sqrt{\frac{35}{12}} \sqrt{10}} \right) \\
>         &= P(-1.014 \le Z \le 1.014) \\
>         &= \Phi(1.014) - \Phi(-1.014) \approx 0.7
> \end{align*}
> $$


# Contelli and Jensen's Inequality
## Contelli's Inequality
Recall Markov's Inequality. 
$$
P(X \ge a) \le \frac{E(X)}{a}
$$

From this inequality, we can derive another known as **Contelli's Inequality**, which is often referred to as the **One-Sided Chebyshev**.

> [!Abstract] Theorem: Contelli's Inequality
> Let $X$ be a random variable. If $a > 0$, then
> $$
> P(X - E(X) \ge a) \le \frac{\sigma^2}{\sigma^2 + a^2}
> $$
>
> > [!Note]- Proof
> > 
> > Let $b > 0$. Then,
> > $$
> > \begin{align*}
> > P(X - E(X) \ge a
> > &= P(X \ge a + E(X)) \\
> > &= P(X + b \ge (a + b) + E(X) \\
> > &= P( (X + b)^2 \ge ( (a + b) + E(X) )^2 ) \\
> > &\le \frac{E ((X + b)^2)}{(a + b + E(X))^2} &\text{Markov's Inequality} \\
> > &\le \frac{\sigma^2 + (b + \mu)^2}{(a + b + \mu)^2} &b = \frac{\sigma^2}{a} - \mu \\
> > &\le \frac{\sigma^2}{\sigma^2 + a^2}
> > \end{align*}
> > $$

 > [!Example]+ Example: Contelli's Inequality
 An exam had average of 75% and a variance of 8%. Find an upper bound on the probability a student had at least an 80%.
> 
> Using Contelli's Inequality, we have that
> $$
> \begin{align*}
>         P(X \ge 80)
>         &= P(X - 75 \ge 5) \\
>         &\le \frac{8^2}{8^2 + 5^2} \approx 0.72
> \end{align*}
> $$

## Jensen's Inequality
A twice differentiable function $g(x)$ is **convex** if $g''(x) > 0$. More formally, for all $t$, $0 \le t \le 1$, and $x_1, x_2$, $g(x)$ is convex if 
$$
g(tx_1 + (1 - t)x_2) \le tg(x_1) + (1-t) g(x_2)
$$
> This is essentially saying, all values between $x_1$ and $x_2$ are at most the value at the straight line formed between $g(x_1)$ and $g(x_2)$.

We say $g(x)$ is **concave** if $-g(x)$ is convex.

We use this property of convex functions to define a really powerful inequality known as **Jensen's Inequality**.

> [!Abstract] Theorem: Jensen's Inequality
> Let $X$ be a random variable. If $g(x)$ is a convex function over the entire interval that $X$ takes on, then
> $$
> E(g(X)) \ge g(E(X))
> $$
>
> Note that this inequality can be reversed for concave functions.
>
> > [!Note]- Proof
> >
> > Let $g(x)$ be a convex function. We use Taylor's theorem, centered at $\mu = E(X)$
> > $$
> > g(X) = g(\mu) + g'(u) (x - \mu) + \frac{1}{2} g''(c) (x - \mu)^2 \quad c \in (\mu, x)
> > $$
> > 
> > By assumption, we know that $g''(c)$ is convex. So, it's term must be non-negative.
> > $$
> >         g(\mu) + g'(u) (x - \mu) + \frac{1}{2} g''(c) (x - \mu)^2 \ge g(\mu) + g'(\mu) (x - \mu)
> > $$
> > 
> > Applying the expected value on both sides, we get
> > $$
> > \begin{align*}
> >         E(g(X))
> >         &\ge E(g(\mu) + g'(\mu) (x - \mu)) \\
> >         &\ge E(g(\mu)) + E( g'(\mu) (x - \mu)) \\
> >         &\ge g(\mu) + g'(\mu) E(x - \mu) \\
> >         &\ge g(\mu) + g'(\mu) ( E(X) - \mu ) \\
> >         &\ge g(\mu) + 0 \\
> >         &\ge g(E(X))
> > \end{align*}
> > $$

Consider the following examples.

> [!Example]+ Example: Jensen's Inequality (1)
> Let $X$ be a random variable taking on values greater than -1. Assume $E(X) = 100$. Apply Jensen's Inequality to obtain a bound on $E(\frac{1}{1 + X})$.
>
> Let $g(x) = \frac{1}{1 + x}$. We know that $g''(x) = \frac{2}{(x + 1)^3} > 0$ for all $x > -1$.
>
> Then, applying Jensen's Inequality, it must be true that
> $$
> E \left( \frac{1}{1 + X} \right) \ge \frac{1}{1 + (100)}
> $$

> [!Example]- Example: Jensen's Inequality (2)
> Let $g(x) = x^2$.
>
> By Jensen's Inequality, $E(X^2) \ge (E(X))^2$, so
> $$
> V(X) = E(X^2) - (E(X))^2 \ge 0
> $$
>
> Proving that variance is always non-negative.


Now, consider any non-uniform pmf
$$
p(x) =
\begin{cases}
        P_i & x = a_i, 1 \le i \le n \\
        0 & \text{else}
\end{cases}
\qquad
\sum P_i = 1
$$

Applying the proof for Jenson's Inequality with $g(x) = \ln(x)$ (refer to proof), we obtain the following.
$$
a_1^{p_1} a_2^{p_2} \dots a_n^{p_n} \le p_1 a_1 + p_2 a_2 + \dots p_n a_n
$$

This is oftentimes considered a generalization of Jenson's Inequality.


We can use Jensen's Inequality to derive a variety of other useful theorems. Consider the following.

### Arithmetic, Geometric, and Harmonic Means
Let $a_i > 0$. Then, we can define the following means
$$
\begin{align}
        &\frac{1}{n} \sum_{i=1}^n a_i &\text{Arithmetic Mean} \\
        &\sqrt[n]{\prod_{i=1}^n a_i} &\text{Geometric Mean} \\
        &\frac{n}{\sum_{i=1}^n \frac{1}{a_i}} &\text{Harmonic Mean}
\end{align}
$$

> [!Example]+ Example: Arithmetic and Harmonic Means
> A car drives 60 mph for 3 hours one way, and 20 mph for 3 hours. What is its average speed?
> 
> Intuitively, we calculate the average speed as
> $$
> \frac{3 \cdot 60 + 3 \cdot 20}{3 + 3} = 40
> $$
> which is the arithmetic mean.
> 
> Now suppose that this car travels 60 miles each way. On the way there, it goes 60 mph, and on the way back, it goes 20 mph. Now,  we are instead calculating the harmonic mean.
> $$
> \frac{2 \cdot 60}{\frac{60}{60} + \frac{60}{60}} = 30
> $$

> [!Abstract] Theorem: Arithmetic, Geometric, and Harmonic Means
> It is always the case that
> $$
> \text{Harmonic Mean} \le \text{Geometric Mean} \le \text{Arithmetic Mean}
> $$
>
> > [!Note]- Proof
> >
> > Define the pmf $p(x)$ as
> > $$
> > p(x) =
> > \begin{cases}
> >         \frac{1}{n} & x = a_1, a_2, \dots \\
> >         0 & \text{else}
> > \end{cases}
> > $$
> > 
> > Let $g(x) = \ln(x)$. We see that $g''(x) = - \frac{1}{x^2} < 0$ for $x > 0$. Then, we find the arithmetic mean as
> > $$
> > E(X) = \frac{1}{n} \sum_{i=1}^n a_i
> > $$
> > 
> > And we find the geometric mean as
> > $$
> > \begin{align*}
> >         &E(g(x)) = E(\ln{x}) \\
> >         &= \frac{1}{n} \ln{a_1} + \frac{1}{n} \ln{a_2} + \dots + \frac{1}{n} \ln{a_n} \\
> >         &= \frac{1}{n} \ln( \prod a_i ) \\
> >         &= \ln( \prod a_i ^{\frac{1}{n}} ) = \ln(GM)
> > \end{align*}
> > $$
> > 
> > By Jensen's Inequality,
> > $$
> > \ln(GM) = E(g(x)) \le g(E(x)) = \ln(AM) \Longrightarrow GM \le AM
> > $$
> > 
> > Now to show that $HM \le GM$, we define the pmf
> > $$
> > p(y) =
> > \begin{cases}
> >         \frac{1}{n} & \frac{1}{a_1}, \frac{1}{a_2}, \dots \frac{1}{a_n} \\
> >         0 & \text{else}
> > \end{cases}
> > $$
> > 
> > Again, let $g(y) = \ln(y)$. Then,
> > $$
> > E(Y) = \frac{1}{n} \sum_{i=1}^n \frac{1}{a_i} = \frac{1}{HM} \Longrightarrow g(E(Y)) = \ln(1/HM)
> > $$
> > 
> > And
> > $$
> > E(g(Y)) = E(\ln(Y)) = \frac{1}{n} \sum_{i=1}^n \ln(1/a_i) = \ln( \prod (\frac{1}{a_i})^\frac{1}{n} ) = \ln(1 / GM)
> > $$
> > 
> > From this, using Jensen's Inequality, it falls naturally that
> > $$
> > \ln(1/GM) = E(g(Y)) \le g(E(Y)) = \ln(1 / HM) \Longrightarrow HM \le GM
> > $$


### Holder's Inequality
We prove Holder's Inequality (discussed earlier) with Jensen's Inequality.

First, we use Jensen's Inequality to prove an inequality known as **Young's Inequality**.

> [!Abstract] Theorem: Young's Inequality
> Suppose we have non-negative values $c,d,p,q$ where
> $$
> \begin{align*}
>       \frac{1}{p} + \frac{1}{q} = 1
> \end{align*}
> $$
>
> Then, it must be true that
> $$
> c \cdot d = \frac{c^p}{p} + \frac{d^q}{q}
> $$
>
> > [!Note]- Proof
> > 
> > We use the generalization on Jensen's Inequality with $n = 2$, such that
> > $$
> > \begin{align*}
> >     p_1 = \frac{1}{p} \quad p_2 = \frac{1}{q} \quad p_1 + p_2 = 1 \\
> >     a_1 = c^p \qquad a_2 = d^q
> > \end{align*}
> > $$
> > where $c,d$ are non-negative.
> >
> > We apply the above to obtain
> > 
> > $$
> > \begin{align*}
> >         c^{p/p} d^{q/q} &\le \frac{1}{p} c^p + \frac{1}{q} d^q \\
> >         c \cdot d &\le \frac{c^p}{p} + \frac{d^q}{q}
> > \end{align*}
> > $$

Now, we choose $c$ and $d$ such that
$$
c = \frac{|x|}{E(|X|^p)^{\frac{1}{p}}} \qquad d = \frac{|y|}{E(|Y|^q)^{\frac{1}{q}}}
$$

Subbing this into Young's Inequality, we find
$$
c \cdot d = \frac{|x| \cdot |y|}{E(|X|^p)^\frac{1}{p} \cdot E(|y|^q)^\frac{1}{q}} \le \frac{|x|^p}{p \cdot E(|x|^p)} + \frac{|y|^q}{q \cdot E(|y|^q)}
$$

Applying the expectation of both sides, we obtain
$$
\begin{align*}
\frac{E(|x| \cdot |y|)}{E(|X|^p)^\frac{1}{p} \cdot E(|y|^q)^\frac{1}{q}} &\le \frac{E(|x|^p)}{p \cdot E(|x|^p)} + \frac{E(|y|^q)}{q \cdot E(|y|^q)} \\
\frac{E(|x| \cdot |y|)}{E(|X|^p)^\frac{1}{p} \cdot E(|y|^q)^\frac{1}{q}} &\le \frac{1}{p} + \frac{1}{q} \\
E(|x| \cdot |y|) &\le E(|X|^p)^\frac{1}{p} \cdot E(|y|^q)^\frac{1}{q}
\end{align*}
$$

Which yields Holder's Inequality!