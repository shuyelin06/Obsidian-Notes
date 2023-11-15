---
title: Random Variables (Multivariate) 
tags:
- stat410
---

# Introduction to Joint Random Variables
Consider 2 random variables over a joint sample space, $X$ and $Y$.
> Note that techniques in this entire section generalize to $n$ variable functions, though for simplicity we will only cover the 2-variable case.

## Discrete Case
In the discrete case, if $X$ and $Y$ are discrete random variables, then the **joint probability distribution** of $X$ and $Y$, denoting the probability of the value pair $(x \in X, y \in Y)$ occurring, is given as
$$
f(x,y) = P(X = x, Y = y)
$$
> In the discrete case of 2 random variables, we often find it useful to represent $f(x,y)$ as a table of values, where rows denote one random variable, and columns denote the other.

The discrete joint pdf has the following properties:
1. $f(x,y) \ge 0$
2. $\sum_x \sum_y f(x,y) = 1$

> [!Example]+ Example: Joint Probability Distributions (Discrete Case)
> There are 3 (different) math books, 2 history, 4 physics.
>
> Before, we could only define a single random variable $X$ for one type of book specifically. Now, using joint distributions, we can define multiple random variables at once.
>
> Let $X$ be the total math books chosen, and $Y$ be the total history books chosen, out of 2 books total. We can use $f(x,y)$ to find the probability of multiple random variables occurring at once.
> $$
> P(X = 1, Y = 1) = \frac{\binom{3}{1}\binom{2}{1}}{\binom{9}{2}} = \frac{1}{6}
> $$

Furthermore, given $f(x,y)$, the **joint cumulative probability distribution** of $X$ and $Y$ is given as
$$
F(x,y) = P(X \le x, Y \le y) = \sum_{s \le x} \sum_{t \le y} f(s,t)
$$
Where $f(s,t)$ is the pdf of the joint distribution.

The discrete joint cdf has the following properties:
1. $F(-\infty, -\infty) = 0$
2. $F(\infty, \infty) = 1$
3. If $a < b$, and $c < d$, then $F(a,c) \le F(b,d)$.


## Continuous Case 
In the continuous case, if $X$ and $Y$ are continuous random variables, then the **joint probability density function** $f(x,y)$ over $X$ and $Y$ is given as the function satisfying
$$
P(X,Y) \in \mathbb{R} = \int\int_R f(x,y) dA
$$
Where $R$ is a region on the $xy$-plane.

The continuous joint pdf has the following properties:
1. $f(x,y) \ge 0$ for all $x,y \in \mathbb{R}$.
2. $\int_{-\infty}^\infty  \int_{-\infty}^\infty f(x,y) dy \; dx = 1$

Furthermore, given $f(x,y)$, we can find the **joint cumulative probability distribution** of $X$ and $Y$ as
$$
F(x,y) = P(X \le x, Y \le y) = \int_{-\infty}^y \int_{-\infty}^x f(s,t) ds dt
$$

Similar to the continuous one-variable case, we can differentiate the cdf to find our pdf, and integrate our pdf to find our cdf. Note that order of differentiation and integration do not matter.
$$
f(x,y) = \frac{\partial^2}{\partial x \partial y} F(x,y) = F_{yx} = \frac{\partial^2}{\partial x \partial y} F(x,y) = F_{xy}
$$

Consider the following examples.

> [!Example]+ Example: Joint Continuous Distributions
> Given the joint cdf
> $$
> F(x,y) = \begin{cases}
>          (1 - e^{-x}) (1 - e^{-y}) & x,y > 0 \\
>          0 & \text{else}
>        \end{cases}
> $$
>
> Find $P(1 < X < 3, 1 < Y < 2)$.
>
> To find this, we first find $f(x,y)$ by taking the partial derivative of the cdf twice.
> $$
> f(x,y) = F_{xy} (x,y) = e^{-(x+y)} = F_{yx}
> $$
>
> $$
> \to P(1 < X < 3, 1 < Y < 2) = \int_1^2 \int_1^3 e^{-(x+y)} \; dx \; dy = 0.074
> $$

