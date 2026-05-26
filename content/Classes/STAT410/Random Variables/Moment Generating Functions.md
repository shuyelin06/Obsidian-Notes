---
title: Moment Generating Functions
tags:
- stat410
---

Now that we have an understanding of random variables, let's explore one of their properties, their **moment**!

# Univariate Case
## Moments and Moment Generating Functions
Let $X$ be a random variable. Then, for all positive $r$, the **$r^{th}$ moment of $X$ about the origin**, denoted $\mu_r'$, is given as
$$
\mu_r' = E(X^r) = \begin{cases}
              \sum_x x^r f(x) & \text{Discrete Case} \\
              \int_{-\infty}^\infty x^r f(x) dx & \text{Continuous Case}
       \end{cases}
$$

Furthermore, the **$r^{th}$ moment around the mean ($\mu$)**, denoted $\mu_r$, is given as 
$$
\mu_r = E( (x - \mu)^r ) = \begin{cases}
           \sum_x (x - \mu)^r f(x) & \text{Discrete Case} \\
           \int_{-\infty}^\infty (x - \mu)^r f(x) dx & \text{Continuous Case}
        \end{cases}
$$

> [!Info] Remark: Expected Value and Variance
> Notice that on $r = 1$, the first moment about the origin is the random variable's expected value
> $$
> \mu_1' = E(X)
> $$
>
> And on $r = 2$, the second moment about the mean is the random variable's variance
> $$
> \mu_2 = E( (x - \mu)^2 ) = V(X)
> $$

We can define a function which will let us easily find these moments! Given a random variable $X$, the **moment generating function (mgf)** is given as
$$
M_x (t) = E(e^{tx}) = \begin{cases}
            \sum_x e^{tx} f(x) & \text{Discrete Case} \\
            \int_{-\infty}^\infty e^{tx} f(x) dx & \text{Continuous Case}
        \end{cases}
$$

How does this let us find our moments?

In our expected value calculation, if we expand $e^{tx}$ as the infinite series
$$
e^{tx} = 1 + tx + \frac{(tx)^2}{2!} + \frac{(tx)^3}{3!} + \dots
$$

We find that
$$
\begin{align*}
        M_x (t) &= E(e^{tx}) \\
        &= \sum_x e^{tx} f(x) \\
        &= \sum_x \left(1 + tx + \frac{t^2 x^2}{2!} + \frac{t^3 x^3}{3!} + \dots \right) f(x) \\
        &= \sum_x f(x) + t \sum_x x f(x) + \frac{t^2}{2!} \sum_x x^2 f(x) + \dots \\
        &= 1 + t u_1' + \frac{t^2}{2!} u_2' + \frac{t^3}{3!} u_3' \dots \frac{t^r}{r!} u_r'
\end{align*}
$$

Thus, in our infinite series, the coefficient of term $\frac{t^n}{n!}$ is the value of the $n^{th}$ moment $u_n'$!

Using this fact, if we let $t = 0$, we can easily find $\mu_n'$ by taking the $n^{th}$ derivative of $M_x(t)$! This is reflected in the following theorem

> [!Abstract] Theorem: Moment Generating Function and Moments
> Given random variable $X$, and its moment generating function $M_x(T)$, we can find the $n^{th}$ moment of $X$ by taking
> $$
> \mu_n' = M_x^n (0) = \frac{d^n}{dt^n} M_x (t) \bigg\vert_{t=0}
> $$

> [!Info] Remark
> If $Y = aX + b$, then
> $$
> M_Y (t) = e^{bt} M_X (at)
> $$

Furthermore, moment generating functions are unique to random variable distributions! This is known as the **uniqueness theorem**.

> [!Abstract] Theorem: Uniqueness of Moment Generating Functions
> Let $X$ and $Y$ be random variables. Then, $X$ and $Y$ have the same distribution if and only if their moment generating functions are the same.
> $$
> M_X (t) = M_Y (t)
> $$
> Thus, we can think of moment generating functions as unique "signatures" for random variables!

See the following examples.

