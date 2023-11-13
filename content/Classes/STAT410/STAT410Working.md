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


# Section 7.2: Moment Generating Functions (Univariate)
Let $X$ be a random variable. The **$r^{th}$ moment of $X$ about the origin** is
$$
\mu_r' = E(X^r) = \begin{cases}
              \sum_x x^r f(x) & \text{Discrete Case} \\
              \int_{-\infty}^\infty x^r f(x) dx & \text{Continuous Case}
       \end{cases}
$$
for any non-negative integer $r$.
> Clearly, $\mu_1' = E(X)$.

Furthermore, the **$r^{th}$ moment around the mean $\mu$** is defined as
$$
\mu_r = E( (x - \mu)^r ) = \begin{cases}
           \sum_x (x - \mu)^r f(x) & \text{Discrete Case} \\
           \int_{-\infty}^\infty (x - \mu)^r f(x) dx & \text{Continuous Case}
        \end{cases}
$$
> Clearly, $\mu_2 = E( (x - \mu)^2 ) = V(X)$.

The **moment generating function (mgf)** of random variable $X$ is
$$
M_x (t) = E(e^{tx}) = \begin{cases}
            \sum_x e^{tx} f(x) & \text{Discrete Case} \\
            \int_{-\infty}^\infty e^{tx} f(x) dx & \text{Continuous Case}
        \end{cases}
$$

Expanding $e^{tx}$ as a series, we find that
$$
\begin{align*}
        e^{tx} = 1 + tx + \frac{(tx)^2}{2!} + \frac{(tx)^3}{3!} + \dots \\
        \to \sum_x e^{tx} f(x) = M_x (t) = \sum_x \left(1 + tx + \frac{t^2 x^2}{2!} + \frac{t^3 x^3}{3!} \right) f(x) \\
            = \sum_x f(x) + t \sum_x x f(x) + \frac{t^2}{2!} \sum_x x^2 f(x) + \dots \\
            = 1 + t u_1' + \frac{t^2}{2!} u_2' + \frac{t^3}{3!} u_3' \dots \frac{t^r}{r!} u_r'
\end{align*}
$$

Thus, the coefficient of $\frac{t^n}{n!}$ is simply $u_n'$, the $n^{th}$ moment! We can use this fact to find the moments.

With
$$
M_x (t) = \sum_{n=0}^\infty u_n' \frac{t^n}{n!}
$$
we can find $u_n'$ by taking the $n^{th}$ derivative and subbing in $t = 0$.

> [!Abstract] Theorem
> $$
> M_x^(n) (0) = \frac{d^n}{dt^n} (M_x (t)) \bigg\vert_{t=0} = u_n'
> $$

> [!Example]
> $$
> f(x) = \begin{cases}
>        e^{-x} & x > 0 \\
>        0 & \text{else}
>      \end{cases}
> $$
>
> Find the mgf of $f(x)$, and a simple expression for $u_r'$.
>
> $$
> \begin{align*}
> M_x (t) = E(e^{tx}) &= \int_0^\infty e^{tx} e^{-x} dx \\
>     &= \int_0^\infty e^{-x (1 - t)} dx \\
>     &= \frac{1}{1 - t}
> \end{align*}
> $$
>
> We can now expand this as a series to find the coefficient of $x^r / r!$.
> $$
> 1 + t + t^2 + t^3 + \dots = 1 + \frac{1}{1!} t + \frac{2!}{2!} t^2 + \dots
> $$
> We find the rth moment as $\mu_r' = r!$.
>
> Alternatively, we can differentiate $M_x (t)$ $r$ times to find $\mu_r'$.
>
> $$
> \begin{align*}
>       M_x'(t) &= \frac{1}{(1 - t)^2} \\
>       M_x''(t) &= \frac{2}{(1 - t)^3} \\
>       &\vdots \\
>       M_x^r (t) &= \frac{(2)(3)(4) \dots (r)}{(1 - t)^{r + 1}} \\
>       M_x^n (0) &= \frac{(2)(3)(4) \dots (n)}{(1 - 0)^{n + 1}} = n!
> \end{align*}
> $$

