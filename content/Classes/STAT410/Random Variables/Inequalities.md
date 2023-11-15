---
title: Inequalities Involving Random Variables
tags:
- stat410
- wip
---

In practice, we often do not know the probability distribution we're observing. However, we can often still make estimations for various parameters of our distributions!

# Holder's Inequality
**Holder's Inequality** establishes a relationship between the product of two random variables as follows:

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

---

#wip

# Section 8.1: Holder and Minkowski's Inequality



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