> [!Example]+ Example: Moments and Moment Generating Functions
> Consider random variable $X$ with pdf given as 
> $$
> f(x) = \begin{cases}
>        e^{-x} & x > 0 \\
>        0 & \text{else}
>      \end{cases}
> $$
>
> Find the moment generating function (mgf) of $f(x)$, and use it to derive a simple expression for the $r^{th}$ moment, $u_r'$.
>
> We find the mgf of $X$ by finding the expected value of $e^{tx}$ (by definition of moment generating functions).
> $$
> \begin{align*}
>       M_x (t) = E(e^{tx})
>       &= \int_0^\infty e^{tx} e^{-x} dx \\
>       &= \int_0^\infty e^{-x (1 - t)} dx \\
>       &= -\frac{1}{1-t} e^{-x (1-t)} \bigg\vert_0^\infty \\
>       &= \frac{1}{1-t}
> \end{align*}
> $$
>
> We can now expand this as a series to find the coefficient of $\frac{x^r}{r!}$.
> $$
> \begin{align*}
>       \frac{1}{1-t}
>       &= 1 + t + t^2 + t^3 + \dots \\
>       &= 1 + \frac{1}{1!} t + \frac{2!}{2!} t^2 + \dots
> \end{align*}
> $$
> We find the rth moment as $\mu_r' = r!$.

> [!Example]- Example: Moments and Moment Generating Functions (2)
> Suppose we have random variable $X$ with pmf given by
> $$
> f(x) = \begin{cases}
>        \frac{1}{8} \binom{3}{x} & x = 0,1,2,3 \\
>        0 & \text{else}
>      \end{cases}
> $$
> Find the moment generating function of $X$, and determine the second moment about the origin.
>
> We first find the moment generating function of $X$, by finding the expected value of $e^{tx}$.
> $$
> \begin{align*}
>         M_x(t) = E(e^{tx})
>         &= \frac{1}{8} \sum_{x=0}^3 e^{tx} \binom{3}{x} \\
>         &= \frac{1}{8} ( 1 + 3e^t + 3e^{2t} + e^{3t} ) \\
> \end{align*}
> $$
> 
> Now with $M_x(t)$, we can easily find the second moment by differentiating twice and setting $t = 0$.
> $$
> M_x''(0) = \frac{1}{8} ( 3 + 3 (2) (2) + 3 (3) ) = 3
> $$

## Common Moment Generating Functions (Discrete Case)
Below, we provide the moment generating functions for common discrete distributions. 

$$
\begin{align*}
        &\frac{e^t}{n} \left( \frac{1 - e^{tn}}{1 - e^t} \right) &\text{Uniform} \\
        &\left( pe^t + (1-p) \right)^n &\text{Binomial} \\
        &\frac{p}{1 - (1-p) e^t} &\text{Geometric} \\
        &\frac{(pe^t)^r}{(1 - (1-p)e^t)^r} &\text{Negative Binomial} \\
        &e^{\lambda (e^t - 1)} &\text{Poisson}
\end{align*}
$$

Derivations for the moment generating functions are given below. Note that some derivations are ommitted, due to their complexity.

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


## Common Moment Generating Functions (Continuous Case)
Below, we provide the moment generating functions for common continuous distributions.

$$
\begin{align*}
        &\frac{e^{\beta t} - e^{\alpha t}}{t (\beta - \alpha)} &\text{Uniform} \\
        &e^{\mu t} e^{\frac{(\sigma t)^2}{2}} &\text{Normal} \\
        &\left( 1 - \frac{t}{\beta} \right)^{-\alpha} &\text{Gamma}
\end{align*}
$$

> [!Note]- Uniform Distribution (Continuous): Derivation for MGF
> $$
> \begin{align*}
>         M_x(t) = E(e^{tx})
>                &= \int_\alpha^\beta e^{tx} \frac{1}{\beta - \alpha} dx \\
>                &= \frac{1}{t(\beta - \alpha)} (e^{\beta t} - e^{\alpha t})
> \end{align*}
> $$