> [!Example]
> Let $X$ have pmf given by
> $$
> f(x) = \begin{cases}
>        \frac{1}{8} \binom{3}{x} & x = 0,1,2,3 \\
>        0 & \text{else}
>      \end{cases}
> $$
> Find the moment generating function of $X$, and determine the second moment about the origin.
> 
> $$
> \begin{align*}
>         M_x(t) = E(e^{tx}) &= \frac{1}{8} \sum_{x=0}^3 e^{tx} \binom{3}{x} \\
>                &= \frac{1}{8} ( 1 + 3e^t + 3e^{2t} + e^{3t} ) \\
> \end{align*}
> $$
> 
> Given $M_x(t)$, we can easily find the second moment about the origin by differentiating twice.
> $$
> M_x''(0) = \frac{1}{8} ( 3 + 12 + 9 ) = 3
> $$

Below, we provide the moment generating functions for discrete distributions.

| Distribution | Moment Generating Function |
| :-: | :-: |
| Uniform | $\frac{e^t}{n} \left( \frac{1 - e^{tn}}{1 - e^t} \right)$  |
| Binomial | $\left( pe^t + (1-p) \right)^n$ |
| Geometric | $p \frac{1}{1 - (1-p) e^t}$ |
| Negative Binomial | $\frac{(pe^t)^r}{(1 - (1-p)e^t)^r}$ |
| Poisson | $e^{\lambda (e^t - 1)}$ |

> [!Note]- Uniform Distribution: Derivation for MGF
> $$
> \begin{align*}
>       M_x(t) = E(e^{tx})
>              &= \sum_{x=1}^n e^{tx} \frac{1}{n} \\
>              &= \sum_{x=0}^{n-1} e^{t(x+1)} \frac{1}{n} \\
>              &= \frac{e^t}{n} \sum_{x=0}^{n-1} (e^t)^x &\text{Ratio Sum} \\
>              &= \frac{e^t}{n} \left( \frac{1 - e^{tn}}{1 - e^t} \right) 
> \end{align*}
> $$

> [!Note]- Binomial Distribution: Derivation for MGF
> $$
> \begin{align*}
>         M_x(t) = E(e^{tx})
>                &= \sum_{x=0}^n e^{tx} \binom{n}{x} p^x (1 - p)^{n-x} \\
>                &= \sum_{x=0}^n \binom{n}{x} (pe^t)^x (1-p)^{n-x} &\text{Binomial Theorem} \\
>                &= \left( pe^t + (1-p) \right)^n
> \end{align*}
> $$

> [!Note]- Geometric Distribution: Derivation for MGF
> $$
> \begin{align*}
>         M_x(t) = E(e^{tx})
>                &= \sum_{x=0}^\infty e^{tx} (1-p)^x p \\
>                &= p \sum_{x=0}^\infty \left( (1-p) e^t \right)^x &\text{Ratio Sum} \\
>                &= p \frac{1}{1 - (1-p) e^t} &t < - \ln (1 - p)
> \end{align*}
> $$
>
> The derivation for negative binomial follows similarly.

> [!Note]- Poisson Distribution: Derivation for MGF
> $$
> \begin{align*}
>         M_x(t) = E(e^{tx})
>                &= \sum_{x=0}^\infty e^{tx} \frac{\lambda^x e^{-\lambda}}{x!} \\
>                &= \sum_{x=0}^\infty \frac{(e^t \lambda)^x e^{\lambda}}{x!} \\
>                &= e^{-\lambda} (e^{e^t \lambda}) = e^{\lambda (e^t - 1)}
> \end{align*}
> $$

Observe how we can use the moment generating functions to find the expected value and variances of distributions.
$$
M_x'(0) = E(X) \qquad M_x''(0) = E(X^2) \qquad V(X) = (M_x'(0))^2 - M_x''(0)
$$

> [!Info] Remark
> If $Y = aX + b$, then
> $$
> M_Y (t) = e^{bt} M_X (at)
> $$

> [!Note] Uniform Distribution (Continuous): Derivation for MGF
> $$
> \begin{align*}
>         M_x(t) = E(e^{tx})
>                &= \int_\alpha^\beta e^{tx} \frac{1}{\beta - \alpha} dx \\
>                &= \frac{1}{t(\beta - \alpha)} (e^{\beta t} - e^{\alpha t})
> \end{align*}
> $$