> [!Example] Example: Joint Probability Distribution (2)
> In a study on workers, the hours $X$ spent using their phones, and the hours $Y$ spent on their job is approximated by the joint pdf
> $$
> f(x,y) = xy e^{-(x+y)} \qquad x,y > 0
> $$
>
> What is the probability a person spends at least twice as much time on their phone than doing their job?
>
> To find this, we want to find $P(X \ge 2Y)$.
> $$
> P(X \ge 2Y) = \int_0^\infty \int_0^{X/2} xy e^{-(x+y)} \; dy dx
> $$

> [!Example]- Example: Joint Continuous Distributions - PDF to CDF
> $$
> f(x,y) = \begin{cases}
>               x + y & 0 < x < 1, 0 < y < 1 \\
>               0 & \text{else} 
>        \end{cases}
> $$
> Given the above joint continuous pdf, find the cdf of $X$ and $Y$.
>
> By virtue of multiple variables, we'll have to address numerous cases to find $F(x,y)$.
> 1. If $x,y \le 0$, then $F(x,y) = 0$.
> 2. If $x,y \ge 1$, then $F(x,y) = 1$.
> 3. If $0 < x,y < 1$,
>    $$
>    F(x,y) = \int_0^y \int_0^x (s + t) ds dt = \frac{1}{2} xy (x + y)
>    $$
> 4. If $x > 1, 0 < y < 1$,
>    $$
>    F(x,y) = \int_0^y \int_0^1 (s + t) ds dt = \frac{1}{2} (y) (y + 1)
>    $$
> 5. If $y > 1$, $0 < x < 1$,
>    $$
>    F(x,y) = \frac{1}{2} (x) (x + 1)
>    $$
>
> Putting these cases together, we find cdf
> $$
> F(x,y) = \begin{cases}
>               0 & x,y \le 0 \\
>               \frac{1}{2} xy (x + y) & 0 < x, y < 1 \\
>               \frac{1}{2} y (y + 1) & 0 < y < 1, x > 1 \\
>               \frac{1}{2} x (x + 1) & 0 < x < 1, y > 1 \\
>               1 & 1 \le x,y
>        \end{cases}
> $$

# Conditional Distributions and Independence
If $f(x,y)$ is the joint pdf of a random variable, then the **marginal distribution** of $X$, denoting the total probability of $x$ occurring over all cases $y$, is given as
$$
g_X (x) =
\begin{cases}
        &\sum_y f(x,y) &\text{Discrete Case} \\
        &\int_{-\infty}^\infty f(x,y) \; dy &\text{Continuous Case}
        
\end{cases}
$$
> The marginal distribution of $Y$ follows similarly.

Note that in a marginal distribution, we sum / integrate over the **other** variable. 

Now, given joint pdf $f(x,y)$ and marginal distribution of $Y$ $g_Y (y)$, we can find the **conditional distribution** of $X$ given $Y = y$ as
$$
f(x | y) = \frac{f(x,y)}{g_Y (y)} \qquad y_Y (y) \ne 0
$$
> This definition is analogous to the definition of conditional probability in the one-variable case.

Similarly, the **cumulative conditional distribution** of $X$ given $Y = y$ is given as
$$
F(x | y) = P( X \le x | Y = y ) =
\begin{cases}
        &\sum_{a\le x} f(a \mid y) &\text{Discrete Case} \\
        &\int_{-\infty}^x f(t \mid y) \; dt &\text{Continuous Case}
\end{cases}
$$
> Note that for the cumulative conditional distribution, $y$ is fixed.