> [!Note]- Normal Distribution: Derivation for MGF
> Suppose we have a random variable $X \sim N(\mu, \sigma^2)$. To find its moment generating function, we will first find the moment generating function of the standardized normal distribution.
> 
> Suppose we have standard normal distribution $Z \sim N(0,1)$. We find its moment generating function as
> $$
> \begin{align*}
>       M_Z(t) &= E(e^{tz}) \\
>              &= \int_{-\infty}^\infty \frac{1}{\sqrt{2\pi}} e^{tx} e^{\frac{-x^2}{2}} dx \\
>              &= \frac{1}{\sqrt{2\pi}} \int_{-\infty}^\infty e^{tx - \frac{x^2}{2}} dx \\
>              &= \frac{1}{\sqrt{2\pi}} \int_{-\infty}^\infty e^{\frac{2tx - x^2}{2}} dx \\
>              &= \frac{1}{\sqrt{2\pi}} \int_{-\infty}^\infty e^{\frac{t^2}{2} -\frac{(x-t)^2}{2}} dx &\text{Complete the Square} \\
>              &= e^{\frac{t^2}{2}} \frac{1}{\sqrt{2\pi}} \int_{-\infty}^\infty e^{\frac{-(x-t)^2}{2}} dx &\text{PDF Verification on} \; N(\mu = t, \sigma^2 = 1) \\
>              &= e^{\frac{t^2}{2}} (1)
> \end{align*}
> $$
>
> Using this moment generating function, and knowing that we can represent $X$ in terms of the standard normal distribution as $X = \mu + \sigma Z$, we transform our moment generating function (see remark in first section) as
> $$
> M_X(t) = e^{\mu t} M_Z(\sigma t) = e^{\mu t} e^{\frac{(\sigma t)^2}{2}}
> $$

> [!Note]- Gamma Distribution: Derivation for MGF
> $$
> \begin{align*}
>       M_x(t) &= \int_0^\infty e^{tx} f(x) dx \\
>              &= \int_0^\infty \frac{\beta^\alpha x^{\alpha - 1}}{\Gamma(\alpha)} e^{- (\beta - t) x} dx
> \end{align*}
> $$
>
> We apply change of variables $u = (\beta - t) x$. Note that by this change of variables, $dx = \frac{du}{\beta - t}$.
> $$
> \begin{align*}
>              &= \frac{\beta^\alpha}{\Gamma(\alpha) (\beta - t)} \int_0^\infty \left( \frac{u}{\beta - t} \right)^{\alpha - 1} e^{-u} du \\
>              &= \frac{\beta^\alpha}{\Gamma(\alpha) (\beta - t)^\alpha} \int_0^\infty u^{\alpha - 1} e^{-u} du \\
>              &= \frac{\beta^\alpha}{\Gamma(\alpha) (\beta - t)^\alpha} ( \Gamma(\alpha) ) \\
>              &= \left( \frac{\beta}{\beta - t} \right)^\alpha \\
>              &= \left( 1 - \frac{t}{\beta} \right)^{-\alpha}
> \end{align*}
> $$


# Multivariate Case
## Sum of Random Variables and Moment Generating Functions
Let $X_1, \dots, X_n$ be random variables. Define the vectors $\vec{X} = (X_1, \dots, X_n)$ and $\vec{t} = (t_1, \dots, t_n)$.

Then, the **joint moment generating function** of $X_1, \dots X_n$ is given as
$$
M (t_1, \dots, t_n) = M (\vec{t}) = E(e^{t_1 X_1 + \dots t_n X_n}) = E(e^{\vec{t} \cdot \vec{X}})
$$
> Note that the $t$'s for each of the moment generating functions are distinct!

Note that if we let all $t$'s be 0 apart from a single $t_i$, we get our moment generating function for $X_i$!
$$
M(0,\dots, 0, t_i, 0, \dots, 0) = E(e{t_i X_i}) = M_{X_i} (t_i)
$$

> [!Info] Remark
> Let $\vec{a} = (a_1, \dots, a_n)$ and $\vec{b} = (b_1, \dots, b_n)$. Similar to the univariate case, if $\vec{Y} = \vec{a} \cdot \vec{X} + \vec{b}$, then
> $$
> M_Y (\vec{t}) = e^{\vec{t} \cdot \vec{b}} M_x(\vec{a} \cdot \vec{t})
> $$

