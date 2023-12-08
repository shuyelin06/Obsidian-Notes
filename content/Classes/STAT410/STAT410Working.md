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

---

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

---
Big Picture: The observed mean ("sample mean") converges to the expected value as the number of trials increase.

> [!Example]
> Flip a coin. If it has heads, place a blue chip in a box. Otherwise, place a red chip in the box. Let $X_i$ be the random variable of the number of blue chips added to the box for trial $i$, namely,
> $$
> X_i =
> \begin{cases}
>         1 & \text{heads} \\
>         0 & \text{tails}
> \end{cases} 
> $$
> 
> Clearly, we know that $\mu = 1/2$. However, if we test, say 4 times, we may not get this expected value! As we increase the number of tests, we should naturally expect this average to converge to the expected value.

The law of large number is broken up into two distinct cases - the **weak law** and the **strong law** of large numbers.

> [!Abstract] Theorem: Weak Law of Large Numbers (WLLN)
> If $X_1, X_2, \dots X_n$ are independent, identically distributed random variables, then
> $$
> \lim_{n\to\infty} P( |\bar{X}_n - \mu | < \epsilon) = 1
> $$
> 
> In other words, $X_n$ converges in probability to $\mu$.
>
> > [!Note] Proof
> >
> > We will show that
> > $$
> > \lim_{n\to\infty} P(|\bar{X}_n - \mu| > \epsilon) = 0
> > $$
> > to show that the contrapositive is true.
> > 
> > $$
> > \lim_{n\to\infty} P(|\bar{X}_n - \mu| > \epsilon) = \lim_{n\to\infty} P(|\bar{X}_n - \mu|^2 > \epsilon^2)
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

> [!Example]
> Let $X$ be the Bernoulli random variable
> $$
> X =
> \begin{cases}
>         1 & \text{Success} \\
>         0 & \text{Failure}
> \end{cases}
> $$
> 
> Let $X_i$ be the value of $X$ at trial $i$, and $\bar{X}_n$ be the "average successes".
> $$
> \bar{X}_n = \frac{X_1 + X_2 + \dots + X_n}{n}
> $$
> 
> By the Weak Law of Large Numbers, we know that $\bar{X}_n \to^P E(X)$, and we know by the Bernoulli Distribution, $E(X) = p$. Thus, the rate at which we see a success will gradually approach the probability of a success (which makes sense!).

> [!Example]
> Using the Weak Law of Large Numbers, we can prove the following theorem.
> 
> > [!Abstract] Theorem: Bernstein's Theorem
> > 
> > If $f(x)$ is continuous on $[a,b]$, then for any $\epsilon > 0$, there exists a polynomial $h(x)$ such that
> > $$
> > |f(t) - h(t)| < \epsilon 
> > $$
> > for all $t \in [a,b]$.
> >
> > In other words, we can approximate any continuous function (on an interval) with a polynomial.


> [!Abstract] Theorem: Strong Law of Large Numbers (SLLN)
> If $X_1, X_2, \dots X_n$ are independent, identically distributed random variables, then
> $$
> P \left( \lim_{n\to\infty} | \bar{X}_n - \mu | < \epsilon \right) = 1
> $$
>
> In other words, $\bar{X}_n$ converges almost surely to $\mu$.
> > Note that the Strong Law of Large Numbers also implies the Weak Law!


# 8.4: Sampling and the Central Limit Theorem
A sequence of random variables $X_1, X_2 \dots X_n$ **converges in distribution** to random variable $X$, denoted $X_n \to^d X$, if the cdfs satisfy
$$
\lim_{n\to\infty} F_{X_n} (x) = F_X (x)
$$
for all $x$ where $x$ is continuous.

