---
title: Working Notes
---

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

We have expected value
$$
E(X) = \frac{\alpha + \beta}{2}
$$

> $$
> \begin{align*}
>       E(X) &= \int_{-\infty}^\infty x f(x) dx \\
>            &= \int_\alpha^\beta \frac{x}{\beta - \alpha} dx \\
>            &= \frac{\alpha + \beta}{2}
> \end{align*}
> $$

We additionally have variance given by
$$
V(X) = \frac{(\beta - \alpha)^2}{12}
$$

> $$
> \begin{align*}
>       E(X^2) &= \int_{-\infty}^\infty x^2 f(x) dx \\
>              &= \int_\alpha^\beta \frac{x^2}{\beta - \alpha} dx \\
>              &= \frac{\alpha^2 + 2 \alpha \beta + \beta^2}{3}
> \end{align*}
> $$
>
> $$
> V(X) = E(X^2) - E(X)^2 = \frac{(\beta - \alpha)^2}{12}
> $$

### Normal Distribution
The **Normal Distribution**, denoted $X \sim N(\mu, \sigma)$ is the distribution with pdf given as follows:
$$
f(x, \mu, \sigma) = \frac{1}{\sigma \sqrt{2 \pi}} e^{-\frac{1}{2} \left( \frac{x - \mu}{\sigma} \right)^2} = \frac{1}{\sigma \sqrt{2 \pi}} \exp\left( -\frac{1}{2} \left( \frac{x - \mu}{\sigma} \right) \right)
$$
> The curve created by this pdf is sometiems referred to as the **bell curve**.

> [!Note]- PDF Verification
> Let
> $$
> k = \int_{-\infty}^\infty f(x) dx \qquad z = \frac{x - \mu}{\sigma}
> $$
> We find
> $$
> dz = \frac{1}{\sigma} dx
> $$
>
> Using this, we can convert our integral into a double integral as so
> $$
> \begin{align*}
>       k &= \int_{-\infty}^\infty \frac{1}{\sqrt{2\pi}} e^{-\frac{1}{2} z^2} dz \\
>       k \sqrt{2\pi} &= \int_{-\infty}^\infty e^{-\frac{1}{2} z^2} dz \\
>       k^2 2 \pi &= \int_{-\infty}^\infty e^{-\frac{1}{2} w^2} dw \int_{-\infty}^\infty e^{-\frac{1}{2} z^2} dz = \int_{-\infty}^\infty \int_{-\infty}^\infty e^{-\frac{1}{2} (z^2 + w^2)} dw dz      
> \end{align*}
> $$
> 
> If we treat $w = x$ and $z = y$, we see we have a double integral spanning the entire $xy$-plane. We convert to polar coordinates to simplify the integral.
> $$
> w = r \cos(\theta) \qquad z = r \sin(\theta)
> $$
> > When converting to polar, don't forget about the Jacobian!
>
> $$
> \begin{align*}
>       k^2 2 \pi &= \int_0^\infty \int_0^{2\pi} e^{\frac{-r^2}{2}} r d\theta dr \\
>             &= \int_0^\infty 2\pi r e^{\frac{-r^2}{2}} \bigg\vert_0^{2\pi} dr \\
>             &= - 2 \pi \left( \lim_{r\to\infty} e^{\frac{-r^2}{2}} - 1 \right) \\
>             &= 2\pi
> \end{align*}
> $$
> Thus, we find $k^2 2 \pi = 2 \pi \to k = 1$. We have verified our pdf.

If can be shown that $\mu = E(X)$ and $\sigma = \sqrt{V(X)}$, called the **standard deviation**.

For $X \sim N(0,1)$, we can this the **standard normal distribution**. In this case, our pdf simplifies to
$$
f(x) = \frac{1}{\sqrt{2\pi}} e^{-x^2 / 2} 
$$
And we find the expected value and variance as
$$
E(X) = 0 \qquad V(X) = 1
$$
> We can find the expected value by the fact that the function we're integrating is odd! We can additionally find $E(X^2) = 0$ to find our variance.

> [!Abstract] Theorem: Standardizing Normal Distributions
> If $X \sim N(\mu, \sigma)$, then the random variable
> $$
> z = \frac{X - \mu}{\sigma}
> $$
> has the standard normal distribution.
> > This has the effect of essentially shifting our $X$ by $\mu$, then constraining our variance to bring our values closer together / further apart. We can prove this with $z$-sub.
>
> Note that the cdf of the standard normal distribution is often denoted $\Phi(x)$. 

Using this standardization, the probability of obtaining any value between $x_1$, $x_2$ can be found as
$$
P(x_1 \le X \le x_2) = P\left( \frac{x_1 - \mu}{\sigma} \le z \le \frac{x_2 - \mu}{\sigma} \right)
$$

Which can easily be evaluated, as many books / resources have common tables of values for the standard distribution.
> These books may represent tables of values for $x$ for both $-\infty \to x$, or $0 \to x$! Be sure you know which type of table you're using.

