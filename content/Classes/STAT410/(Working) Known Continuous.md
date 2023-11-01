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

Finally, we have expected value and variance given as 
$$
E(X) = \frac{\alpha + \beta}{2} \qquad V(X) = \frac{(\beta - \alpha)^2}{12}
$$

These can easily be derived using the definitions for $E(X)$ and $V(X)$, so we omit the derivations below.


### Normal Distribution
The **Normal Distribution**, denoted $X \sim N(\mu, \sigma)$ is the distribution with pdf given as follows:
$$
f(x, \mu, \sigma) = \frac{1}{\sigma \sqrt{2 \pi}} e^{-\frac{1}{2} \left( \frac{x - \mu}{\sigma} \right)^2}
$$
> The curve created by this pdf is sometimes referred to as the **bell curve**.

> [!Note]- PDF Verification
> Let us verify the pdf of the normal distribution below. In other words, we must show that
>
> $$
> \int_{-\infty}^\infty f(x) dx = 1
> $$
>
> Now, let 
> $$
> k = \int_{-\infty}^\infty f(x) dx \qquad z = \frac{x - \mu}{\sigma} \to dz = \frac{1}{\sigma} dx
> $$
>
> Using these variables, we can convert our integral to a double integral as so:
> $$
> \begin{align*}
>       k &= \int_{-\infty}^\infty f(x) dx = \int_{-\infty}^\infty \frac{1}{\sqrt{2\pi}} e^{-\frac{1}{2} z^2} dz \\
>       k \sqrt{2\pi} &= \int_{-\infty}^\infty e^{-\frac{1}{2} z^2} dz \\
>       k^2 2 \pi &= \int_{-\infty}^\infty e^{-\frac{1}{2} w^2} dw \int_{-\infty}^\infty e^{-\frac{1}{2} z^2} dz = \int_{-\infty}^\infty \int_{-\infty}^\infty e^{-\frac{1}{2} (z^2 + w^2)} dw dz      
> \end{align*}
> $$
> 
> Now, if we let $w = x$ and $z = y$, we find that we have a double integral spanning the entire $xy$-plane. Furthermore, as our $x$ and $y$ terms in the integral are given in the form ($x^2 + y^2$), we will convert to polar coordinates to simplify our integral.
> $$
> w = r \cos(\theta) \qquad z = r \sin(\theta) \quad \to \quad w^2 + z^2 = 1
> $$
>
> Accounting for the Jacobian as well, we perform a change of variables to obtain the integral 
> $$
> \begin{align*}
>       k^2 2 \pi &= \int_0^\infty \int_0^{2\pi} e^{\frac{-r^2}{2}} r d\theta dr \\
>             &= \int_0^\infty 2\pi r e^{\frac{-r^2}{2}} \bigg\vert_0^{2\pi} dr \\
>             &= - 2 \pi \left( \lim_{r\to\infty} e^{\frac{-r^2}{2}} - 1 \right) \\
>             &= 2\pi
> \end{align*}
> $$
> Thus, we find $k^2 2 \pi = 2 \pi \to k = 1$. We have verified our pdf.

The expected value and variance for the normal distribution are given as
$$
E(X) = \mu \qquad V(X) = \sigma^2 
$$
> Note that $\sigma = \sqrt{V(X)}$ is often called the **standard deviation**, whereas $\mu = E(X)$ is often called the **mean**.

---

The normal distribution on $X \sim N(0,1)$ is called the **standard normal distribution**. In this special case, our pdf simplifies down to
$$
f(x) = \frac{1}{\sqrt{2\pi}} e^{-x^2 / 2} 
$$
And we find the expected value and variance as
$$
E(X) = 0 \qquad V(X) = 1
$$
> To find the expected value, we can use the fact that the function we're integrating is odd. 

Given a random variable representing a normal distribution, we can perform a transformation on the random variable to obtain the standard normal distribution. This transformation is known as **standardization**.

