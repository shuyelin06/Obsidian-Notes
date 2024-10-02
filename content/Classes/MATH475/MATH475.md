---
title: MATH475
tags:
- math475
---

Combinatorics and graph theory

- [[Counting and Enumeration]]

---

# Section 2: Generating Functions
## 2.1, 2.2: Power Series Review, Intro to Ordinary Generating Functions
A **formal power series** is an infinite sum 
$$
\sum_{n=0}^\infty a_n x^n
$$
whose coefficients represent a sequence $\{a_n\}$.

The function $F(x) = \sum_{n=0}^\infty a_n x^n$ is the **ordinary generating function** of $\{a_n\}_{n=0}^\infty$, sometimes denoted the OGF.
> These functions are quite interesting! Oftentimes, we can manipulate these functions into something else that we can recognize.

> [!Example]+ Example: Ordinary Generating Functions of Sequences
> Let $\{a_n\}$ be given by
> $$
> \frac{1}{2!}, \frac{1}{3!}, \frac{1}{4!}, \dots
> $$
> 
> What is $F(x)$?
> 
> We can find $F(x)$ as
> $$
> \begin{align*}
> F(x) &= \frac{1}{2!} + \frac{1}{3!} x + \frac{1}{4!} x^2 + \dots \\
> &= \frac{1}{x^2} \left( \frac{1}{2!} x^2 + \frac{1}{3!} x^3 + \dots \right) \\
> &= \frac{1}{x^2} (e^x - x - 1)
> \end{align*}
> $$

> [!Example]+ Example: Sequences of Ordinary Generating Functions
> Find $\{a_n\}$ if the OGF is
> $$
> F(x) = \frac{-4x + 3}{(1 - x)(1 - 2x)}
> $$
> 
> Note that our denominator looks like the output of a geometric series, but as a product! So, we apply partial fractions to get separate geometric series.
> 
> $$
> \begin{align*}
> \frac{-4x + 3}{(1 - x)(1 - 2x)} 
> &= \frac{A}{(1 - x)} + \frac{B}{(1 - 2x)} \\ 
> -4x + 3 
> &= A (1 - 2x) + B(1 - x) \\
> A = 1&, B = 2
> \end{align*}
> $$
> 
> So, we get
> $$
> \begin{align*}
> F(x) 
> &= \frac{-4x + 3}{(1 - x)(1 - 2x)} = \frac{1}{1 - x} + \frac{2}{1 - 2x} \\
> &= \sum_{n=0}^\infty x^n + 2 \sum_{n=0}^\infty (2x)^n \\
> &= \sum{n=0}^\infty (1 + 2^{n + 1}) x^n
> \end{align*}
> $$
> So we find our sequence to be
> $$
> \{a_n\} = \{1 + 2^{n+1}\}
> $$

Given a **recurrence**, say $a_n = a_{n-1} + a_{n-2}$ (the fibonacci recurrence) where we are given a term in terms of the previous ones, we can obtain the closed form OGF, and then use a series expansion to get an explicit closed form formula for our sequence $\{a_n\}$. 

> [!Info] Lemma
> We have
> $$
> h(x) = 1 - x - x^2 = - \left( x + \frac{1 + \sqrt{5}}{2} \right) \left( x + \frac{1 - \sqrt{5}}{2} \right)
> $$
> Moreover, if $r_1 = \frac{1 + \sqrt{5}}{2}$, $r_2 = \frac{1 - \sqrt{5}}{2}$, then $r_2 = -\frac{1}{r_1}$.

