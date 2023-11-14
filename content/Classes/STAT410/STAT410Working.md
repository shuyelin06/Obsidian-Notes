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

-- end of MGF topic --


# Section 8.1: Holder and Minkowski's Inequality
In practice, we may not know the distribution.

However, sometimes, given what we have, we can still make estimations for various parameters, such as $E(X)$.

Moreover, what if we do NOT know the joint distribution, but we do know the distributions of $X$ and $Y$?

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

> [!Info] Holder's Inequality and Cauchy-Schwarz Inequality
> Let $p = 2$. Then we get
> $$
> \vert E(XY) \vert \le \left( E(\vert X \vert^2) \right)^{\frac{1}{2}} \left( E(\vert Y \vert^2) \right)^{\frac{1}{2}}
> $$
> which is known as the Cauchy-Schwarz Inequality!
>
> If $X = \vert Z \vert^r$, $1 < r < p$, and $Y = 1$, then
> $$
> \vert E(XY) \vert \le E( \vert Z \vert^r ) \le \left( E( \vert Z \vert^{rp} ) \right)^\frac{1}{p}
> $$
> Letting $s = pr$, we find
> $$
> E( \vert Z \vert^r ) \le ( E(\vert Z \vert^s) )^{\frac{r}{s}}
> $$
> Finally, raising both sides to the rth power, we find that
> $$
> E( \vert Z \vert^r )^{\frac{1}{r}} \le ( E(\vert Z \vert^s) )^{\frac{1}{s}} \qquad 1 < r < s
> $$
> Which is called **Lyapunov's Inequality**.

> [!Example]
Suppose $Z_1 = X - E(X)$, and $Z_2 = Y - E(Y)$.

By the Cauchy-Scwarz Inequality,
$$
\begin{align*}
        \vert E(z_1 z_2) \vert
        &= \vert E( (X - E(X)) (Y - E(Y)) ) \vert = \vert \text{Cov}(x,y) \vert \\
        &\le E( \vert X - E(X) \vert^2 )^\frac{1}{2} E( \vert Y - E(Y) \vert^2 )^{\frac{1}{2}} = \sqrt{ V(X) } \sqrt{ V(Y) } \\
        &\left\vert \frac{\text{Cov}(X,Y)}{\sqrt{V(X)} \sqrt{V(Y)}} \right\vert \le 1 
\end{align*}
$$

Which proves that our correlation coefficient satisfies
$$
\vert \mathcal{P}_{X,Y} \vert \le 1
$$

---

> [!Example]
Let $X \sim N(\mu_1, 1)$ and $Y \sim N(\mu_2, 1)$. Assume that we know what $E(X), V(X), E(Y), V(Y)$ are.

What is $E(XY)$?
> Note that as we do not know $f_{X,Y} (x,y)$, and we do not know if $X$ and $Y$ are independnet, we cannot calculate $E(XY)$!

We do know, however, that
$$
V(X) = E(X^2) - E(X)^2 \to E(X^2) = V(X) + E(X)^2 = 1 + E(X)^2
$$
> Standard deviation is 1, so variance is 1.

Using the Cauchy-Schwarz Inequality, we find that
$$
\begin{align*}
        \vert E(XY) \vert
              &\le E(X^2)^\frac{1}{2} E(Y^2)^\frac{1}{2} \\
              &\le (1 + E(X)^2)^\frac{1}{2} (1 + E(Y)^2)^\frac{1}{2}
\end{align*}
$$

So we can at least find an upper bound on $E(XY)$ without knowing the joint pdf!

---

> [!Abstract] Theorem: Minkowksi's Inequality
> Let $p \ge 1$.
>
> Then,
> $$
> E( \vert X + Y \vert^p)^\frac{1}{p} \le E(|X|^p)^\frac{1}{p} + E(|Y|^p)^\frac{1}{p}
> $$
>
> > [!Note] Proof
> > We know that the LHS without the $1 / p$ power is
> > $$
> > \begin{align*}
> >     E(|X+Y|^p)
> >     &= E(|X+Y| \cdot |X+Y|^{p-1}) \le E( (|X| + |Y| ) \cdot |X + Y|^{p-1} ) \\
> >     &= E(|X| \cdot |X+Y|^{p-1} + |Y| \cdot |X+Y|^{p-1} ) \\
> >     &= E(|X| \cdot |X+Y|^{p-1}) + E(|Y| \cdot |X+Y|^{p-1})
> > \end{align*}
> > $$
> >
> > We see that in both terms of the summation, we have an expected value of a product, meaning we can apply Holder's Inequality to obtain
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
> > Since $\frac{1}{p} + \frac{1}{q} = 1$, we have
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