> [!Abstract] Theorem: Standardizing Normal Distributions
> If $X \sim N(\mu, \sigma)$, then the transformation
> $$
> z = \frac{X - \mu}{\sigma}
> $$
> will yield the standard normal distribution.
>
> This transformation essentially has the effect of shifting our values by $\mu$, then bringing them closer together / further apart by dividing by $\sigma$. 
>
> Note that the cdf of the standard normal distribution is often denoted $\Phi(x)$.

Standardizing normal distributions is often helpful in the real world, as the standard normal distribution is much easier to use in data analysis! Using the standard normal distribution, we can find the probability of obtaining any value between $x_1$, $x_2$ as
$$
P(x_1 \le X \le x_2) = P\left( \frac{x_1 - \mu}{\sigma} \le z \le \frac{x_2 - \mu}{\sigma} \right)
$$

Which can easily be evaluated using commonly known tables for the standard distribution. 
> These books may represent tables of values for $x$ for both $-\infty \to x$, or $0 \to x$! Be sure you know which type of table you're using.

Some examples of this are given below.

> [!Example]+ Example: Standardizing Normal Distributions (1)
> The height of students obey a normal distribution with $\mu = 67$ inches, $\sigma = 3$ inches. What percent of students have heights between 64 and 70 inches?
>
> To calculate this, we will first standardize this distribution. Let's define $Z$ as
> $$
> Z = \frac{X - \mu}{\sigma}
> $$
>
> Then, we can calculate the probability as
> $$
> \begin{align*} 
> P(64 < X < 70) &= P\left( \frac{64 - 67}{3} < z < \frac{70 - 67}{3}  \right) \\
>      &= P(-1 < z < 1) = \int_{-\infty}^1 p(x) - \int_{-\infty}^{-1} \\
>      &= F(1) - F(-1)
> \end{align*}
> $$
>
> We can then use a table of values (or a calculator) to find our result. Note that if we have a table that only tells us $F(1)$, we can find $F(-1) = 1 - F(1)$ by virtue of the normal distribution's symmetry.

> [!Example]- Example: Standardizing Normal Distributions (2)
> Radiation Exposure in an area takes on a normal distribution with mean $\mu = 4.35$ mrem and standard distribution $\sigma = 0.59$ mrem. What is the probability a person is exposed to more than $5.2$ mrem?
>
> Using our standardization of $z = (X - \mu) / \sigma$, we want
> $$
> \begin{align*}
>       P(X > 5.2) &= 1 - P(X < 5.2) \\
>           &= 1 - P\left( z < \frac{5.2 - 4.35}{0.59} \right) \\
>           &= 1 - F(1.44) = 0.0749 
> \end{align*}
> $$


### Gamma Distribution
The **Gamma Distribution**, denoted $X \sim \Gamma(\alpha, \beta)$ is the distribution whose pdf is given as
$$
f(x, \alpha, \beta) = \frac{\beta^\alpha x^{\alpha - 1} e^{-\beta x}}{\Gamma(\alpha)} \qquad x, \alpha, \beta > 0
$$

where $\Gamma(\alpha)$ is the **gamma function**.
$$
\Gamma(\alpha) = \int_0^\infty t^{\alpha - 1} e^{-t} dt
$$
> This complicated looking expression is essentially just scaling a function $x^t e^{-t}$ so that it becomes a valid pdf.

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
> > Furthermore, we see that
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

Conceptually, the Gamma distribution is fairly similar to the Poisson distribution in the discrete case.

If the Poisson distribution measures the probability of $x$ successes in some time interval $t$, then the Gamma distribution is measuring the probability of "waiting" a certain amount of time $x$ for $\alpha$ successes, where $\beta$ is our average rate of success.

We can find the expected value and variance of the Gamma Distribution as so:
$$
E(X) = \frac{\alpha}{\beta} \qquad V(X) = \frac{\alpha}{\beta}
$$