> [!Example]+ Example: Applying Normal Distributions (1)
> The height of students obey a normal distribution with $\mu = 67$ inches, $\sigma = 3$ inchdes.
>
> What percent of students have heights between 64 and 70 inches?
>
> We first standardize this distribution - let $z = (x - \mu) / \sigma$. Then,
> $$
> P(64 < X < 70) = P\left( \frac{64 - 67}{3} < z < \frac{70 - 67}{3}  \right) = P(-1 < z < 1)
> $$
>
> We can calculate this to be
> $$
> \int_{-\infty}^1 p(x) - \int_{-\infty}^{-1} = F(1) - F(-1)
> $$
> and use a table of values (or a calculator) to find our result.
> > Note that if we have a table that only tells us $F(1)$, we can find $F(-1) = 1 - F(1)$ by virtue of the normal distribution's symmetry.

> [!Example]- Example: Applying Normal Distributions (2)
> Radiation Exposure in an area takes on a normal distribution with mean $\mu = 4.35$ mrem and standard distribution $\sigma = 0.59$ mrem. What is the probability a person is exposed to more than $5.2 mrem$?
>
> Using our standardization $z = (X - \mu) / \sigma$, we want
> $$
> \begin{align*}
>       P(X > 5.2) &= 1 - P(X < 5.2) \\
>           &= 1 - P\left( z < \frac{5.2 - 4.35}{0.59} \right) \\
>           &= 1 - \Phi(1.44) = 0.0749 
> \end{align*}
> $$

### Gamma Distribution
The **Gamma Distribution**, denoted $X \sim \Gamma(\alpha, \beta)$ is the distribution whose pdf is given as follows:
$$
f(x, \alpha, \beta) = \frac{\beta^\alpha x^{\alpha - 1} e^{-\beta x}}{\Gamma(\alpha)} \qquad x, \alpha, \beta > 0
$$

where $\Gamma(\alpha)$ is the **gamma function**.
$$
\Gamma(\alpha) = \int_0^\infty t^{\alpha - 1} e^{-t} dt
$$
> This complicated looking expression is essentially just scaling a function $x^t e^{-t}$ so that it becomes a valid pdf.

Conceptually, we can relate the Gamma distribution to the Poisson distribution. If the Poisson distribution measures the probability of $x$ successes in some time interval $t$, then the Gamma distribution is measuring the probability of "waiting" a certain amount of time $x$ for $\alpha$ successes, where $\beta$ is our average rate of success.

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
> > We furthermore see that
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

We have the following properties of the Gamma Distribution.

> [!Abstract] Theorem: Gamma Function Expectation
> If $X \sim \Gamma (\alpha, \beta)$, then
> $$
> E(X) = \frac{\alpha}{\beta} \qquad V(X) = \frac{\alpha}{\beta}
> $$
>
> > [!Note]- Proof (Expected Value)
> > $$
> > \begin{align*}
> >     E(X) &= \frac{1}{\Gamma(\alpha)} \int_0^\infty \beta^\alpha x^\alpha e^{-\beta x} dx \\
> >          &= \frac{1}{\Gamma(\alpha)} \int_0^\infty y^\alpha e^{-y} \frac{1}{\beta} dx &y = \beta x \\
> >          &= \frac{1}{\beta} \frac{\Gamma(\alpha + 1)}{\Gamma(\alpha)} &\Gamma(\alpha + 1) = \int_0^\infty t^\alpha e^{-t} dt\\
> >          &= \frac{\alpha}{\beta} \frac{\Gamma(\alpha)}{\Gamma(\alpha)} &\Gamma(\alpha + 1) = \alpha \Gamma(\alpha) \\
> >          &= \frac{\alpha}{\beta}
> > \end{align*}
> > $$
> > The proof for variance follows similarly.

The Gamma distribution has many use cases. Below, we list one of the most common special cases of $X \sim \Gamma(\alpha, \beta)$, the **exponential distribution**.

If random variable has pdf $f(x, \beta) = \beta e^{-\beta x}$, known as the **exponential distribution**, we really just have $\Gamma(1, \beta)$ (probability of time until the first success).

> [!Example] Example: Exponential and Gamma Distribution
> Suppose the total cars exceeding the speed limit in half an hour is a random variable with a Poisson distribution with $\lambda = 8.4$.
>
> What is the probability the wait time is at most 5 minutes between cars exceeding the speed limit?
>
> Here, we define $t = 1$ as "one unit of 30 min". So, we can expect an average of $\lambda \cdot t = 8.4$ cars exceeding the speed limit in a 30 minute period. We find the probability that our wait time is at most 5 minutes using the Gamma distribution, with $\alpha = 1, \beta = 8.4$.
> $$
> \int_0^{5/30} 8.4^1 e^{-8.4 x} x^0 dx \approx 0.75
> $$