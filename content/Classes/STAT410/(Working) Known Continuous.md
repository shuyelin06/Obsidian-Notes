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

---

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

---

If Random Variable $X$ has pdf
$$
f(x, v) = \frac{1}{2^{v/2} \Gamma(v/2)} x^{\frac{v-2}{2}} e^{-\frac{x}{2}}
$$
then it is the **chi-squared distribution**, where $v$ is the degrees of freedom.
> Subbing in from the Gamma distribution, if
> $$
> Y \sim \Gamma(v/2, 1/2)
> $$
> Then $E(Y) = v, V(Y) = 2v$

This distribution is used a lot in sampling theory.

---

### Cauchy Distribution
If $X$ has pdf
$$
f(x, \theta) = \frac{1}{\pi} \cdot \frac{1}{(x - \theta)^2 + 1}
$$
with $-\infty < x < \infty$, t is the **Cauchy distribution**. If you were to sketch this distribution, you would find it look similar to a normal distribution, but with slower decreasing sides.

> Let's verify this is a pdf for $\theta = 0$.
> $$
> \begin{align*}
> \frac{1}{\pi} \int_{-\infty}^\infty \frac{1}{x^2 + 1} dx &= \frac{1}{\pi} \left( \lim_{t\to\infty} \tan^{-1}(t) - \lim_{s\to-\infty} \tan^{-1} (s) \right) \\
>               &= \frac{1}{\pi} \left( \frac{\pi}{2} + \frac{\pi}{2} \right) = 1
> \end{align*}
> $$

We find the expected value does not exist.
$$
\begin{align*}
E(X) &= \frac{1}{\pi} \int_{-\infty}^\infty \frac{ \vert x \vert }{1 + x^2} dx = \frac{2}{\pi} \int_0^\infty \frac{x}{1+x^2} dx
     &= \frac{1}{\pi} \lim_{t\to\infty} \ln(1 + u) \bigg\vert_0^t = \infty
\end{align*}
$$

This distribution commonly ocurs in optics problems.


###
If $X$ has pdf
$$
f(x, \alpha, \beta) = \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha) \Gamma(\beta)} x^{\alpha - 1} (1 - x)^{\beta - 1}
$$
where $0 < x < 1$, and $\alpha, \beta > 0$, then it is called the **Beta Distribution**, $X \sim \text{Beta}(\alpha, \beta)$.

We verify this is a valid pdf.

> To verify it is a pdf, we will start from the Gamma distribution and manipulate it to obtain our Beta Distribution. We use
> $$
> \Gamma(\alpha) = \int_0^\infty t^{\alpha - 1} e^{-t} dt
> $$
> With $\alpha = a + 1, \beta = b + 1$, and
> $$
> \Gamma(\alpha) \Gamma(\beta) = \int_0^\infty x^a e^{-x} dx \int_0^\infty y^b e^{-y} dy = \int \int \dots dx dy
> $$
>
> We can manipulate this double integral and show it is equal to $\Gamma(\alpha + \beta)$.
>
> Use change of variables $x = uv$, $y = (1-u)v$. Then, $u = x / (x + y)$, and $v = y / (1 - u)$. Note that as $x \to \infty, u \to 1$.
> $$
> \int_0^\infty \int_0^1 u^a (1-u)^b v^{a+b+1} e^{-v} du dv
> $$
> Note that we can pull $\Gamma(a + b + 2)$ out of this,
> $$
> \Gamma(a + b + 2) \int_0^1 u^a (1 - u)^b du = \Gamma(\alpha + \beta) x^{\alpha - 1} (1-u)^{\beta - 1}
> $$
> Which will divide our expression to get 1.