> [!Note] Normal Distribution: Derivation for MGF
> Suppose we know if $Z \sim N(0,1)$, and $X = \mu + \sigma Z$, then $X \sim N(\mu, \sigma^2)$.
>
> First, we find our mgf for $Z$.
> $$
> \begin{align*}
>       M_Z(t) = E(e^{tz})
>              &= \int_{-\infty}^\infty \frac{1}{\sqrt{2\pi}} e^{tx} e^{-x^2 / 2} dx \\
>              &= \frac{1}{\sqrt{2\pi}} \int_{-\infty}^\infty e^{tx - x^2 / 2} dx \\
>              &= \frac{1}{\sqrt{2\pi}} \int_{-\infty}^\infty e^{(2tx - x^2)/2} dx \\
>              &= \frac{1}{\sqrt{2\pi}} \int_{-\infty}^\infty e^{t^2/2 - (x-t)^2 / 2} dx &\text{Complete the Square} \\
>              &= e^{t^2/2} \frac{1}{\sqrt{2\pi}} \int_{-\infty}^\infty e^{- (x-t)^2 / 2} dx \\
>              &= e^{t^2 / 2} & \text{PDF for } N(\mu = t, \sigma^2 = 1)
> \end{align*}
> $$
>
> Using this fact, and knowing that $X = \mu + \sigma Z$, we apply our previous remark to find that the moment generating function of $X$ is
> $$
> M_X(t) = e^{\mu t} M_Z(\sigma t) = e^{\mu t} e^{(\sigma t)^2 / 2}
> $$

> [!Note] Gamma Distribution: Derivation for MGF
> $$
> \begin{align*}
>       M_x(t) &= \int_0^\infty e^{tx} f(x) dx \\
>              &= \int_0^\infty \frac{\beta^\alpha x^{\alpha - 1}}{\Gamma(\alpha)} e^{- (\beta - t) x} dx \\
>              &= \frac{\beta^\alpha}{\Gamma(\alpha) (\beta - t)} \int_0^\infty \left( \frac{u}{\beta - t} \right)^{\alpha - 1} e^{-u} du \\
>              &= \frac{\beta^\alpha}{\Gamma(\alpha) (\beta - t)} \int_0^\infty u^{\alpha - 1} e^{-u} du \\
>              &= \frac{\beta^\alpha}{\Gamma(\alpha) (\beta - t)} \Gamma(\alpha) \\
>              &= \left( \frac{\beta}{\beta - t} \right)^\alpha \\
>              &= \left( 1 - \frac{t}{\beta} \right)^{-\alpha}
> \end{align*}
> $$

# Section 7.3: Sum of Random Variables and Moment Generating Functions (Multivariate)
Let $X_1, \dots, X_n$ be random variables and defined the vectors $\vec{X} = (X_1, \dots, X_n)$ and $\vec{t} = (t_1, \dots, t_n)$. Then, the function
$$
M (t_1, \dots, t_n) = M (\vec{t}) = E(e^{t_1 X_1 + \dots t_n X_n}) = E(e^{\vec{t} \cdot \vec{X}})
$$
is the **joint moment generating function** fof $X_1 \dots X_n$.

> [!Info]
> Let $\vec{a} = (a_1, \dots, a_n)$ and $\vec{b} = (b_1, \dots, b_n)$. Then, if $\vec{Y} = \vec{a} \cdot \vec{X} + \vec{b}$, then
> $$
> M_Y (\vec{t}) = e^{\vec{t} \cdot \vec{b}} M_x(\vec{a} \cdot \vec{t})
> $$

Note that $M(0,\dots, 0, t_i, 0, \dots, 0) = E(e{t_i X_i}) = M_{X_i} (t_i)$.

> [!Abstract] Theorem
> 1. Uniqueness: Random variable $X$ and $Y$ have the same distribution if and only if $M_X(t) = M_Y(t)$.
>
> 2. If $X_1 \dots X_n$ are independent, then the joint mgf is given as
> $$
> M(\vec{t}) = \prod_{i=1}^n M_{x_i} (t_i)
> $$
>
> 3.
> $$
> \frac{\partial^2}{\partial t_i \partial t_j} M(\vec{t}) \bigg\vert_{t_1=\dots=t_n=0} = E(X_i X_j)
> $$
>
> > Note that from (2) (assuming independence), if we look at the univariate case, say
> > $$
> > Z = X + Y
> > $$
> > Then
> > $M_Z (t) = E(e^{tz}) = E(e^{t(X+Y)})$
> >
> > So, if RV are independent, then our MGF of the sum of random variables is the product of the MGFs.