> [!Note]- Derivation for Expected Value
> $$
> \begin{align*}
>     E(X) &= \frac{1}{\Gamma(\alpha)} \int_0^\infty \beta^\alpha x^\alpha e^{-\beta x} dx \\
>          &= \frac{1}{\Gamma(\alpha)} \int_0^\infty y^\alpha e^{-y} \frac{1}{\beta} dx &y = \beta x \\
>          &= \frac{1}{\beta} \frac{\Gamma(\alpha + 1)}{\Gamma(\alpha)} &\Gamma(\alpha + 1) = \int_0^\infty t^\alpha e^{-t} dt\\
>          &= \frac{\alpha}{\beta} \frac{\Gamma(\alpha)}{\Gamma(\alpha)} &\Gamma(\alpha + 1) = \alpha \Gamma(\alpha) \\
>          &= \frac{\alpha}{\beta}
> \end{align*}
> $$
> The derivation for variance follows similarly.

---

The Gamma distribution has many use cases. Below, we list some of the of most common cases.

The Gamma distribution on $X \sim \Gamma(1, \beta)$ is known as the **exponential distribution**. In this distribution, we're measuring the probability of the first success at some time.
$$
f(x, \beta) = \beta e^{-\beta x}
$$

> [!Example]+ Example: Exponential Distribution
> Suppose the total cars exceeding the speed limit in half an hour is a random variable with a Poisson distribution with $\lambda = 8.4$.
>
> What is the probability the wait time is at most 5 minutes between cars exceeding the speed limit?
>
> Here, we define $t = 1$ as "one unit of 30 min". So, we can expect an average of $\lambda \cdot t = 8.4$ cars exceeding the speed limit in a 30 minute period. We find the probability that our wait time is at most 5 minutes using the Gamma distribution, with $\alpha = 1, \beta = 8.4$.
> $$
> \int_0^{5/30} 8.4^1 e^{-8.4 x} x^0 dx \approx 0.75
> $$

The Gamma Distribution with pdf
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

In the continuous case, if $X$ and $Y$ are random variables and $f(x,y)$ is defined over $\mathbb{R}^2$, then $f(x,y)$ is the **joint probability density function** over $X$ and $Y$ if
$$
P(X,Y) \in \mathbb{R} = \int\int_R f(x,y) dA
$$
where $R$ is a region on the $xy$-plane.

Properties of the cumulative pdf are given below.
1. $f(x,y) \ge 0$ for all $x,y \in \mathbb{R}$.
2. $\int_{-\infty}^\infty  \int_{-\infty}^\infty f(x,y) dy dx = 1$

If $X,Y$ are continuous random variables, then
$$
F(x,y) = P(X \le x, Y \le y) = \int_{-\infty}^y \int_{-\infty}^x f(s,t) ds dt
$$
where $f(s,t)$ is the joint pdf of $X$ and $Y$ is the **joint distribution function (cumulative)** of $X$ and $Y$.

Similar to the idea of the one-varibale case, we now have
$$
f(x,y) = \frac{\partial^2}{\partial x \partial y} F(x,y) = F_{yx} = \frac{\partial^2}{\partial x \partial y} F(x,y) = F_{xy}
$$

> [!Example] Example: Calculating the CDF (Continuous Case)
> $$
> f(x,y) = \begin{cases}
>               x + y & 0 < x < 1, 0 < y < 1 \\
>               0 & \text{else} 
>        \end{cases}
> $$
> Given the above pdf, find the cdf of $X$ and $Y$.
>
> Clearly, if $x,y \le 0$, then $F(x,y) = 0$. Furthermore, if $x,y \ge 1$, then $F(x,y) = 1$, and for $0 < x,y < 1$,
> $$
> F(x,y) = \int_0^y \int_0^x (s + t) ds dt = \frac{1}{2} xy (x + y)
> $$
>
> And for $x > 1, 0 < y < 1$, we have
> $$
> F(x,y) = \int_0^y \int_0^1 (s + t) ds dt = \frac{1}{2} (y) (y + 1)
> $$
> 
> Similarly, for $y > 1$, $0 < x < 1$ we have
> $$
> F(x,y) = \frac{1}{2} (x) (x + 1)
> $$
>
> This gives us cdf
> $$
> F(x,y) = \begin{cases}
>               0 & x,y \le 0 \\
>               \frac{1}{2} xy (x + y) & 0 < x, y < 1 \\
>               \frac{1}{2} y (y + 1) & 0 < y < 1, x > 1 \\
>               \frac{1}{2} x (x + 1) & 0 < x < 1, y > 1 \\
>               1 & 1 \le x,y
>        \end{cases}
> $$