> [!Example]- Example: Closed Form Fibonacci Sequence
> $$
> a_n = a_{n-1} + a_{n-2} \qquad a_0 = 0, a_1 = 1
> $$
> 
> Find a closed form ogf for the sequence, and find a closed form for $a_n$ with it.
> 
> Our goal is first to find the closed form OGF.
> 
> We first start with the ogf, and then apply our sequence definition to the $a_n$ term. Note that we need to take out the base case as the definition for $a_n$ is only defined for $n \ge 2$.
> $$
> \begin{align*}
> F(x) 
> &= \sum_{n=0}^\infty a_n x^n = 0 + 1x + \sum_{n=2}^\infty a_n x^n \\
> &= x + \sum_{n=2}^\infty (a_{n-1} + a_{n-2}) x^n \\
> &= x + \sum_{n=2}^\infty a_{n-1} x^n + \sum_{n=2}^\infty a_{n-2} x^n \\
> &= x + x \sum_{n=2}^\infty a_{n-1} x^{n-1} + x^2 \sum_{n=2}^\infty a_{n-2} x^{n-2}
> \end{align*}
> $$
> We can use this to express $F(x)$ as a function of itself. Note that the first summation is $F(x)$ without the $a_0$ term, and the second summation is just $F(x)$.
> $$
> \begin{align*}
> F(x)
> &= x + x \sum_{n=2}^\infty a_{n-1} x^{n-1} + x^2 \sum_{n=2}^\infty a_{n-2} x^{n-2} \\
> &= x + x (F(x) - a_0) + x^2 F(x) \\
> &= x + x F(x) + x^2 F(x) \\
> F(x)
> &= \frac{x}{1 - x - x^2}
> \end{align*}
> $$
> We have found a closed form ogf. We can now use this to find our closed form sequence. We do this by applying partial fraction decomposition and converting the result into a geometric series.
> > Here, we apply our lemma.
> $$
> \begin{align*}
> F(x)
> &= \frac{x}{1 - x - x^2} \\
> &= \frac{-x}{\left( x + \frac{1 + \sqrt{5}}{2} \right) \left( x + \frac{1 - \sqrt{5}}{2} \right)} \\
> &= \frac{-x}{(x + r_1) (x + r_2)} = \frac{A}{x + r_1} + \frac{B}{x + r_2} \\
> &= \frac{-1}{\sqrt{5}} \left( \frac{r_1}{x + r_1} - \frac{r_2}{x + r_2} \right) \\
> &= \frac{1}{\sqrt{5}} \left( \frac{r_2}{x + r_2} - \frac{r_1}{x + r_1} \right) \\
> &= \frac{1}{\sqrt{5}} \left( \frac{1}{1 - (-x / r_2)} - \frac{1}{1 - (-x / r_1)} \right) \\ 
> &= \frac{1}{\sqrt{5}} \left( \sum_{n=0}^\infty (r_2 x)^n - \sum_{n=0}^\infty (r_1 x)^n \right) \\
> &= \sum_{n=0}^\infty \frac{1}{\sqrt{5}} (r_2^n - r_1^n) x^n 
> \end{align*}
> $$
> We've found our closed form sequence!
> $$
> \{a_n\} = \frac{1}{\sqrt{5}} (r_2^n - r_1^n) =  \frac{1}{\sqrt{5}} \left( \left( \frac{1 - \sqrt{5}}{2} \right)^n - \left(  \frac{1 + \sqrt{5}}{2} \right)^n \right)
> $$