> [!Abstract] Theorem
> If $X \sim \text{Beta}(\alpha, \beta)$, then
> $$
> E(X) = \frac{\alpha}{\alpha + \beta} \qquad V(X) = \frac{\alpha \beta}{(\alpha + \beta)^2 (\alpha + \beta + 1)}
> $$
>
> > [!Note] Proof (Expected Value)
> > $$
> > \begin{align*}
> > E(X) &= \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha) \Gamma(\beta)} \int_0^1 x \cdot x^{\alpha - 1} (1 - x)^{\beta - 1} dx \\
> >      &= \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha) \Gamma(\beta)} \frac{\Gamma (\alpha + 1) \Gamma(\beta)}{\Gamma(\alpha + 1 + \beta)} \frac{\Gamma(\alpha + 1 + \beta)}{\Gamma(\alpha + 1) \Gamma(\beta)} \int_0^1 x^\alpha (1-x)^{\beta - 1} dx
> > \end{align*}
> > $$
> > Looking at the last two terms, notice that we are really just integrating $\text{Beta}(\alpha + 1, \beta)$. Note that because of this, we eliminate terms by how definition of the beta function being a pdf.
> >
> > $$
> > \begin{align*}
> >  \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha) \Gamma(\beta)} \frac{\Gamma (\alpha + 1) \Gamma(\beta)}{\Gamma(\alpha + 1 + \beta)} &= \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha) \Gamma(\beta)} \frac{\alpha \Gamma (\alpha) \Gamma(\beta)}{\Gamma(\alpha + \beta) (\alpha + \beta)} \\
> > &= \frac{\alpha}{\alpha + \beta}
> > \end{align*}
> > $$
> >
> > The derivation for the variance is quite similar.


What we covered (SUMMARY)
1. Uniform
2. Normal
3. Gamma (Exponential, Chi-Squared)
4. Cauchy
5. Beta


# Section 5.3: Transforming Random Variables
Given $X$, how do we find the distribution of $Y = g(X)$?

In the discrete case, g(X) needs to be one-to-one, and if it is, we just sub in our values and we're done!