> [!Example] Transformations on Random Variables (Continuous Case)
> $$
> f(x,y) = \begin{cases}
>               x^2 + y & 0 \le x \le 3, 0 \le y \le 4 \\
>               0 & \text{else}
>        \end{cases}
> $$
>
> Find $P( \vert X - 1 \vert \le 1/2)$.
>
> $$
> P( \vert X - 1 \vert \le 1/2) = P(1/2 \le X \le 3/2) = \int_0^4 \int_{1/2}^{3/2} x^2 + y \; dx dy = \frac{37}{180}
> $$

> [!Example]
> Given the joint CDF
> $$
> F(x,y) = \begin{cases}
>          (1 - e^{-x}) (1 - e^{-y}) & x,y > 0 \\
>          0 & \text{else}
>        \end{cases}
> $$
>
> Find $P(1 < X < 3, 1 < Y < 2)$. To find this, we need $f(x,y)$, so we need to take the partial derivative twice.
> $$
> f(x,y) = F_{xy} (x,y) = e^{-(x+y)} = F_{yx}
> $$
>
> $$
> \to P(1 < X < 3, 1 < Y < 2) = \int_1^2 \int_1^3 e^{-(x+y)} \; dx dy = 0.074
> $$

> [!Example]
> In a study, the houss $X$ spent using their phones, andthe hours $Y$ spent on their job is approximated by the joint pdf
>
> $$
> f(x,y) = xy e^{-(x+y)} \qquad x,y > 0
> $$
>
> What is the probability a person spends at least twice as much time on their phone than doing their job?
>
> We want $P(X \ge 2Y)$.
> $$
> P(X \ge 2Y) = \int_0^\infty \int_0^{X/2} xy e^{-(x+y)} \; dy dx
> $$

Note that these techniques generalize to $n$ variable functions.

# Section 6.2: Conditional Distributions and Independence
If $f(x,y)$ is the joint pmf of a discrete random variable, then the function $g_X (x) = \sum_y f(x,y)$ for each $x$ that $X$ takes on is the **marginal distribution** of $X$.
> We have an analogoue on $Y$ as well.

In other words, the total probability of $x$ occurring over all possible cases.

Similarly for the continuous case, we have
$$
g_X (x) = \int_{-\infty}^\infty f(x,y) dy
$$
> note that for the marginal distributions, we sum or integrate over the other variable.

If $f(x,y)$ is the joint pmf of discrete random variable $X$ and $Y$, and $g_Y (y)$ is the marginal distribution (pmf) of $Y$, then
$$
f(x | y) = \frac{f(x,y)}{g_Y (y)} \qquad y_Y (y) \ne 0
$$
for each $x$ in $X$, is the **conditional distribution (pmf)** of $X$, given $Y = y$.
> This is exactly analogous to the definition of conditionla probability.

Similarly, the conditional cdf of $X$ given $Y = y$ is
$$
f(x | y) = P( X \le x | Y =y ) = \sum_{a\le x} f(a | y)
$$

For the continuous case, everything follows naturally with the pmf replaced with pdf.

> [!Example]
> Let the joint pdf of $X$ and $Y$ be
> $$
> f(x,y) = \begin{cases}
>          \frac{2}{3} (x + 2y) & 0 < x, y < 1 \\
>          0 & \text{else}
>        \end{cases}
> $$
>
> Find $P(X \le 1/2 | Y = 1/2)$. In other words, we want the cdf $F(1/2, 1/2)$.
>
> We want
> $$
> \int_0^{1/2} f(x | y = 1/2) \; dx
> $$
>
> We do this by first finding the marginal pdf as
> $$
> g_Y (y) = \int_{-\infty}^\infty f(x,y) dx = \int_0^1 f(x,y) dx = \frac{1}{3} (1 + 4y)
> $$
> Then
> $$
> \begin{align*}
>       f(x|y) &= \frac{f(x,y)}{g_Y(y)} \\ 
>       &= \frac{\frac{2}{3} (x + 2y)}{\frac{1}{3} (1 + 4y)} \\
>       \to f(x | 1/2) &= \frac{2x + 2}{3}
> \end{align*}
> $$
>
> Letting us find our answer as
> $$
> P(X \le 1/2 | Y = 1/2) = \int_0^{1/2} \frac{2x + 2}{3} dx = \frac{5}{12} 
> $$