> [!Example]
> Suppose $X$ and $Y \sim U(-1,1)$.
>
> From earlier, we find
> $$
> M_X(t) =\frac{1}{2t} (e^t - e^{-t})
> $$
>
> So,
> $$
> M_{X+Y} (t) = \left( \frac{e^t - e^{-t}}{2t} \right)^2
> $$

> [!Example]
> Let $X_1, \dots X_n$ be independent, and assume $X_i \sim \text{Gamma}(\alpha_i, \beta)$. We showed earlier that
> $$
> M_{X_i} (t) = \left( 1 - \frac{t}{\beta} \right)^{-\alpha_i}
> $$
> 
> To obtain the mgf of $Y = \sum_{i=1}^n X_i$ (assuming our distributions are independent), we get
> $$
> \begin{align*}
>         M_Y (t) &= \prod_{i=1}^n M_{X_i} (t) \\
>                 &= \prod_{i=1}^n \left( 1 - \frac{t}{\beta} \right)^{-\alpha_i} \\
>                 &= \left( 1 - \frac{t}{\beta} \right)^{-(\alpha_1 + \alpha_2 + \dots + \alpha_n)}
> \end{align*}
> $$
>
> Thus, we've shown that the sum of the independent Gamma random variable stays Gamma, provided that $\beta$ is the same for all random variables.

> [!Example]
> Let
> $$
> f_{x,y} (x,y) = \begin{cases}
>                 e^{-y} & 0 < x < y < \infty \\
>                 0 & \text{else}
>         \end{cases}
> $$
> be a joint pdf. Find the joint mgf.
> 
> We find our joint mgf by applying our definition. 
> $$
> \begin{align*}
>         M_{X,Y} (s,t) = E(e^{sX + tY})
>                 &= \int_0^\infty \int_x^\infty e^{sx + ty} \cdot e^{-y} dy dx \\
>                 &= \int_0^\infty \int_x^\infty e^{sx} e^{y(t-1)} dy dx & \text{Assume} \; t < 1 \\
>                 &= \int_0^\infty \frac{1}{t-1} \left( -e^{sx} e^{x (t-1)} \right) dx \\
>                 &= \int_0^\infty \frac{1}{t-1} \left( -e^{x (s+t-1)} \right) dx & \text{Assume} \; s+t < 1 \\
>                 &= \frac{1}{t-1} \frac{1}{s + t - 1} & s + t < 1, t < 1
> \end{align*}
> $$
> 
> Note how we have to choose the bounds of $s$ and $t$ so that our integral can evaluate. Outside of these bounds, our integral (and thus mgf) would be undefined.
>
> Furthermore, we can find $M_X (s)$ and $M_X (t)$ by setting $t = 0$ and $s = 0$, respectively.
> $$
> M_X (s) = \frac{1}{1-s} \qquad M_Y (t) = \frac{1}{(t-1)^2}
> $$

> [!Example]
> Let
> $$
> f(x,y) = \begin{cases}
>          \frac{1}{x!(y-x)!} & y = 0, 1, \dots \quad x = 0, 1, \dots, y \\
>          0 & \text{else}
>        \end{cases}
> $$
> be a joint pmf. Find the joint mgf of $X,Y$.
> 
> We find the joint mgf by applying our definition.
> $$
> \begin{align*}
>         M_{X,Y} (s,t) = E(e^{sX + tY})
>                 &= \sum_{y=0}^\infty \sum_{x=0}^y e^{sx+ty}  \frac{1}{x!(y-x)!} \\
>                 &= \sum_{y=0}^\infty e^{ty} \sum_{x=0}^y e^{sx} \frac{1}{x!(y-x)!} \\
>                 &= \sum_{y=0}^\infty \frac{e^{ty}}{y!} \sum_{x=0}^y \frac{y!}{x! (y-x)!} e^{sx} \\
>                 &= \sum_{y=0}^\infty \frac{e^{ty}}{y!} \sum_{x=0}^y \binom{y}{x} \left( e^s \right)^x 1^{y-x} & \text{Binomial Theorem} \\
>                 &= \sum_{y=0}^\infty \frac{e^{ty}}{y!} (e^s + 1)^y \\
>                 &= \sum_{y=0}^\infty \frac{(e^t \cdot (e^s + 1))^y}{y!} & \text{Exponential Series} \\
>                 &= \exp ( e^t (1 + e^s) )
> \end{align*}
> $$