> [!Example] Example: Convergence of Distributions
> $$
> X_n =
> \begin{cases}
>         1 & s = 1 \\
>         0 & s = 0
> \end{cases} \qquad
> X =
> \begin{cases}
>         1 & s = 0 \\
>         0 & s = 1
> \end{cases}
> $$
> 
> Now, because
> $$
> \lim_{n\to\infty} P( |X_n - X| < \epsilon ) \ne 1
> $$
> we know that $X_n \not\to^P X$.
> 
> However, assuming that the probability of $s$ occurring is uniformly distributed, we see that
> $$
> F_{X_n} =
> \begin{cases}
>         1/2 & 0 \le x < 1 \\
>         1 & x \ge 1
> \end{cases} = F_X
> $$
> Thus, $X_n \to^d X$.

If $X_1, X_2, \dots X_n$ are independent, identically distributed random variables, we say they constitute a **random sample** from an **infinite** population.

A **statistic** is a value calculated using this random sample (not the population). The process of calculating these statistics is known as **statistical inference**!

If $X_1, X_2, \dots X_n$ is a random sample, the **sample mean** and **sample variance** are respectively defined as
$$
\bar{X} = \frac{1}{n} \sum_{i=1}^n X_i \qquad s^2 = \frac{1}{n-1} \sum_{i=1}^n (X_i - \bar{X})^2
$$
> The unintuitive $n - 1$ in the sample variance is known as **Bessel's Correction**, and occurs as a sort of a "correction" as $X_i - \bar{X}$ is smaller than $X_i - \mu$.


> [!Abstract] Theorem:
> If $X_1, X_2 \dots X_n$ is a random sample from an infinite population with mean $\mu$ and variance $\sigma^2$, then
> $$
> E(\bar{X}) = \mu \qquad V(\bar{X}) = \frac{\sigma^2}{n}
> $$

Now, given a statistic from a sample of size $n$, we are essentially defining a function for it given the random variables $X_1, \dots X_n$. 
$$
Y = g(X_1, \dots X_n)
$$
We can thus think of this function $Y$ as its own random variable!

We then ask, what is the distribution of $Y$?

> [!Example]
> Let $X_i \sim \text{Gamma}(\alpha, \beta)$, and consider the statistic
> $$
> T = \sum_{i=1}^n X_i
> $$
>
> We showed in a previous example that $T \sim \text{Gamma}(n\alpha, \beta)$. Moreover, to find the distribution of $\bar{X} = \frac{T}{n}$, we find
> $$
> M_{\bar{X}} (t) = M_T \left( \frac{T}{n} \right) = \left( \frac{\beta}{1 - \beta t / \alpha} \right)^{n\alpha} \to \bar{X} \sim \text{Gamma}(n \alpha, \beta / n)
> $$
> But given a small manipulation in this random variable, our distribution quickly becomes a mess! For example, it's difficult to find the distribution of $Y = \bar{X} + a$, as its moment generating function doesn't match any commonly known distribution!

The **Central Limit Theorem** provides a convenient way to approximate some of the above distributions!

> [!Abstract] Theorem: Central Limit Theorem
> Let $X_1, X_2, \dots X_n$ be a sequence of independent, identically distributed random variables with mean $\mu$, variance $\sigma^2$ and moment generating function $M_x (t)$.
> 
> Then, if we define the distribution of their averages $\bar{X}$,
> $$
> \bar{X} = \frac{X_1 + X_2 + \dots + X_n}{n}
> $$
> Then the distribution $\bar{X}$ converges in distribution to the standard normal distribution! 
> $$
> \frac{(\bar{X} - \mu)}{\sigma / \sqrt{n}} \to^d N(0,1)
> $$
>
> Equivalently,
> $$
> \lim_{n\to\infty} P \left( \frac{\bar{X} - \mu}{\sigma / \sqrt{n}} < a \right) = \int_{-\infty}^a \frac{1}{\sqrt{2\pi}} e^{-x^2 / 2} \; dx
> $$
> Or in other words, multiplying both top and bottom by $n$, we obtain
> $$
> \lim_{n\to\infty} P \left( \frac{X_1 + X_2 + \dots + X_n - n \mu}{\sigma \sqrt{n}} < a \right) = \int_{-\infty}^a \frac{1}{\sqrt{2\pi}} e^{-x^2 / 2} \; dx
> $$
> > This is often more useful, as we are often more interested in some probability from the summation $X_1 \dots X_n$ itself, rather than their average.
>
> > [!Note]- Proof
> >
> > For the sake of simplicity, we will assume the variance is finite and use moment generating functions - however, there exist generalizations for non-fininte variances too!
> > 
> > > [!Abstract] Theorem
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