> [!Example]- Example: Solving Recurrence Relations
> Consider codes of length $n$ using $A,B,C,D$. Let $a_n$ denote the total codes with an even number of $A$'s. 
> 1. Find a recurence of $a_n$ in terms of $a_{n-1}$
> 2. Find a closed form ogf.
> 3. Find a closed form for $a_n$.
> 
> We first find a recurrence. If we have $n - 1$ length strings, we could add a $B,C,D$ to get a $n$ length string. Or, with $n - 1$ length strings, we need an odd number of $A$'s to add an extra $A$ onto, which we can find as all strings minus the even ones.
> $$
> a_n = a_{n-1} + a_{n-1} + a_{n-1} + (4^{n-1} - a_{n-1}) = 2a_{n-1} + 4^{n-1}
> $$
> We now need to find our base case. Clearly, $a_1 = 3$, as the string can only be a $B,C,D$. So, $a_0 = 1$.
> 
> We now use our recurrence to find a closed form ogf.
> $$
> \begin{align*}
> F(x) 
> &= \sum_{n=0}^\infty a_n x^n = 1 + \sum_{n=1}^\infty a_n x^n \\
> &= 1 + \sum_{n=0}^\infty (2a_{n-1} + 4^{n-1}) x^n \\
> &= 1 + 2 \sum_{n=1}^\infty a_{n-1} x^n + \sum_{n=1}^\infty 4^{n-1} x^n \\
> &= 1 + 2 x \sum_{n=1}^\infty a_{n-1} x^{n-1} + x \sum_{n=1}^\infty 4^{n-1} x^{n-1} \\
> &= 1 + 2 x \sum_{n=1}^\infty a_{n-1} x^{n-1} + x \sum_{n=1}^\infty 4^{n-1} x^{n-1} \\
> &= 1 + 2x F(x) + x \frac{1}{1 - 4x} \\
> F(x) 
> &= \frac{1}{1 - 2x} \left(1 + \frac{x}{1 - 4x} \right) \\
> &= \frac{1}{1 - 2x} + \frac{x}{(1 - 4x) (1 - 2x)}
> \end{align*}
> $$
> 
> We now use our closed form ogf to find a closed form sequence.
> $$
> \begin{align*}
> F(x) 
> &= \frac{1}{1 - 2x} + \frac{x}{(1 - 4x) (1 - 2x)} \\
> &= \frac{1}{2(1 - 2x)} + \frac{1}{2(1 - 4x)} \\
> &= \frac{1}{2} \sum_{n=0}^\infty (2x)^n + \frac{1}{2} \sum_{n=0}^\infty (4x)^n \\
> &= \sum_{n=0}^\infty \frac{1}{2} (2^n + 4^n) x^n
> \end{align*}
> $$
> We found our closed form solution as
> $$
> \{a_n\} = \left\{ \frac{1}{2} (2^n + 4^n) \right\}
> $$


--- End of Exam 1 Content ---

## 2.3: Ordinary Generating Functions and Counting
What if $a_n$ is a combinatorial value, like $S(n,k)$? Well, using our techniques, we can actually find the closed form solution of $S(n,k)$ (at least in some cases)!

We describe various combinatorial objects that can be used to solve counting problems.

### Weak Compostions with Contraints
We have 
$$
\frac{1}{1-x} = \sum_{n=0}^\infty x^n
$$
Differentiating this, we get
$$
\begin{align*}
&\frac{1}{(1-x)^2} = \sum_{n=1}^\infty n x^{n-1} = 1 + 2x + 3x^2 + \dots = \sum_{n=0}^\infty (n+1) x^n \\
&\frac{2}{(1-x)^3} = \sum_{n=2}^\infty (n-1) x^{n-2} = \sum_{n=0}^\infty (n+2)(n+1) x^n \\
&\vdots
\end{align*}
$$
Generalizing this, we find that at the $m^{th}$ derivative,
$$
\begin{align*}
\frac{m!}{(1-x)^{m+1}} 
&= \sum_{n=0}^\infty (n+m)(n+m-1) \dots (n+1) x^n \\
&= \sum_{n=0}^\infty \frac{(n+m)!}{n!} x^n \\
\frac{1}{(1-x)^{m+1}}
&= \sum_{n=0}^\infty \frac{(n+m)!}{n! m!} x^n = \sum_{n=0}^\infty \binom{n+m}{m} x^n
\end{align*}
$$
Letting $m = k - 1$, we find 
$$
\frac{1}{(1-x)^k} \sum_{n=0}^\infty \binom{n+k-1}{k-1} x^n
$$
Now observe that
$$
\frac{1}{(1-x)^k} = \left( \frac{1}{1-x} \right)^k = (1 + x + x^2 + \dots) (1 + x + x^2 + \dots) \dots
$$
We can find that the coefficient of any $x^n$ is $\binom{n+k-1}{k-1}$! And in fact, our disgusting product can actually just be seen as all possible ways we can choose $x^{n_1}$ in group 1, $x^{n_2}$ in group 2, ... $x^{n_k}$ in group $k$ where 
$$
x^{n_1} x^{n_2} \dots x^{n_k} = x^{n_1 + n_2 + \dots n_k} = x^n
$$
Which is in fact weak compositions! With this relation, we can actually solve any weak composition problem (with any constraints)! 
> Each exponent represents one "dollar" we can give, and each series represents one entity we could give dollars to, where the series depends on the constraints we have!