-- end of MGF topic --

# Section 7.4: Conditional Expectation
If $X$ is a random variable, the **conditional expectation** of $g(x)$ given $Y = y$ is
$$
E( g(x) \mid y ) = \sum_x g(x) f(x \mid y)
$$
in the discrete case, and
$$
E( g(x) \mid y ) = \int_{-\infty}^\infty g(x) f(x \mid y) dx
$$
in the continuous case.

In particular, if $g(x) = x^i$, the **conditional $i^{th}$ moment is given as $E(X_i \mid Y = y)$.
1. $E(X \mid Y = y)$ is the **conditional mean**.
2. $V(X \mid Y = y) = E(X^2 \mid Y = y) - (E(X \mid Y = y))^2$ is the **conditional variance**.

> [!Abstract]
> We have
> 1. $E(X^i) = E( E(X^i \mid Y = y) )$
> 2. $V(X) = V(E(X \mid Y)) + E(V(X \mid Y))$
>
>

> [!Note] Proof (1)
First, we find that
$$
\begin{align*}
        E(X^i \mid Y = y)
        &= \int_{-\infty}^\infty x^i f(x \mid y) dx \\
        &= \int_{-\infty}^\infty x^i \frac{f(x,y)}{g_Y(y)} dx = h(Y)
\end{align*}
$$
where $h(Y)$ is some function on $Y$. We can then use this to obtain
$$
\begin{align*}
        E(X^i) = E( h(Y) )
        &= \int_{-\infty}^\infty h(y) g_Y (y) dy \\
        &= \int_{-\infty}^\infty \left[ \int_{-\infty}^\infty x^i \frac{f(x,y)}{g_Y(y)} dx \right] g_Y (y) dy \\
        &= \int_{-\infty}^\infty \left[ \int_{-\infty}^\infty x^i f(x,y) dx \right] dy \\
        &= \int_{-\infty}^\infty \int_{-\infty}^\infty x^i g_X(x) f(y \mid x) dx dy \\
        &= \int_{-\infty}^\infty \int_{-\infty}^\infty x^i g_X(x) f(y \mid x) dy dx \\
        &= \int_{-\infty}^\infty x^i g_X(x) \left[ \int_{-\infty}^\infty f(y \mid x) dy \right] dx \\
        &= \int_{-\infty}^\infty x^i g_X(x) (1) dx = E(X^i)
\end{align*}
$$

> [!Note] Proof (2)
> Taking the right-hand side expression, we find
> $$
> \begin{align*}
>         V(E (X \mid Y)) + E(V(X \mid Y))
>             &= E( E(X \mid Y)^2  - E ( E(X \mid Y) ))^2 + E(E(X^2 \mid Y) - (E(X \mid Y))^2) \\
>             &= E( E(X \mid Y)^2 ) - [ E(X) ]^2 + E( E(X^2 \mid Y)) - E (E (X \mid Y) )^2 \\
>             &= E(X^2) - (E(X))^2 = V(X)
> \end{align*}
> $$

> [!Example]
Suppose
$$
P(y = 1) = \frac{1}{8} \qquad P(y = 2) = \frac{7}{8}
$$

Let $Z = X \mid Y$, and define
$$
P(z = 2y) = \frac{3}{4} \qquad P(z = 3y) = \frac{1}{4}
$$

If $y = 1$, then
$$
X \mid (Y = 1) =
  \begin{cases}
        2 & P = \frac{3}{4} \\
        3 & P = \frac{1}{4}
  \end{cases}
$$

This can give us expected value
$$
E(X \mid Y = 1) = 2 \frac{3}{4} + 3 \frac{1}{4} = \frac{9}{4}
$$
Similarly,
$$
E(X \mid Y = 2) = 4 \frac{3}{4} + 6 \frac{1}{4} = \frac{18}{4}
$$