> [!Example]+ Example: Joint Conditional Distributions
> Let the joint pdf of $X$ and $Y$ be given as
> $$
> f(x,y) = \begin{cases}
>          \frac{2}{3} (x + 2y) & 0 < x, y < 1 \\
>          0 & \text{else}
>        \end{cases}
> $$
>
> Find $P(X \le 1/2 | Y = 1/2)$.
>
> First, we find the marginal pdf as
> $$
> g_Y (y) = \int_{-\infty}^\infty f(x,y) dx = \int_0^1 f(x,y) dx = \frac{1}{3} (1 + 4y)
> $$
>
> and use this to find $f(x \mid y)$ as
> $$
> \begin{align*}
>       f(x|y) &= \frac{f(x,y)}{g_Y(y)} \\ 
>       &= \frac{\frac{2}{3} (x + 2y)}{\frac{1}{3} (1 + 4y)} \\
>       \to f\left(x \mid \frac{1}{2} \right) &= \frac{2x + 2}{3}
> \end{align*}
> $$
>
> Finally, we use this to find our answer as
> $$
> P(X \le 1/2 | Y = 1/2) = \int_{-\infty}^x f\left(t \mid \frac{1}{2} \right) \; dt = \int_0^{1/2} \frac{2x + 2}{3} dx = \frac{5}{12} 
> $$

Let $X_1, X_2, \dots X_n$ be random variables, and let $g_i (X)$ be the marginal distribution of random variable $X_i$.

We say that random variables $X_1, X_2, \dots X_n$ are **independent** if and only if for all $(x_1, \dots, x_n)$ that $X_1, \dots, X_n$ take on, we have that
$$
f(x_1, \dots, x_n) = g_1 (x_1) g_2 (x_2) \dots g_n (x_n)
$$
In other words, the joint probability distribution of all of the variables equals the product of their marginal probability distributions.

It naturally follows from this that if $X$ and $Y$ are independent, then
$$
f(x | y) = \frac{f(x,y)}{g_Y (y)} = \frac{g_X (x) g_Y (y)}{g_Y (y)} = g_X (x)
$$
> This is the same as our one-variable case! It tells us that the conditioning of $Y$ does not affect our probability of $X$, if they are independent.

Consider the following examples for independence.

> [!Example]+ Example: Independence on Joint Distributions
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
> We find that $X$ and $Y$ are independent, as $g_X (x) \cdot g_Y (y) = f(x,y)$.
> $$
> \begin{align*}
>       g_X (x) &= \int_0^1 f(x,y) dy = 2x \\
>       g_Y (y) &= \int_0^1 f(x,y) dx = 6 (1-y) y \\
>       g_X (x) g_Y (y) &= 12xy (1 - y) = f(x,y)
> \end{align*}
> $$

Knowing independence can be highly useful, and simplify many computations. For example, it gives us an easy shortcut for evaluating combinations of random variables!

> [!Abstract] Theorem: Summation of Independent Random Variables
> Let $X, Y$ be independent random variables with pmf/pdfs given as $f_X (x), f_Y (y)$. Define $Z = X + Y$.
>
> Then, for the continuous case,
> $$
> f_Z (z) = \int_{-\infty}^\infty f_X (x) f_Y (z - x) dx
> $$
> Called the **convolution** of the two functions.

> [!Example]+ Example: Summation of Independent Random Variables
> Let $X \sim \text{Binom}(n,p)$ and $Y \sim \text{Binom} (m,p)$. Furthermore, let $X,Y$ be independent and assume
> $$
> f_X (t) = f_Y (t) = \begin{cases}
>         e^{-t} & t > 0 \\
>         0 & \text{else}
>     \end{cases}
> $$
>
> What is the pdf of random variable $Z = X + Y$?
>
> We can find this using the convolution of $X$ and $Y$.
> $$
> \begin{align*}
>       f_Z (z) &= \int_{-\infty}^\infty f_X (x) f_Y (z - x) dx \\
>       &= \int_0^z e^{-x} e^{-(z-x)} dx \\
>       &= z e^{-z}
> \end{align*}
> $$
> 
> Note that we can only do this because our random variables are independent of one another.