> [!Example]+ Example: Model for Solving Weak Compositions
> Find the ordinary generating function and state the coefficient that would count the total ways to distribute $100 to 4 kids so that kid 1 gets at most 5 dollars, kid 2 gets at least 3 dollars, kid 3 gets an even number of dollars, and kid 4 gets any amount.
> 
> We want the coefficient of $x^{100}$ such that
> $$
> (1 + x + x^2 + x^3 + x^4 + x^5) (x^3 + x^4 + x^5 + \dots ) (1 + x^2 + x^4 + \dots) (1 + x + x^2 + x^3 + \dots)
> $$
> Each series is given in terms of the ways we can give dollars to each of the kids. For example because kid 2 gets at least 3 dollars, the series is $x^3, x^4, \dots$ as when we make a "choice" in our product, the exponent (dollars) we wantt to select for kid 2 must be 3 or more. 
>
> Its hard to solve this by hand, but we could easily solve this by a computer!

### Stirling Numbers 
> [!Abstract] Theorem: OGF for Stirling Numbers
> Let $k$ be a fixed positive integer. Then the OGF for $\{a_n\} = \{S(n,k)\}$ is
> $$
> F_k (x) = \sum_{n=0}^\infty a_n x^n = \frac{x^k}{(1-x)(1-2x) \dots (1-kx)}
> $$
>
> > [!Note]- Proof
> > 
> > Recall that
> > $$
> > S(0,0) = 1 \qquad S(n,0) = S(0,k) = 0 \qquad S(n,k) = S(n-1,k-1) + kS(n-1, k)
> > $$
> > 
> > Then, $F_k (x) = \sum a_n x^n = \sum_{n=0}^\infty S(n,k) x^n$. We solve for a closed form solution.
> > $$
> > \begin{align*}
> > \sum_{n=0}^\infty S(n,k) x^n 
> > &= \sum_{n=0}^\infty (S(n-1,k-1) + kS(n-1, k)) x^n \\
> > &= \sum_{n=1}^\infty S(n-1,k-1) x^n + \sum_{n=1}^\infty kS(n-1, k) x^n \\
> > &= x \sum_{n=1}^\infty S(n-1,k-1) x^{n-1} + x k\sum_{=1}^\infty S(n-1, k) x^{n-1} \\
> > &= x F_{k-1} (x) + x kF_k (x)
> > \end{align*}
> > $$
> > This yields us a recursion of $F_k$ in terms of $F_{k-1}$.
> > $$
> > F_k (x) = \frac{x F_{k-1} (x)}{1-kx}
> > $$
> > So, if I repeat this recursion, I will get my definition above!
> > $$
> > F_k (x) = \frac{x}{1-kx} F_{k-1} = \frac{x}{1-kx} \frac{x}{1-(k-1)x} F_{k-2} = \dots = \frac{x^k}{(1-x)(1-2x) \dots (1-kx)}
> > $$

### Integer Partitions
> [!Abstract] Theorem: 
> The OGF for the total integer partitions of $n$, $p(n)$, is
> $$
> F(x) = \sum_{n=0}^\infty p(n) x^n = \frac{1}{(1-x)(1-x^2)(1-x^3)\dots} = \prod_{k=1}^\infty \frac{1}{1-x^k}
> $$
>
> > [!Note]- Proof (Sketch)
> > 
> > $$
> > \begin{align*}
> > F(x) 
> > &= \frac{1}{1-x} \frac{1}{1-x^2} \frac{1}{1-x^3} \dots \\
> > &= (1 + x + x^2 + \dots) (1 + x^2 + x^4 + x^6 + \dots) (1 + x^3 + x^6 + x^9 + \dots)
> > \end{align*}
> > $$
> > Notice that each product gives us multiples of $k$, and if we select one of them, we are choosing the number of $k$'s we want in our integer partition! For example, if we chose $x^6$ in our $k = 2$ product (2nd one), we are choosing $2 + 2 + 2$, or in other words, 3 integers of 2! So,
> > 1. Group 1 relates to how many 1s are in the sum
> > 2. Group 2 relates to how many 2s are in the sum
> > 3. ...
> > 
> > More generally, the $k^{th}$ group in the ogf is given as
> > $$
> > 1 + x^k + x^{2k} + \dots + x^{t(k)} + \dots
> > $$
> > Where the term $x^{k(t)}$ which represents us choosing the "$t$" number of $k$'s to the integer partition of $n$.