Lt $g_i (x)$ be the marginal distribution of random variable $X_i$. We say random variables $X_1, X_2, \dots, X_n$ are **independent** if and only if for all $(x_1, \dots, x_n)$ that $X_1, \dots, X_n$ take on, we have that
$$
f(x_1, \dots, x_n) = g_1 (x_1) g_2 (x_2) \dots g_n (x_n)
$$

Thus, we see that if $X$ and $Y$ are independent,
$$
f(x | y) = \frac{f(x,y)}{g_Y (y)} = \frac{g_X (x) g_Y (y)}{g_Y (y)} = g_X (x)
$$
> Given that $Y$ is something, we still get the same probability of $X$ - our probability of $X$ is not affected.

> [!Example]
> Given the joint pdf of $X,Y$
> $$
> \begin{align*}
> f(x,y) = \begin{cases}
>          12xy (1-y) & 0 < x,y < 1 \\
>          0 & \text{else}
>        \end{cases}
> \end{align*}
> $$
>
> We find that
> $$
> \begin{align*}
>       g_X (x) = \int_0^1 f(x,y) dy = 2x \\
>       g_Y (y) = \int_0^1 f(x,y) dx = 6 (1-y) y
> \end{align*}
> $$
> 
> Because the product $g_X (x) g_Y (y) = f(x,y)$ our random variables $X,Y$ are independent.

> [!Example]
> Let $X \sim \text{Binom} (n,p)$ and $Y \sim \text{Binom} (m,p)$.
>
> Assume $X$ and $Y$ are independent. Define $Z = X + Y$ to get random variable $Z \sim \text{Binom} (n+m, p)$. Determine the pmf of $X|Z$.
>
> Now
> $$
> f(x|z) = \frac{P(X = x | z = x + y)}{g_Z (z)} = \frac{P(X = x | Y = z - x)}{g_Z (z)}
> $$
> Because we know $X$ and $Y$ are independent,
> $$
> \frac{P(X = x | Y = z - x)}{g_Z (z)} = \frac{P(X = x) P(Y = z - x)}{g_Z (z)} = \frac{g_X (x) g_Y (y)}{g_Z (z)}
> $$
> $$
> = \frac{\binom{n}{x} p^x (1-p)^{n-x} \binom{m}{z-x} p^{z-x} (1-p)^{m-z+x} }{\binom{n+m}{z} p^z (1-p)^{n+m-z}}
> $$
>
> $X|Z$ turns out to be the hypergeometric distribution!
> $$
> \frac{\binom{n}{x} \binom{m}{z-x}}{\binom{n+m}{z}}
> $$
>
> So, $X$ and $Z$ are not independent, as the conditioning of $Z$ yielded a completely different distribution from $X$.

> [!Abstract]
> Let $X, Y$ be independent random variables with pmf/pdfs given as $f_X (x), f_Y (y)$. Define $Z = X + Y$.
>
> Then, for the continuous case,
> $$
> f_Z (z) = \int_{-\infty}^\infty f_X (x) f_Y (z - x) dx
> $$
> Called the convolution of the two functions.

> [!Example]
> Let $X \sim \text{Binom}(n,p)$ and $Y \sim \text{Binom} (m,p)$.
? 
> Let $X,Y$ be independent and assume
> $$
> f_X (t) = f_Y (t) = \begin{cases}
>         e^{-t} & t > 0 \\
>         0 & \text{else}
>     \end{cases}
> $$
>
> Take random variable $Z = X + Y$. Then, its pdf is
> $$
> \begin{align}
>       f_Z (z) &= \int_{-\infty}^\infty f_X (x) f_Y (z - x) dx \
>       &= \int_0^z e^{-x} e^{-(z-x)} dx \\
>       &= z e^{-z}
> \end{align}
> $$
> This gives us the same exponential distributions as $X$ and $Y$, though note that this generally does not happen.
> 
> Note that we can only do this because our random variables are independent of one another.