# Transformations of Joint Distributions
Recall in the one-variable case, that for random variable $X$ with pdf $f_X (x)$, and random variable $Y = g(X)$, we can find the pdf of $Y$ as
$$
f_Y (y) = f_X ( g^{-1} (y) ) \cdot \frac{d}{dy} ( g^{-1} (y) )
$$

Let's generalize this fact to multiple variables. Given joint pdf $f_{X,Y} (x,y)$ and random variables $u = h_1 (x,y)$ and $v = h_2 (x,y)$, how do we find the joint pdf of $u$ and $v$?

Assuming that the partial derivatives exist, and that $h_1 (x,y)$ and $h_2 (x,y)$ are one-to-one, **we can perform a change in variables to find our pdf** (similar to multivariable calculus). This gives us the following theorem:

> [!Abstract] Theorem: Transforming Joint Distributions
> Let $X,Y$ be random variables with joint pdf $f_{X,Y} (x,y)$ and let there be random variables
> $$
> U = h_1 (X,Y) \qquad V = h_2 (X,Y)
> $$
>
> Then, the joint pdf of $U$ and $V$, $f_{U,V} (u,v)$, is given as
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
> > Which can be helpful if $J^{-1}$ evaluates to a constant.

Consider the following examples.

> [!Example]+ Example: Transforming Joint Distributions
> Let the joint pdf of random variables $X,Y$ be given as
> $$
> f(x,y) = \begin{cases}
>          e^{-(x+y)} & x,y > 0 \\
>          0 & \text{else}
>        \end{cases}
> $$
>
> Find the joint pdf of random variables $U,V$ where
> $$
> U = X + Y, V = \frac{X}{X + Y}
> $$
>
> First, we solve for $x,y$ in terms of $u,v$.
> $$
> x = uv \qquad y = u - uv
> $$
> 
> We can use this perform a change of variables using our theorem. 
> $$
> J(u,v) = \text{det} \begin{bmatrix}
>     \partial x / \partial u & \partial x / \partial v \\
>     \partial y / \partial u & \partial y / \partial v
>   \end{bmatrix} = 
> \begin{vmatrix}
>        v & u \\ 1-v & -u
>        \end{vmatrix} = -u
> $$ 
> $$
> f_{U,V} (u,v) = f_{X,Y} (uv, u - uv) \vert -u \vert = u e^{-u} \qquad 0 < u, 0 < v < 1
> $$

# Expectation and Variance
Let $X,Y$ be random variables. If $f(x,y)$ is their pdf, then the expected value of some combination of $X$ and $Y$, given as $g(x,y)$ is given as
$$
E(g(x,y)) =
\begin{cases}
        \sum_x \sum_y g(x,y) \cdot f(x,y) & \text{Discrete Case} \\
        \int_{-\infty}^\infty \int_{-\infty}^\infty g(x,y) \cdot f(x,y) \; dy \; dx & \text{Continuous Case}
\end{cases}
$$
Provided the values exist.

> [!Abstract] Theorem: Linearity of Expectation
> Let $c_1, \dots c_n$ be constants, and $X_1, \dots X_n$ be random variables. Then,
> $$
> E \left( \sum_{i=1}^n c_i g_i (x_1, \dots, x_n) \right) = \sum_{i=1}^n c_i E( g_i (x_1, \dots, x_n) )
> $$
>
> In particular, we can apply this theorem for $X$ and $Y$ on $c_1$ and $c_2$, to find
> $$
> E(X + Y) = E(X) + E(Y)
> $$

> [!Example]+ Example: Expectation
> Let $X$ and $Y$ be random variables with pdf $f(x,y)$ given as
> $$
> f(x,y) =
> \begin{cases}
>       \frac{2}{7} (x + 2u) & 0 < x < 1, 1 < y < 2 \\
>       0 & \text{else}
> \end{cases}
> $$
>
> We can find the expectation of some combination of $X$ and $Y$, say, $g(x,y) = X / Y^3$.
>
> $$
> E \left( \frac{X}{Y^3} \right) = \int_1^2 \int_0^1 \left( \frac{X}{Y^3} \right) \frac{2}{7} (x + 2y) dx dy = \frac{10}{56}
> $$