> [!Example]+ Example: Integer Partitions
> How many ways can you make \$1 using any number of pennies, nickels, dimes, quarters, and half dollars?
>
> We can formulate this as the following OGF, where we are looking for the coefficient of $x^{100}$.
> 
> $$
> \begin{align*}
> &(1 + x + x^2 + \dots) (1 + x^5 + x^{10} + \dots) (1 + x^{10} + x^{20} + \dots) \\
> &\qquad (1 + x^{25} + x^{50} + \dots) (1 + x^{50} + x^{100} + \dots)
> \end{align*}
> $$
> 
> By computer, we get 292.
> > Same as in weak compositions, with such a model, we can now manipulate this expression for any constraints! Say, if we wanted to use at least 5 pennies, we could replace the first group with $(x^5 + x^6 + \dots)$!

> [!Abstract] Theorem: Distinct Integer Partitions
> The total ways to partition integer $n$ into parts where every number is distinct equals the total ways to partition integer $n$ where each part is an odd number.
> 
> > [!Note]- Proof
> >
> > The ogf for partitions into **distinct parts** is
> > $$
> > F(x) = (1 + x) (1 + x^2) (1 + x^3) \dots
> > $$
> > 
> > As this ensures we choose any integer at most once. We change them using difference of squares.
> > $$
> > \begin{align*}
> > &= \frac{1-x^2}{1-x} \frac{1-x^4}{1-x^2} \frac{1-x^6}{1-x^3} \dots \\
> > &= \frac{1}{(1-x) (1-x^3) (1-x^5) \dots} \\
> > &= (1 + x + x^2 + \dots) (1 + x^3 + x^6 + \dots) (1 + x^5 + x^10 + \dots) \dots
> > \end{align*}
> > $$
> > 
> > This is the ogf for integer partitions of odd integers!

> [!Example]+ Example: Distinct Integer Partitions
> $n = 6$. The distinct integer partitions vs. the odd integer partitions are given as
> $$
> \begin{align*}
> 6 = 2 + 4 = 1 + 5 = 1 + 2 + 3 \\
> 1 + 1 + 1 + 1 + 1 + 1 = 1 + 5 = 3 + 3 = 1 + 1 + 1 + 3
> \end{align*}
> $$
> Both have 4 cases!

## Integer Partitions into $k$ Parts
> [!Abstract] Theorem: Integer Partitions into $k$ Parts
> The OGF for $p_k (n)$, the ways to partition $n$ into exactly $k$ parts, is given as
> $$
> \begin{align*}
> F(x)
> &= (1 + x + x^2 + \dots) (1 + x^2 + x^4 + \dots) \dots \\ 
> &\qquad (1 + x^{k-1} + x^{2k-2} + \dots) (x^k + x^{2k} + \dots) \\
> &= (1 + x + x^2 + \dots) (1 + x^2 + x^4 + \dots) \dots (1 + x^k + x^{2k} + \dots) x^k
> \end{align*}
> $$
>
> > [!Note]- Proof / Intuition
> > 
> > First, we find the ogf for the partitions of integer $n$ into parts with size at most $k$. To do this, we stop our product at the $k^{th}$ term.
> > $$
> > F(x) = (1 + x + x^2 + \dots) (1 + x^2 + x^4 + \dots) \dots (1 + x^k + x^{2k} + \dots)
> > $$
> > 
> > If we look at a Ferrers diagram, we find that the conjugate of this is integer partitions into at most $k$ parts!
> > 
> > Then, with this, we can get integer partitions into exactly $k$ parts by subtracting partitions of at most $k - 1$ parts from partitions of at most $k$ parts.
> > > We can also think of this as, to force exactly $k$ parts, we must always choose 1 part to be of size $k$! This way, when we take the conjugate, we will have exactly $k$ parts.
> > $$
> > \begin{align*}
> > F(x) 
> > &= (1 + x + x^2 + \dots) (1 + x^2 + x^4 + \dots) \dots (1 + x^k + x^{2k} + \dots) \\
> > &\qquad - (1 + x + x^2 + \dots) (1 + x^2 + x^4 + \dots) \dots (1 + x^{k-1} + x^{2k-2} + \dots) \\
> > &= (1 + x + x^2 + \dots) (1 + x^2 + x^4 + \dots) \dots \\ 
> > &\qquad (1 + x^{k-1} + x^{2k-2} + \dots) (x^k + x^{2k} + \dots)
> > \end{align*}
> > $$