> [!Example]
> If $X \sim \text{Binomial} (n,p)$, find the pmf of $Y = 2X + 3$.
>
> We find the pmf of $Y$ by finding the values of $Y$ that are valid, and subbing in the distribution.
>
> We know that $P(Y = y) = P(2X + 3 = y) = P(X = (y-3)/2$. So, if $(y - 3)/2 \ne 0, 1, \dots, n$, then $P(Y) = 0$.
>
> Now, subbing in our distribution, we find pmf
> $$
> f_Y(y) = \begin{cases}
>        \binom{n}{(y-3)/2} p^{(y-3)/2} (1-p)^{n-(y-3)/2} & y = 3, 5, \dots, 2n + 3 \\
>        0 & \text{otherwise}
> \end{cases}
> $$

In the continuous case, where $y = g(x)$ is strictly increasing (or decreasing), we have the theorem:

> [!Abstract] Theorem: Transforming Random Variables, Continuous
> Let $f_x(x)$ be the pdf of a continuous random variable, and suppose $y = g(x)$ is strictly increasing or decreasing. Then, the pdf of $Y = g(x)$ is given as
> $$
> \begin{align*}
> f_Y(y) = \begin{cases}
>               f_x ( g^{-1} (y)) \left \vert \frac{d}{dy} g^{-1} (y) \right \vert & y = g(x) \text{ for some } x \\
>               0 & \text{otherwise}
>        \end{cases}
> \end{align*}
> $$
> Provided $\frac{d}{dy} g^{-1} (y)$ exists.
>
> > [!Note]
> >
> > Assume $y = g(x)$ is increasing. Then, we know $x = g^{-1} (y)$ and $dx = \frac{d}{dy} \left( g^{-1} (y) \right) dy$. We use this to find $P(a < Y < b)$ as
> > $$
> > \begin{align*}
> > P(a < Y < b) &= P(g^{-1} (a) < X < g^{-1} (b) ) \\
> >     &= \int_{g^{-1}(a)}^{g^{-1}(b)} f_X (x) dx \\
> >     &= \int_a^b f_X ( g^{-1} (y) ) \frac{d}{dy} g^{-1} (y) dy \\
> >     &= \text{CDF of Y} \\
> >     &= \int_a^b f_Y (y) dy
> > \end{align*}
> > $$

> [!Example]
> Let the pdf of $X$ be given as
> $$
> f_X (x) = \begin{cases}
>         e^{-x} & x > 0 \\
>         0 & \text{else}
>     \end{cases}
> $$
> Find the pdf of $Y = \sqrt{x}$.
>
> We see that because our pdf is always decreasing, using the theorem, we can find
> $$
> y = \sqrt{x} \to x = g^{-1} (y) = y^2
> $$
> 
> And use this to find the pdf as
> $$
> f_Y (y) = \begin{cases}
>         2y e^{-y^2} & y > 0 \\
>         0 & \text{else}
>     \end{cases}
> $$

> [!Example]
> Let $X \sim \text{Uniform} (0,4)$. Find the pdf of $Y = \sqrt{x}$. (PRACTICE)
>
> Using the cdf of Y, we can try to find the pdf of $Y$
> $$
> F_Y (y) = P(Y \le y) = P( \sqrt{x} \le y ) = P ( x \le y^2 )
> $$
> Given the pdf of $x$, we can just integrate up to $y^2$ to find the cdf of $y$.
>
> $$
> \int_{-\infty}^{y^2} f_X (x) dx = \int_0^{y^2} 1/4 dx = \frac{1}{4} y^2
> $$
> We now differentiate to get the pdf of $y$, $f_Y (y) = \frac{1}{2} y$, which holds between $0 \le y \le 2$.
>
> This is a generalized technique that may work for simple scenarios.

> [!Example]
> Let $X \sim N(0,1)$ be the standard normal distribution. Find the pdf of $Y = X^2$.
>
> Note that we cannot use the theorem, as the pdf of our normal distribution is not strictly increasing or decreasing.
>
> We can just use our generalized technique instead! We note that $y = x^2 \to x = \vert \sqrt{y} \vert$. Then, we find the cdf of $y$ as 
> $$
> F_Y(y) = P(Y \le y) = P(x^2 \le y) = P( -\sqrt{y} \le x \le \sqrt{y} ) = F_X(\sqrt{y}) - F_X (-\sqrt{y}) 
> $$
>
> We differentiate here to find the pdf as
> $$
> f_y (Y) = f_x (\sqrt{y}) \frac{1}{2} y^{-1/2} + f_x (-\sqrt{y}) \frac{1}{2} y^{-1/2} = f_x (\sqrt{y}) y^{-1/2} = \frac{1}{x} f_x (x)
> $$
> For $y > 0$, else 0.
>
> > General solution: start with the cdf of $Y$ to relate to $X$, then differentiate to find the pdf solution.

--- End of chapter 5


# Section 6.1: Joint Distributions
Consider 2 random variables over a joint sample space. For a random variable $X, Y$, we are interested in $P(X = x, Y = y)$.

If $X$ and $Y$ are discrete random variables, the function $f(x,y) = P(X = x, Y = y)$ for each pair of values $(x,y)$ that $X,Y$ take on, otherwise known as the **joint probability distribtion (joint pdf)** of $X$ and $Y$.

Properties of the joint probability distribution are given as follows:
1. $f(x,y) \ge 0$
2. $\sum_x \sum_y f(x,y) = 1$

In the discrete case of 2 random variables, we will often represent the results of random variables now as a table of values.

> [!Example]
> There are 3 (different) math books, 2 history, 4 physics.
>
> Before, we could only define a single random variable $X$ for one type of book specifically. Now, we can define multiple random variables at once.
>
> Let $X,Y$ be the total math and history books chosen out of2 at once, respectively.
>
> We can use this to find the probability of multiple random variables occurring at once.
> $$
> P(X = 1, Y = 1) = \frac{\binom{3}{1}\binom{2}{1}}{\binom{9}{2}} = \frac{1}{6}
> $$

If $X,Y$ are discrete random variables, the function
$$
F(x,y) = P(X \le x, Y \le y) = \sum_{s \le x} \sum_{t \le y} f(s,t)
$$
where $f(s,t)$ is the pdf of the joint distribution, is the **joint cumulative probability distribution** of $X$ and $Y$.

Properties of the joint cdf are given as follows:
1. $F(-\infty, -\infty) = 0$
2. $F(\infty, \infty = 1$
3. If $a < b$, and $c < d$, then $F(a,c) \le F(b,d)$.

> [!Example]
> From the last example,
> $$
> F(1,1) = P(X \le 1, Y \le 1) = f(0,0) + f(0,1) + f(1,0) + f(1,1) = \frac{8}{9}
> $$