While the joint moment generating function can be extremely difficult (and annoying) to calculate, we can easily find it if the random variables are independent. This is expressed in the following theorem:

> [!Abstract] Theorem: Independence and Joint MGFs
> Suppose we have random variables $X_1, \dots X_n$.
>
> If $X_1, \dots X_n$ are independent, then the joint mgf is given as the product of each random variable's moment generating function.
> $$
> M(\vec{t}) = \prod_{i=1}^n M_{x_i} (t_i)
> $$
>
> Furthermore, if $X_1, \dots X_n$ are independent, if we let all $t_1 = \dots = t_n = 0$, we can differentiate our joint mgf twice to find the expected value of random variable products.
> $$
> E(X_i X_j) = \frac{\partial^2}{\partial t_i \partial t_j} M(\vec{t}) \bigg\vert_{t_1=\dots=t_n=0}
> $$
>
> > [!Info] Remark
> > 
> > Note that if we have random variable $Z = X + Y$ where $X$ and $Y$ are independent, then
> > $M_Z (t) = E(e^{tz}) = E(e^{t(X+Y)})$
> >
> > And thus, applying our theorem, we can find $M_Z (t)$ as the product of the moment generating functions of $X$ and $Y$!
> > $$
> > M_Z (t) = M_X (t) \cdot M_Y (t)
> > $$

Consider the following examples.

> [!Example]+ Example: Joint Moment Generating Functions
> Suppose $X, Y \sim \text{Uniform} (-1,1)$.
>
> From our earlier derivation, we know that the moment generating function of $X$ and $Y$ is
> $$
> M_X(t) =\frac{1}{2t} (e^t - e^{-t})
> $$
>
> So, assuming $X$ and $Y$ are independent, we can find the moment generating of their sum as
> $$
> M_{X+Y} (t) = \left( \frac{e^t - e^{-t}}{2t} \right)^2
> $$

> [!Example]- Example: Joint Moment Generating Functions (2)
> Let $X_1, \dots X_n$ be independent, and assume $X_i \sim \text{Gamma}(\alpha_i, \beta)$.
>
> From our earlier derivation, we know that the moment generating of any $X_i$ is given as
> $$
> M_{X_i} (t) = \left( 1 - \frac{t}{\beta} \right)^{-\alpha_i}
> $$
> 
> Thus, assuming our distributions are independent, we can find the moment generating function of the sum of all $X_i$ (let $Y = \sum_{i=1}^n X_i$) as
> $$
> \begin{align*}
>         M_Y (t) &= \prod_{i=1}^n M_{X_i} (t) \\
>                 &= \prod_{i=1}^n \left( 1 - \frac{t}{\beta} \right)^{-\alpha_i} \\
>                 &= \left( 1 - \frac{t}{\beta} \right)^{-(\alpha_1 + \alpha_2 + \dots + \alpha_n)}
> \end{align*}
> $$
>
> Thus, because this still conforms to the moment generating function for the Gamma distribution, we've shown that the sum of the independent Gamma random variable stays as the Gamma distribution, provided that $\beta$ stays constant! 

> [!Example]- Example: Joint Moment Generating Functions (3)
> Let $f_{x,y} (x,y)$ be a joint pdf given as
> $$
> f_{x,y} (x,y) = \begin{cases}
>                 e^{-y} & 0 < x < y < \infty \\
>                 0 & \text{else}
>         \end{cases}
> $$
>
> Find the joint moment generating function.
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
> Note that in this derivation, we forcefully choose the bounds of $s$ and $t$ so that our integral can evaluate. This means that outside of these bounds, our integral (and thus mgf) would be undefined.
>
> Furthermore, we can find $M_X (s)$ and $M_X (t)$ by setting $t = 0$ and $s = 0$, respectively.
> $$
> M_X (s) = \frac{1}{1-s} \qquad M_Y (t) = \frac{1}{(t-1)^2}
> $$