Recall that if $X,Y$ are independent, then $f_{X,Y} (x,y) = f_X (x) f_Y (y)$. Supposing that $X,Y$ are independent, we find that
$$
\begin{align*}
	E(XY)
	&= \int_{-\infty}^\infty \int_{-\infty}^\infty xy f_{X,Y} (x,y) \\
	&= \int_{-\infty}^\infty \int_{-\infty}^\infty xy f_X (x) f_Y (y) dy dx \\
	&= \int_{-\infty}^\infty x f_X (x) dx \int_{-\infty}^\infty y f_Y (y) dy \\
	&= E(X) \cdot E(Y)
\end{align*}
$$

This is formalized in the following theorem.

> [!Abstract] Theorem: Independence and Expectation
> If $X,Y$ are independent, then
> $$
> E(XY) = E(X) \cdot E(Y)
> $$

Note that this does not, however, imply the converse. In other words, $E(XY) = E(X) \cdot E(Y)$ does not necessarily mean $X$ and $Y$ are independent.

When $X$ and $Y$ are not independent, we can measure their relationship with one another. One measure that may help in doing this is the **covariance**, denoted $\text{Cov}(X,Y)$.
$$
Cov(X,Y) = E((X - E(X)) (Y - E(Y))) = E( (X - \mu_x) (Y - \mu_y) )
$$
> $Cov(X,Y)$ is seen as a measure of the linear relationship of $X$ and $Y$.

The covariance tells us the direction of the relationship between $X$ and $Y$.
1. If covariance is negative, then $X$ and $Y$ have a negative relationship (as $X$ increases, $Y$ decreases)
2. If covariance is positive, then $X$ and $Y$ have a positive relationship (as $X$ increases, $Y$ increases)

> [!Abstract] Theorem: Covariance
> $$
> Cov(X,Y) = E(XY) - E(X) E(Y)
> $$
>
> > [!Note]- Proof
> > $$
> > \begin{align*}
> >     E( (X - E(X)) (Y - E(Y)) )
> >        &= E(XY - E(X) Y - X E(Y) + E(X) E(Y) ) \\
> >        &= E(XY) - E(X) E(Y) - E(X) E(Y) + E(X) E(Y) \\
> >        &= E(XY) - E(X) E(Y)
> > \end{align*}
> > $$

It follows from this theorem that if $X$ and $Y$ are independent, then $Cov(X,Y) = 0$ (they are uncorrelated). Other properties of our covariance are given below:
- $Cov(X,X) = V(X)$
- $Cov(X,Y) = Cov(Y,X)$
- $Cov(kX, Y) = kCov(X,Y)$

We can further use covariance to define **correlation coefficient** of $X$ and $Y$ as
$$
\mathcal{P}_{X,Y} = \frac{Cov(X,Y)}{\sqrt{V(X)V(Y)}}
$$
measuring the "power" of the relationship - or in other words, how related $X$ and $Y$ are.

Properties of the correlation coefficient are given below.
1. $-1 \le \mathcal{P}_{X,Y} \le 1$
2. $\mathcal{P}_{X,Y} = \pm 1$ if and only if $Y = \alpha X + \beta$, for some $\alpha, \beta \in \mathbb{R}$.


# Conditional Expectation
Let $X$ and $Y$ be random variables, and let $g(X)$ be a function on random variable $X$.

Then, the **conditional expectation** of $g(X)$ given $Y = y$ is defined as
$$
E( g(x) \mid y ) =
\begin{cases}
        &\sum_x g(x) f(x \mid y) &\text{Discrete Case} \\
        &\int_{-\infty}^\infty g(x) f(x \mid y) \; dx &\text{Continuous Case}