## 2.4: Exponential Generating Functions
The **exponential generating function** for sequence $\{a_n\}$ is
$$
F(x) = \sum_{n=0}^\infty a_n \frac{x^n}{n!}
$$

> [!Info] Lemma: Product of OGFs
> Let $f(x) = \sum_{n=0}^\infty a_n x^n$, $g(x) = \sum_{n=0}^\infty b_n x^n$. Then,
> $$
> f(x) g(x) = \sum_{n=0}^\infty c_n x^n
> $$
> Where $c_n = \sum_{i=0}^n a_i b_{n-i}$.

> [!Info] Lemma: Product of EGFs
> Let 
> $$
> F(x) = \sum_{n=0}^\infty \bar{a}_n \frac{x^n}{n!} \qquad G(x) = \sum_{n=0}^\infty \bar{b}_n \frac{x^n}{n!}
> $$
>
> Then, 
> $$
> F(x) \cdot G(x) = \sum_{n=0}^\infty \bar{c}_n \frac{x^n}{n!}
> $$
> Where $\bar{c}_n = \sum_{i=0}^n \binom{n}{i} \bar{a}_i \bar{b}_{n-i}$
>
> What's important about this is that $\bar{c}_n$ gives us the total ways to separate $[n]$ into two blocks, such that block 1 does something in $\bar{a}_i$ ways, and block 2 does something in $\bar{b}_{n-i}$ ways! This can be used to solve more problems.
>
> > [!Note]- Proof 
> > 
> > Recall that if $A(x) = \sum a_n x^n, B(x) = \sum b_n x^n$, then $A(x) \cdot B(x) = \sum c_n x^n$, $c_n = \sum_{i=0}^n a_i b_{n-i}$.
> > 
> > Let $a_n = \bar{a}_n / n!, b_n = \bar{b}_n / n!$ to get our lemma.

> [!Abstract] Theorem: EGFs for Stirling Numbers
> The egf for the Stirling Number $S(n,k)$ (for fixed $k > 0$) is given as
> $$
> F(x) = \sum_{n=0}^\infty S(n,k) \frac{x^n}{n!} = \frac{(e^x - 1)^k}{k!}
> $$
>
> > [!Note]- Proof
> > 
> > Recall that
> > $$
> > \begin{align*}
> > S(n,k) 
> > &= \frac{1}{k!} \sum_{i=0}^k (-1)^i \binom{k}{i} (k - i)^n \\
> > F(x) 
> > &= \sum_{n=0}^\infty \left[ \frac{1}{k!} \sum_{i=0}^k (-1)^i \binom{k}{i} (k - i)^n \right] \frac{x^n}{n!} \\
> > &= \frac{1}{k!} \sum_{i=0}^k \left[ (-1)^i \binom{k}{i} \sum_{n=0}^\infty \frac{(k-i)^n x^n}{n!} \right] \\
> > &= \frac{1}{k!} \sum_{i=0}^k \left[ (-1)^i \binom{k}{i} e^{(k-i)x} \right] \\
> > &= \frac{1}{k!} (e^x - 1)^k
> > \end{align*}
> > $$

From this theorem, we can find that the egf for the bell number is
$$
F(x) = \sum B(n) \frac{x^n}{n!} = e^{e^x - 1}
$$

> [!Note]- Proof
> $$
> \begin{align*}
> F(x)
> &= \sum_{n=0}^\infty B(n) \frac{x^n}{n!} \\
> &= \sum_{n=0}^\infty \left[ \sum_{k=0}^n S(n,k) \right] \frac{x^n}{n!} \\
> &= \sum_{n=0}^\infty \left[ \sum_{k=0}^n S(n,k) \frac{x^n}{n!} \right] \\
> &= \sum_{k=0}^\infty \frac{1}{k!} [e^x - 1]^k \\
> &= e^{e^x - 1}
> \end{align*}
> $$