Given a statistic, the Central Limit Theorem tells us that its averages (given our sample size is sufficiently large) will become the normal distribution!

> [!Example]
> From the earlier example, $Y = \bar{X} + a$ had a moment generating function given as
> $$
> M_Y (t) = e^{at} \left( \frac{1}{1 - \beta t / n} \right)^{n \alpha}
> $$
> If we know that $\bar{X}$ is approximately the normal distribution, then we can find that $\bar{X} + a$ is approximately
> $$
> N \left(\mu + a, \frac{\sigma^2}{n} \right)
> $$

> [!Example]
> The amount of nicotine in a cigarette can be expressed by a random variable  with mean $\mu = 0.8$ mg, and standard deviation $\sigma = 0.1$ mg. Suppose there are 20 cigarettes in one pack. 
> 
> If a person smokes 5 packs of cigarettes a week, what is the probability the total nicotine consumed in a week is at least 82 mg?
> 
> Because we have 20 cigarettes over 5 packs, we'll have 100 total cigarettes. Let $X_i$ denote the amount of nicotine in cigarette $i$. If
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

> [!Example]
> In a sample of 25 people, their height is measured. We find $\bar{X} = 67.64$ inches (note that this is the sample mean). Now suppose the population variance is $\sigma^2 = 9$.
> 
> Use the Central Limit Theorem to find the probability that $\mu$ exceeds 70 inches.
> 
> Here, if $\mu = 70$, we see that
> $$
> Z = \frac{\bar{X} - \mu}{\sigma / \sqrt{n}} = \frac{67.64 - 70}{3 / \sqrt{25}} \approx -3.266
> $$
> As $\mu$ increases, this will only become more negative, so we want to know the probability that $P(Z < -3.266) = \Phi(-3.266) = 0.00056$.

Observe that in many situations, we start with a discrete random variable, and approximate it with $N(0,1)$, a continuous random variable. Under this conversion from discrete to continuous, it's most ideal to use a **continuity correction** to account for any error from conversions, where
$$
P(X = i) \approx P(i - 1/2 < X < i + 1/2)
$$
> Note that this correction is applied on $X$, and is most particularly effective for integers. 

> [!Example] 
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

# 8.5: Contelli and Jensen's Inequality
Recall Markov's Inequality
$$
P(X \ge a) \le \frac{E(X)}{a}
$$

Using this inequality, we can derive another known as **Contelli's Inequality**.

> [!Abstract] Theorem: Contelli's Inequality (One-Sided Chebyshev)
> If $a > 0$, then
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

 > [!Example]
 An exam had average 75% and a variance of 8%. Find an upper bound on the probability a student had at least an 80%.
> 
> Using Contelli's Inequality, we have that
> $$
> \begin{align*}
>         P(X \ge 80)
>         &= P(X - 75 \ge 5) \\
>         &\le \frac{8^2}{8^2 + 5^2} \approx 0.72
> \end{align*}
> $$

A twice differentiable function $g(x)$ is **convex** if $g''(x) > 0$. Equivalently for all $t$, $0 \le t \le 1$, and $x_1, x_2$, we have
$$
g(tx_1 + (1 - t)x_2) \le tg(x_1) + (1-t) g(x_2)
$$
> This is essentially saying, all values between $x_1$ and $x_2$ are at most the line formed between $g(x_1)$ and $g(x_2)$.

We say $g(x)$ is **concave** if $-g(x)$ is convex.