\end{cases}
$$

In particular, if $g(x)$ is given as $x^i$, then we define the **conditional $i^{th}$ moment** as $E(x^i | y)$. We can use this to define the following:
$$
\begin{align*}
       &E(X \mid Y) &\text{Conditional Mean} \\
       &V(X \mid Y) = E(X^2 | Y) - E(X | Y)^2 &\text{Conditional Variance}
\end{align*}
$$

We also have the following properties:

> [!Abstract] Theorem: Conditional Expectation and Expectation / Variance
> The following two equalities are true.
> $$
> \begin{align*}
>       &E(X^i) = E( E(X^i \mid Y) ) \\
>       &V(X) = V(E(X \mid Y)) + E(V(X \mid Y)) \\
> \end{align*}
> $$
>
> We prove them below.
>
> 
> > [!Note]- Proof (1)
> > 
> > First, define function $h(Y)$ as
> > $$
> > \begin{align*}
> >         h(Y)
> >         &= E(X^i \mid Y = y) \\
> >         &= \int_{-\infty}^\infty x^i f(x \mid y) dx \\
> >         &= \int_{-\infty}^\infty x^i \frac{f(x,y)}{g_Y(y)} dx
> > \end{align*}
> > $$
> > 
> > We want to use this to show that $E(X^i) = E(h(Y))$.
> > $$
> > \begin{align*}
> >         E( h(Y) )
> >         &= \int_{-\infty}^\infty h(y) g_Y (y) dy \\
> >         &= \int_{-\infty}^\infty \left[ \int_{-\infty}^\infty x^i \frac{f(x,y)}{g_Y(y)} dx \right] g_Y (y) dy \\
> >         &= \int_{-\infty}^\infty \left[ \int_{-\infty}^\infty x^i f(x,y) dx \right] dy
> > \end{align*}
> > $$
> > 
> > Here, we apply the definition of conditional probability (multivariate case)
> > $$
> > f(y \mid x) = \frac{f(x,y)}{g_X (x)}
> > $$
> > 
> > $$
> > \begin{align*}
> >         &\int_{-\infty}^\infty \left[ \int_{-\infty}^\infty x^i f(x,y) dx \right] dy \\
> >         &= \int_{-\infty}^\infty \int_{-\infty}^\infty x^i g_X(x) f(y \mid x) dx dy \\
> >         &= \int_{-\infty}^\infty \int_{-\infty}^\infty x^i g_X(x) f(y \mid x) dy dx \\
> >         &= \int_{-\infty}^\infty x^i g_X(x) \left[ \int_{-\infty}^\infty f(y \mid x) dy \right] dx \\
> >         &= \int_{-\infty}^\infty x^i g_X(x) (1) dx = E(X^i)
> > \end{align*}
> > $$
>
> > [!Note]- Proof (2)
> >
> > We start from the right-hand side expression, and find that
> > $$
> > \begin{align*}
> >         V(E (X \mid Y)) + E(V(X \mid y))
> >             &= E( E(X \mid Y)^2  - E ( E(X \mid Y) ))^2 \\
> >                &\quad + E(E(X^2 \mid Y) - (E(X \mid Y))^2) \\
> >             &= E( E(X \mid Y)^2 ) - [ E(X) ]^2 \\
> >                &\quad + E( E(X^2 \mid Y)) - E (E (X \mid Y) )^2 \\
> >             &= E(X^2) - (E(X))^2 = V(X)
> > \end{align*}
> > $$

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