But why are egfs useful? Well, let's consider the product
$$
(1 + x + \frac{x^2}{2!} + \dots) (1 + x + \frac{x^2}{2!} + \dots) (1 + x + \frac{x^2}{2!} + \dots)
$$

Then, we can find the contribution to $x^n / n!$ as
$$
\frac{x_1^{s_1} x_2^{s_2} x_3^{s_3}}{s_1! s_2! s_3!} \qquad s_1 + s_2 + s_3 = n
$$
Thus, the $x^n / n!$ term is
$$
\left( \sum_{s_1 + s_2 + s_3 = n} \frac{n}{s_1! s_2! s_3!} \right) \frac{x^n}{n!}
$$
This actually is permutations with repetition using any number of A's, B's, and C's ($3^n$)! In fact, this makes a lot of sense, because
$$
\left(1 + x + \frac{x^2}{2!} + \dots\right)^3 = (e^x)^3 = e^{3x} = \sum 3^n \frac{x^n}{n!}
$$
> Like with OGFs, EGFs give us a much more versatile way to do these types of problems! See the below example.

> [!Example]+ Example: Closed Form Sequences (1)
> How many rearrangements of length $n$ use an odd number of A's, even number of B's, and any number of C's?
> 
> If $a_n$ denotes the value, find the closed form for $a_n$.
> $$
> \begin{align*}
> F(x)
> &= 
> \left( x + \frac{x^3}{3!} + \frac{x^5}{5!} + \dots  \right)
> \left( 1 + \frac{x^2}{2!} + \frac{x^4}{4!} + \dots  \right)
> \left( 1 + x + \frac{x^2}{2!} + \dots \right) \\
> &= 
> \left[ (1 + x + \frac{x^2}{2!} + \dots) - (1 - x + \frac{(-x)^2}{2!} + \frac{(-x)^3}{3!} + \dots \right] \frac{1}{2} \\
> &\quad \left[ (1 + x + \frac{x^2}{2!} + \dots) + (1 - x + \frac{(-x)^2}{2!} + \frac{(-x)^3}{3!} + \dots \right] \frac{1}{2} \\
> &\quad \left( 1 + x + \frac{x^2}{2!} + \dots \right) \\
> &= \left( \frac{e^x - e^{-x}}{2} \right) \left( \frac{e^x + e^{-x}}{2} \right) e^x \\
> \end{align*}
> $$
> We've found a closed form egf. We can now use this to find our closed form sequence!
> $$
> \begin{align*}
> &= \frac{e^{3x} - e^{-x}}{4} \\
> &= \frac{1}{4} \left[ \sum_{n=0}^\infty \frac{(3x)^n}{n!} - \sum_{n=0}^\infty \frac{(-x)^n}{n!} \right] \\
> &= \frac{1}{4} \left[ \sum_{n=0}^\infty \frac{(3^n - (-1)^n)}{n!} x^n \right] \\
> &= \sum_{n=0}^\infty \left( \frac{3^n - (-1)^n}{4} \right) \frac{x^n}{n!} \
> a_n = \frac{3^n - (-1)^n}{4}
> \end{align*}
> $$

> [!Example] Example
> There are 3 bookshelves and $n$ books. How many ways can you arrange the books on shelves such that each shelf has at least 1 book? 
> 
> One way we could count this directly is by rearranging the books, and then using stars and bars!
> 
> Alternatively, we can use egfs to find all ways to arrange books so each shelf has at least 1 book.
> 
> The egf for one shelf with $i$ books is given as
> $$
> \sum_{i=1}^\infty a_i \frac{x^i}{i!} = \sum_{i=1}^\infty i! \frac{x^i}{i!} = \sum_{i=1}^\infty x^i
> $$
> 
> This problem is asking for the coefficient of $x^n / n!$ in
> $$
> \left( \sum_{i=1}^\infty x^i \right)^3 = \left( \frac{x}{1-x} \right)^3 = x^3 \frac{1}{(1-x)^3}
> $$
> Note that $1 / (1-x)^3$ is the ogf for weak compositions into 3 parts. 
> $$
> \begin{align*}
> = \sum_{i=0}^\infty \binom{i + 3 - 1}{3 - 1} x^{i+3} \\
> = \sum_{n=3}^\infty \binom{n-1}{2} x^n & n = i + 3 \\
> = \sum_{n=3}^\infty \binom{n-1}{2} n! \frac{x^n}{n!}
> \end{align*}
> $$
> We find that the coefficient of $\frac{x^n}{n!}$, the total ways, is 
> $$
> \binom{n-1}{2} n!
> $$

> [!Example] Example:
> Recall $D_n$ is the total derangements of $[n]$ bijections such that $f(i) \ne i$ for all $i \in [n]$.
>
> First, what is the egf for the total bijections where $f(i) = i$ for all $i \in [n]$? We find the EGF is
> $$
> \sum_{n=0}^\infty 1 \frac{x^n}{n!} = e^x
> $$
> As everything is fixed, so there is only one possible bijection.
>
> Let $D(x)$ be the egf for derangements: 
> $$
> D(x) = \sum D_n \frac{x^n}{n!}
> $$
> What is the meaning of $e^x D(x)$? The coefficient of $x^n / n!$ counts all possible permutations! From the $e^x$, we have the number of fixed inputs, and from $D(x)$ we have the number of deranged inputs!
> 
> $$
> \begin{align*}
> D(x) e^x 
> &= \sum_{n=0}^\infty n! \frac{x^n}{n!} \\
> &= \sum_{n=0}^\infty x^n = \frac{1}{1-x} \\
> D(x) 
> &= e^{-x} \frac{1}{1-x} \\
> &= \left( \sum_{j=0}^\infty \frac{(-x)^j}{j!} \right) \left( \sum_{i=0}^\infty x^i \right) \\
> &= \sum_{n=0}^\infty \left( \sum_{i=0}^n \frac{(-1)^i}{i!} 1 \right) x^n \\
> &= \sum_{n=0}^\infty \left( n! \sum_{i=0}^n \frac{(-1)^i}{i!} \right) \frac{x^n}{n!}
> \end{align*}
> $$
> Thus, 
> $$
> D_n = n! \sum_{i=0}^n \frac{(-1)^i}{i!} 
> $$
> > Note that above, we applied the product of ogf theorem discussed earlier.

> [!Example] Example:
> How many ways can we split up "n" people into any number of groups, where each group sits at an unlabeled circular table? We assume the tables are not distinguishable, and every table has at least 1 person. 
>
> We let the case of 0 tables be 1 way.
>
> In the $n = 4$ case, observe that we have the following number of ways:
> $$
> \begin{matrix}
> 1 & \star & | & \star & | & \star & | & \star \\
> \binom{4}{2} \frac{2!}{2} & | & \star & \star & | & \star & | & \star \\
> \binom{4}{2} \frac{1}{2} & \star & \star & | & \star & \star \\
> \binom{4}{3} \frac{3!}{3} & \star & \star & \star & | & \star \\
> \frac{4!}{4} & \star & \star & \star & \star
> \end{matrix}
> $$
> In total, we have 24 ways.
>
> First, the egf for 1 table with $n$ people is
> $$
> \begin{align*}
> G(x) 
> &= \sum_{n=1}^\infty a_n \frac{x^n}{n!} = \sum_{n=1}^\infty \frac{n!}{n} \frac{x^n}{n!} \\
> &= \sum_{n=1}^\infty \frac{x^n}{n} = \sum_{n=0}^\infty \frac{x^{n+1}}{n+1} \\
> &= \int \sum_{n=0}^\infty x^n dx = \int \frac{1}{1-x} dx \\
> &= \ln \left( \frac{1}{1-x} \right)
> \end{align*}
> $$
>
> Thus, for $k$ tables, we want the coefficient of $x^n / n!$ in
> $$
> \frac{1}{k!} \ln \left( \frac{1}{1-x} \right) \ln \left( \frac{1}{1-x} \right) \dots \ln \left( \frac{1}{1-x} \right)
> $$
> We divide by $k!$ as there is no ordering on the tables.
>
> But we can use any number of tables! So, we want
> $$
> \sum_{k=0}^\infty \frac{1}{k!} \left[ \ln\left( \frac{1}{1-x} \right) \right]^k = e^{\ln(1 / (1 - x))} = \sum_{n=0}^\infty n! \frac{x^n}{n!}
> $$
> We have $n!$ ways.