# Section 6.3: Transforming Random Variables of Joint Distribution
Recall that if $f_X (x)$ is the pdf, $y = g(x)$, the pdf for $Y = g(x)$ is
$$
f_Y (y) = f_X ( g^{-1} (y) ) \cdot \frac{d}{dy} g^{-1} (y)
$$

Now given $f_{X,Y} (x,y)$ and $u = h_1 (x,y), v = h_2 (x,y)$, what is the joint pdf of $u$ and $v$?

We assume that or partial derivatives exist, and that they're one-to-one. We can then solve $x,y$ in terms of $u,v$ (change of variables in multi-variable calculus).

> [!Abstract] Theorem: Transforming Joint Distributions
> Suppose we have random variables $X,Y$ with joint pdf $F_{X,Y} (x,y)$ and
> $$
> U = h_1 (X,Y) \qquad V = h_2 (X,Y)
> $$
>
> Then, the joint pdf of $U$ and $V$ is given as
> $$
> f_{U,V} (u,v) = f_{X,Y} (x (u,v), y(u,v)) \bigg\vert J(u,v) \bigg\vert
> $$
> Where the Jacobian, $J$ (provided $J \ne 0$) is given as
> $$
> J = \text{det} \begin{bmatrix}
>     \partial x / \partial u & \partial x / \partial v \\
>     \partial y / \partial u & \partial y / \partial v
>   \end{bmatrix}
> $$
> 
> > **Note**: One can show that with $U = h_1(X,Y), V = h_2 (X,Y)$,
> > $$
> > J^{-1} = \frac{1}{ \text{det} \begin{bmatrix}
> >          \partial h_1 / \partial x & \partial h_1 / \partial y \\
> >          \partial h_2 / \partial x & \partial h_2 / \partial y
> >        \end{bmatrix} }
> > $$
> > Which can be helpful if $J^{-1}$ yields a constant result (if it does not, we'll have to convert $X,Y$ into $U,V$ which can be painful).

> [!Example]
> Let the joint pdf of $X,Y$ be given as
> $$
> f(x,y) = \begin{cases}
>          e^{-(x+y)} & x,y > 0 \\
>          0 & \text{else}
>        \end{cases}
> $$
>
> Find the joint density of $U = X + Y, V = \frac{X}{X + Y}$.
>
> We first solve for $x,y$ in terms of $u,v$ to perform our change of variables.
> $$
> x = uv \qquad y = u - uv
> $$
> We can use this to find our Jacobian as
> $$
> J(u,v) = \begin{vmatrix}
>        v & u \\ 1-v & -u
>        \end{vmatrix} = -u
> $$ 
>
> Now, we can apply our theorem.
> $$
> f_{U,V} (u,v) = f_{X,Y} (uv, u - uv) \vert -u \vert = u e^{-u} 
> $$
> With bounds $0 < u, 0 < v < 1$.

> [!Example]
> Let $X \sim N(\mu_1, \sigma_1^2)$, $Y \sim N(\mu_2, \sigma_2^2)$
>
> Assume $X$ and $Y$ are independent. Find the joint pdf of $U = X + Y, V = X - Y$.
>
> Being independent, we know that $f_{X,Y} (x,y) = f_X (x) * f_Y (y)$.
>
> Then,
> $$
> x = \frac{u + v}{2} \qquad y = \frac{u - v}{2} 
> $$
> We can find the Jacobian as $- 1/2$, and find our joint pdf as
>
> $$
> \begin{align*}
> f_{U,V} (u,v) = f_{X,Y} ( \frac{u+v}{2}, \frac{u-v}{2} ) \vert \frac{1}{-2} \vert
> \end{align*}
> $$

> [!Example]
> Let $X,Y$ have joint pdf
> $$
> f(x,y) = \begin{cases}
>          xy / 96 & 0 < x < 4, 0 < y < 5 \\
>          y & \text{else}       
>        \end{cases}
> $$
> Find the pdf of $U = X + 2Y$.
>
> We find the joint distribution of $U$ by finding the joint distribution of $U$ and $V$ first. Let $u = x + 2y$, and $v = x$. Then, $x = v$, and $y = (u - v) / 2$
>
> ... YOu need to find the new region between $0 < v < 4, v  + 2 < u < v + 10$ after transforming
>
> Then, we need to find the marginal distribution to find the distribution of $U$.


---


...


---

The **covariance** of $X$ and $Y$ is given as
$$
Cov(X,Y) = E((X - E(X)) (Y - E(Y))) = E( (X - \mu_x) (Y - \mu_y) )
$$

> [!Abstract]
> $$
> Cov(X,Y) = E(XY) - E(X) E(Y)
> $$
>
> > [!Note] Proof
> > $$
> > E(XY - E(X) Y - X E(Y) + E(X) E(Y) ) = E(XY) - E(X) E(Y) - E(X) E(Y) + E(X) E(Y)
> > $$

> [!Info] Corollary
> If $X$ and $Y$ are independent, then $Cov(X,Y) = 0$ (they are uncorrelated).

Properties are given below:
- $Cov(X,X) = V(X)$
- $Cov(X,Y) = Cov(Y,X)$
- $Cov(kX, Y) = kCov(X,Y)$

> $Cov(X,Y)$ is seen as a measure of the linear relationship of $X$ and $Y$.

The **correlation coefficient** of $X$ and $Y$ is
$$
\mathcal{P}_{X,Y} = \frac{Cov(X,Y)}{\sqrt{V(X)V(Y)}}
$$

> [!Abstract] Theorem
> For random variables $X,Y$,
> 1. $-1 \le \mathcal{P}_{X,Y} \le 1$
> 2. $\mathcal{P}_{X,Y} = \pm 1$ if and only if $Y = \alpha X + \beta$, for some $\alpha, \beta \in \mathbb{R}$.

> [!Example]
> Let the pdf of $X,Y$ be
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
>       &E(X) = \dots = 1/3 \\
>       &E(Y) = \dots = 1/3 \\
>       &E(XY) = \dots = 1/12 \\
>       &Cov(XY) = E(XY) - E(X) E(Y) = -1/36
> \end{align*}
> $$
>
> Furthermore, we can find the correlation coefficient as
> $$
> \begin{align*}
>       &V(X) = E(X^2) - E(X)^2 = 1/18
>       &V(Y) = E(Y^2) - E(Y)^2 = 1/18
>       &\mathcal{P}_{X,Y} = -1/2
> \end{align*}
> $$

> [!Abstract] Theorem
> Let $X_1, \dots, X_n$ be random variables, and assume
> $$
> Y_1 = \sum_{i=1}^n a_i X_i \qquad Y_2 = \sum_{i=1}^n b_i X_i
> $$
>
> Then,
> $$
> Cov(Y_1, Y_2) = \sum_{i=1}^n a_i b_i V(X_i) + 2 \sum_{i < j} a_i b_j Cov(X_i, Y_j)
> $$
>
> > [!Info] Corollary
> > If $Y = X_1 + X_2 + \dots + X_n$, then
> > $$
> > Cov(Y,Y) = V(Y) = \sum_{i=1}^n V(X_i) + 2 \sum_{i < j} Cov(X_i, X_j)
> > $$
> > In particular, if $X_1, \dots, X_n$ are independent, then
> > $$
> > V(Y) = \sum_{i=1}^n V(X_i)
> > $$

> [!Example]
> Let the pdf of $X,Y$ be
> $$
> f(x,y) = \begin{cases}
>          \frac{1}{3} (x + y) & 0 < x < 1, 0 < y < 2 \\
>          0 & \text{else}
>        \end{cases}
> $$
>
> Find $V(Z)$, where $Z = 3X + 4Y - 5$.
> 
> Since the variance of a constant is 0, and $Cov(X,5) = Cov(Y,5) = 0$, we want
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