> [!Example]+ Example: Conditional Expectation
> Suppose that
> $$
> P(y = 1) = \frac{1}{8} \qquad P(y = 2) = \frac{7}{8}
> $$
> 
> Now suppose we have random variable $Z = X \mid Y$, and define
> $$
> P(z = 2y) = \frac{3}{4} \qquad P(z = 3y) = \frac{1}{4}
> $$
> 
> On the cases $y = 1, 2$, then
> $$
> Z = X \mid (Y = 1) =
>   \begin{cases}
>         2(1) & P = 3/4 \\
>         3(1) & P = 1/4 \\
>   \end{cases}
> \qquad
> Z = X \mid (Y = 2) =
>   \begin{cases}
>         2(2) & P = 3/4 \\
>         3(2) & P = 1/4 \\
>   \end{cases}
> $$
> 
> We use this to find expected values
> $$
> \begin{align*}
>     &E(X \mid Y = 1) = 2 \cdot \frac{3}{4} + 3 \cdot \frac{1}{4} = \frac{9}{4} \\
>     &E(X \mid Y = 2) = 4 \cdot \frac{3}{4} + 6 \cdot \frac{1}{4} = \frac{18}{4}
> \end{align*}
> $$
> 
> This gives us the expected value distribution
> $$
> E(X \mid Y) =
>     \begin{cases}
>         9/4 & y = 1 \\
>         18/4 & y = 2
>     \end{cases}
> $$
> 
> We can then use this to find $E (E(X \mid Y)) = E(X)$!
> $$
> \begin{align*}
>         E(X) &= E(E (X \mid Y)) \\
>         &= \frac{9}{4} P(y = 1) + \frac{18}{4} P(y = 2) = \frac{9}{4} \cdot \frac{1}{8} + \frac{18}{4} \cdot \frac{7}{8}
> \end{align*}
> $$

> [!Example]- Example: Conditional Expectation (2)
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
> Given that
> $$
> g_Y (y) = \frac{2}{(y + 1)^3}
> $$
> 
> We can find $E(X \mid Y)$ by finding
> $$
> \begin{align*}
>         E(X \mid Y)
>             &= \int_{-\infty}^\infty x f(x \mid y) dx \\
>             &= \int_0^\infty x x \left( \frac{x^2 e^{-x (y+1)}}{g_Y (y)} \right) \\
>             &= \int_0^\infty \frac{1}{2} (y + 1)^3 x^3 e^{-x (y + 1)} dx
> \end{align*}
> $$
> 
> Let $u = x (y + 1) \to du = y + 1$. We find
> $$
> E(X \mid Y) = \frac{1}{2 (y+1)} \int_0^\infty u^3 e^{-u} du = \frac{1}{2(y+1)} \Gamma(4) = \frac{3!}{2(y+1)}
> $$

Sometimes, we can use conditional expectation to find expected values that are recursively defined in terms of themselves. See the following examples.

> [!Example]+ Example: Conditional Expectation (3)
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
> Note that we express $E(X)$ recursively in terms of itself, as if the man enters tunnel 2 or 3, he ends up back where he started but with additional time spent.
>
> Solving for $E(X)$, we find $E(X) = 14$. 

> [!Example]- Example: Conditional Expectation (4)
> A biased coin has $P(\text{Heads}) = p$. We toss the coin until we get 2 consecutive heads. What is the number of expected tosses?
> 
> Let:
> 1. $A_1$ be the event of the sequence $H,H$.
> 2. $A_2$ be the event of the sequence $H,T$.
> 3. $A_3$ be the event of the sequence of just $T$.
> 
> As $A_1, A_2, A_3$ partition the sample space of the toss sequences, we can find our expected value by breaking it up across these different sequences.
>
> Define $X$ as the total number of tosses needed until we get 2 consecutive heads. Then,
> $$
> \begin{align*}
>         E(X)
>         &= E(X \mid A_1) P(A_1) + E(X \mid A_2) P(A_2) + E(X \mid A_3) P(A_3) \\
>         &= 2 \cdot p^2 + (2 + E(X)) \cdot p (1 - p) + (1 + E(X)) \cdot (1 - p)
> \end{align*}
> $$
>
> Solving for $E(X)$, we find $E(X) = \frac{p+1}{p^2}$.