Giving us
$$
E(X \mid Y) =
    \begin{cases}
        \frac{9}{4} & y = 1 \\
        \frac{18}{4} & y = 2
    \end{cases}
$$
Thus, with this, we can even find $E (E(X \mid Y))$, giving us the expectation with respect to various values $Y$.
$$
E(E (X \mid Y)) = \frac{9}{4} P(y = 1) + \frac{18}{4} \frac{7}{8} = \frac{9}{4} \cdot \frac{1}{8} + \frac{18}{4} \cdot \frac{7}{8}
$$

---

> [!Abstract] Theorem: Law of Total Expectation
> We have
> $$
> E(X) = E( E(X \mid Y) ) = \sum_y E(X \mid Y = y) P(Y = y)
> $$
>
> We can generalize this fact further. If $A_1, \dots A_n$ partition the sample space, then
> $$
> E(X) = \sum_{i=1}^n E(X \mid A_i) P(A_i)
> $$

> [!Example]
> Let
> $$
> f_{X,Y} (x,y) =
>         \begin{cases}
>                 x^2 e^{-x (y + 1)} & x,y > 0 \\
>                 0 & \text{else}
>         \end{cases}
> $$
> Find $E(X \mid Y)$.
> 
> We can do this by finding
> $$
> \begin{align*}
>         E(X \mid Y)
>             &= \int_{-\infty}^\infty x f(x \mid y) dx \\
>             &= \int_0^\infty x x \left( \frac{x^2 e^{-x (y+1)}}{g_Y (y)} \right) \\
>             &= \int_0^\infty \frac{1}{2} (y + 1)^3 x^3 e^{-x (y + 1)} dx
> \end{align*}
> $$
> Given that
> $$
> g_Y (y) = \frac{2}{(y + 1)^3}
> $$
> 
> Let $u = x (y + 1) \to du = y + 1$. We find
> $$
> E(X \mid Y) = \frac{1}{2 (y+1)} \int_0^\infty u^3 e^{-u} du = \frac{1}{2(y+1)} \Gamma(4) = \frac{3!}{2(y+1)}
> $$

---

> [!Example]
> A man is stuck in a cave. There are 3 tunnel exits:
> 1. Tunnel 1 takes 2 hours to get out.
> 2. Tunnel 2 takes 5 hours, but returns to the starting point.
> 3. Tunnel 3 takes 7 hours, but returns to the starting point.
> 
> If he picks a tunnel at random each time, what is the expected time until he gets out?
> 
> Let $X$ be the total hours to get out, and $Y$ be the tunnel he enters initially. We want
> $$
> \begin{align*}
>         E(X)
>         &= \sum_{y=1}^3 E(X \mid Y = y) P(Y = y) \\
>         &= E(X \mid Y = 1) P(Y = 1) + P(X \mid Y = 2) P(Y = 2) + P(X \mid Y = 3) P(Y = 3) \\
>         &= 2 \frac{1}{3} + (5 + E(X)) \frac{1}{3} + (7 + E(X)) \frac{1}{3} 
> \end{align*}
> $$
> Solving for $E(X)$, we find $E(X) = 14$. Note that we express $E(X)$ recursively in terms of itself, as if the man enters tunnel 2 or 3, he ends up back where he started but with additional time spent.

> [!Example]
> A biased coin has $P(\text{Heads}) = p$. We toss the coin until we get 2 consecutive heads. What is the number of expected tosses?
> 
> Let:
> 1. $A_1$ be the event of the sequence $H,H$.
> 2. $A_2$ be the event of the sequence $H,T$.
> 3. $A_3$ be the event of the sequence of just $T$.
> 
> As $A_1, A_2, A_3$ partition the sample space of the toss sequences, we can find our expected value by breaking it up across these different sequences. Define $X$ as the total number of tosses needed until we get 2 consecutive heads. Then,
> $$
> \begin{align*}
>         E(X)
>         &= E(X \mid A_1) P(A_1) + E(X \mid A_2) P(A_2) + E(X \mid A_3) P(A_3) \\
>         &= 2 p^2 + (2 + E(X)) p (1 - p) + (1 + E(X)) (1 - p)
> \end{align*}
> $$
>
> Solving for $E(X)$, we find $E(X) = \frac{p+1}{p^2}$.

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