> [!Abstract] Theorem: Jensen's Inequality
> If $g(x)$ is a convex function, then
> $$
> E(g(X)) \ge g(E(X))
> $$
>
> > [!Note] Proof
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
> >         &E(g(X)) \ge E(g(\mu) + g'(\mu) (x - \mu)) \\
> >         &E(g(X)) \ge E(g(\mu)) + E( g'(\mu) (x - \mu)) \\
> >         &E(g(X)) \ge g(\mu) + g'(\mu) E(x - \mu) \\
> >         &E(g(X)) \ge g(\mu) + g'(\mu) ( E(X) - \mu ) \\
> >         &E(g(X)) \ge g(\mu) + 0 \\
> >         &E(g(X)) \ge g(E(X))
> > \end{align*}
> > $$


> [!Example]
> Let $g(x) = \sqrt{x}$. Notice how $g''(x) = - \frac{1}{4} x^{-3/2} < 0$ for all $x > 0$, telling us that this function is concave.
>
> Thus, we know that $h(x) = \sqrt{x}$ is convex. By Jensen's Inequality,
> $$
> E( -\sqrt{x} ) \ge - \sqrt{ E(X) } \quad \Longrightarrow \quad E(\sqrt{x}) \le \sqrt{E(X)}
> $$
>
> Thus, in general, if $g(X)$ is concave, then $E(g(x)) \le g(E(X))$.

> [!Example]
> Let $g(x) = x^2$.
>
> By Jensen's Inequality, $E(X^2) \ge (E(X))^2$, so
> $$
> V(X) = E(X^2) - (E(X))^2 \ge 0
> $$

Let $a_i > 0$. Then, we have the following
$$
\begin{align}
        &\frac{1}{n} \sum_{i=1}^n a_i &\text{Arithmetic Mean} \\
        &\sqrt[n]{\prod_{i=1}^n a_i} &\text{Geometric Mean} \\
        &\frac{n}{\sum_{i=1}^n \frac{1}{a_i}} &\text{Harmonic Mean}
\end{align}
$$

> [!Example]
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

> [!Abstract] Theorem
> It is always the case that
> $$
> \text{Harmonic Mean} \le \text{Geometric Mean} \le \text{Arithmetic Mean}
> $$
>
> > [!Note] Proof
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


> [!Example]
> Let $X$ be a random variable taking on values greater than -1. Assume $E(X) = 100$. Apply Jensen's Inequality to obtain a bound on $E(\frac{1}{1 + X})$.
>
> Let $g(x) = \frac{1}{1 + x}$. We know that $g''(x) = \frac{2}{(x + 1)^3} > 0$ for all $x > -1$.
>
> Then, applying Jensen's Inequality, it must be true that
> $$
> E \left( \frac{1}{1 + X} \right) \ge \frac{1}{1 + (100)}
> $$

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

---

Now say we have $n = 2$, with
$$
p_1 = \frac{1}{p} \quad p_2 = \frac{1}{q} \quad p_1 + p_2 = 1
$$
and
$$
a_1 = c^p \qquad a_2 = d^q
$$
where $c,d$ are non-negative. We apply our above findings and obtain

$$
\begin{align*}
        c^{p/p} d^{q/q} &\le \frac{1}{p} c^p + \frac{1}{q} d^q \\
        c \cdot d &\le \frac{c^p}{p} + \frac{d^q}{q}
\end{align*}
$$

Which is known as **Young's Inequality**.

Now choose
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
Which is Holder's Inequality!


---

Final Exam Content to Know:
- Markov's Inequality
- Chebyshev's Inequality (both cases $k = c \sigma$)
- Definition of convergence in probability and in distribution
- Central Limit Theorem (don't need anything leading up to it, just the theorem itself, NO TAYLORS THEOREM NEEDED, NO CONTINUITY CORRECTION)
- Jensen's Inequality

No need to know pdfs for discrete / continuous, expectation / variance for these.

Defo have 1,2,4,5 deeply memorized.

Larger part of the 1st half of the final is joint distributions.

Main Focus of the final will be on (5.3) transformations in 1 Variable, and on joint distributions, the next section. Before 5.3, know counting (1.1), Bayes' Theorem (3.2), properties of E(X) and V(X). Know geometric series formula, series expansion for $e^x$.
> Like only 25% of the final will be on material before 5.3 (transformations in 1 variable).