---

> [!Example]
> Let $X,Y \sim \text{Gamma}(\alpha,\beta)$. We know that for this distribution
> $$
> V(X) = \alpha \beta^2 \qquad E(X) = (\alpha \beta)^2 \quad \to \quad E(X^2) = V(X) + E(X)^2
> $$
> 
> For $p = 2$ in Monkowski's Inequality, the left hand side would normally yield
> $$
> E(|X+Y|^2)^\frac{1}{2} = E(|X|^2 + 2|XY| + |Y|^2)
> $$
> But this requires we know the joint distribution! Instead, we can apply our inequality to at least gain an idea of what our expected value evaluates to be.
> $$
> E(|X+Y|^2)^\frac{1}{2} \le 2 (\alpha \beta^2 + (\alpha \beta)^2)^\frac{1}{2}
> $$

---

# Section 8.2: Markov and Chebyshev's Inequality

> [!Abstract] Theorem: Markov's Inequality
> Let $X$ be a random variable that takes on non-negative values. Then for any $a > 0$,
> $$
> P(X \ge a) \le \frac{E(X)}{a}
> $$
>
> > [!Note] Proof
> >
> > $$
> > \begin{align*}
> >         E(X)
> >         &= \sum_{x \ge a} x P(X = x) + \sum_{x < a} x P(X = x) \\
> >         &\ge \sum_{x \ge a} x P(X = x) + 0 \\
> >         &\ge \sum_{x \ge a} a P(X = x) = a P(X \ge a) \\
> >         \to P(X \ge a) &= \frac{E(X)}{a}
> > \end{align*}
> > $$

> [!Example] Example: Markov's Inequality
> An exam average is 75%. If we let $a = 80$, and $X$ is the random variable denoting the score on the exam, then
> $$
> P(X \ge 80) \le \frac{75}{80} \approx 0.9375
> $$
> telling us that the proportion of students scoring less than 80% can be at most 93.75%.

Not very useful in practice... if we know the distribution, why don't we just calculate the probability ourselves?

> [!Example]
> Let $X \sim \text{Binomial} (10, \frac{1}{2})$, giving us $E(X) = 5$.
> 
> If $a = 11$, we get $P(X \ge 11) \le \frac{5}{11}$, even though the probability is clearly 0.

---

> [!Abstract] Theorem: Chebyshev's Inequality
> Let $X$ be a random variable, and define
> $$
> \mu = E(X) \qquad \sigma^2 = V(X)
> $$
> where $\sigma$ is called the **standard deviation**.
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
> This establishes a bound for the proportion of values in our distribution within some number of standard deviations from the mean.
>
> > [!Note] Proof
> >
> > We have
> > $$
> > \begin{align*}
> >         \sigma^2
> >         &= V(X) = E( (X - \mu)^2 ) \\
> >         &= \int_{-\infty}^\infty (x - \mu)^2 f(x) \; dx \\
> >         &= \int_{-\infty}^{\mu - k} (x - \mu)^2 f(x) \; dx + \int_{\mu - k}{\mu + k} (x - \mu)^2 f(x) \; dx + \int_{\mu + k}^\infty (x - \mu)^2 f(x) \; dx \\
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


> [!Example]
> Let the pdf of $X$ be given as
> $$
> f(x) =
> \begin{cases}
>         630x^4 (1 - x)^4 & 0 < x < 1 \\
>         0 & \text{else}
> \end{cases}
> $$
> 
> Integrating yields the following values.
> $$
> \mu = E(X) = \frac{1}{2} \qquad \sigma = \sqrt{\frac{1}{44}} \approx 0.15
> $$
> 
> Using these values, by Chebyshev's Inequality, the probability that $X$ will take on values within 2 standard deviations of the mean is 
> $$
> P(|X - \mu| < 2\sigma) \ge 1 - \frac{1}{4}
> $$


> [!Example]
> An IQ test has mean 100, standard deviation 16. Show that the probability a person has an IQ of at least 148 or at most 52 is at most $\frac{1}{9}$.
> 
> We apply Chebyshev's theorem. Here,
> $$
> X \ge 148 \qquad X \le 52 \qquad |X-100| \ge 48
> $$
> 
> By Chebyshev's, we have
> $$
> P(|X-100| \ge 48) = \frac{16^2}{48^2}
> $$

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