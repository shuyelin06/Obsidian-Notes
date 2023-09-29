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

Using this standardization, the probability of obtaining any value between $x_1$, $x_2$ can be found as
$$
P(x_1 \le X \le x_2) = P\left( \frac{x_1 - \mu}{\sigma} \le z \le \frac{x_2 - \mu}{\sigma} \right)
$$

Which can easily be evaluated, as many books / resources have common tables of values for the standard distribution.
> These books may represent tables of values for $x$ for both $-\infty \to x$, or $0 \to x$! Be sure you know which type of table you're using.

