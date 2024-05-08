---
title: Derivatives
tags:
- math410
---

# Limits
In this section, we discuss limits and what they mean.

A point $x_0 \in \mathbb{R}$ is a **limit point** of $D \subseteq \mathbb{R}$, provided there exists some sequence $\{x_n\}$ in $D / \{x_0\}$ such that
$$
\{x_n\} \to x_0
$$

> [!Example]+ Example: Limit Points of $\mathbb{R}$
> What are limit points of $D = \mathbb{R}$?
> 
> All of the points in $\mathbb{R}$, as for any $x_0$, we can define the sequence
> $$
> \{x_n\} = x_0 + \frac{1}{n}
> $$
> Which wil converge to $x_0$.

> [!Example]- Example: Limit Points of Intervals
> Let $D = (0,1)$. What are the limit points?
>
> All of the points in the interval $[0,1]$, as we can define a sequence that converges to the endpoints, or any value inside of the interval.

Let $f : D \to \mathbb{R}$ be a function, and let $x_0 \in \mathbb{R}$ be a limit point of $D$. Then, the **limit** of $f$ is
$$
\lim_{x \to x_0} f(x) = L
$$
If for any sequence $\{x_n\}$ in $D/\{x_0\}$, if $\{x_n\} \to x_0$, then $f(x_n) \to L$.
> Limits can only be defined if there exists a sequence in our domain that converges to the point (by definition of a limit point).

Formally, for all $\epsilon > 0$, there exists a $\delta > 0$ such that for all $x \in D$,
$$
0 < | x - x_0 | < \delta \to | f(x) - L | < \epsilon
$$

Note that all of our limit rules apply, and can be used.

# Derivatives
## Definition
Consider a function $f : I \to \mathbb{R}$ defined along some interval. Say we want the "slope" of the function at some limit point $x_0 \in I$.

This is the **derivative** of the function, $f'(x_0)$, defined as
$$
f'(x_0) = \lim_{x \to x_0} \frac{f(x) - f(x_0)}{x - x_0} = \lim_{h \to 0} \frac{f(x + h) - f(x_0)}{h}
$$
Where $\{x\} \in I / \{x_0\}$ is any sequence converging to $x_0$.
> Note you can obtain the decond definition from the first by setting $x = x_0 + h$

If the derivative for $f$ exists at a point $x_0$, we say $f$ is **differentiable** at this point.

> [!Abstract] Theorem: Differentiability and Continuity
> If $f'(x_0)$ exists, then $f$ is continuous at $x_0$. In other words, differentiability implies continuity.
>
> > [!Note]- Proof
> >
> > Let $x_n \to x_0$, where $x_n \in I / \{x_n\}$. We want to show that $f(x_n) \to f(x_0)$.
> > 
> > $$
> > \begin{align*}
> >     f(x_n) - f(x_0) = \frac{f(x_n) - f(x_0)}{x_n - x_0} (x_n - x_0) \to f'(x_0) \cdot 0 = 0
> > \end{align*}
> > $$

Derivatives have a variety of useful properties that we can prove! They are given below.

> [!Abstract] Theorem: Product Rule
> If $f : I \to \mathbb{R}$ and $g : I \to \mathbb{R}$ are both differentiable at $x_0$, so is $f \cdot g$.
> $$
> \frac{d}{dx} f(x) g(x) = f'(x) g(x) + f(x) g'(x)
> $$
>
> > [!Note]- Proof
> >
> > Let $x_n \to x_0$ with $x_n \in I / \{x_0\}$. Then, 
> > $$
> > \begin{align*}
> >     \lim_{x_n \to x_0} \frac{f(x_n) g(x_n) - f(x_0) g(x_0)}{x_n - x_0}  
> >     &=  \lim_{x_n \to x_0} \frac{f(x_n) g(x_n) - f(x_0) g(x_0) + f(x_n) g(x_0) - f(x_n) g(x_0)}{x_n - x_0} \\
> >     &= \lim_{x_n \to x_0} \frac{f(x_n) (g(x_n) - g(x_0)) + g(x_0) (f(x_n) - f(x_0))}{x_n - x_0} \\
> >     &= \lim_{x_n \to x_0} f(x_n) \frac{g(x_n) - g(x_0)}{x_n - x_0} + g(x_0) \frac{f(x_n) - f(x_0)}{x_n - x_0} \\
> >     &= f(x_0) g'(x_0) + g(x_0) f'(x_0)
> > \end{align*}
> > $$

> [!Abstract] Theorem: Chain Rule
> If $f : I \to \mathbb{R}$ and $g : I \to \mathbb{R}$ are both differentiable at $x_0$, so is $f(g(x))$.
> $$
> \frac{d}{dx} f(g(x)) = f'(g(x)) g'(x)
> $$


> [!Abstract] Theorem: Derivatives of Inverses
> Let $x_0 \in I$ and $f : I \to \mathbb{R}$ be a strictly monotone continuous function. Suppose $f'(x_0) \ne 0$ exists (to avoid division by 0). Then, we can find the derivative of $f$'s inverse as follows: 
> $$
> (f^{-1})'(x_0) = \frac{1}{f'(y_0)} = \frac{1}{f' (f^{-1}(x_0))}
> $$

> [!Example]- Example: Derivatives of Inverses
> Let $f(x) = x^2$, where $f : [0, \infty) \to \mathbb{R}$. Find $(f^{-1})' (4)$.
>
> We have $f'(x) = 2x$, and $f^{-1} (4) = 2$. Then,
> $$
> (f^{-1})' (4) = \frac{1}{2(2)} = \frac{1}{4}
> $$

## Mean-Value Theorem
### Definition and Proof
Let $f$ be a function continuous on $[a,b]$, and differentiable on $(a,b)$. Then $\exists c \in (a,b)$ such that
$$
f'(c) = \frac{f(b) - f(a)}{b - a}
$$
In other words, there exists a point where the derivative is equal to the average slope!

> [!Example]+ Example: Mean-Value Theorem Applications
> $\forall x$, let $|f'(x)| \le M$. Then, by mean value theorem,
> $$
> | f(x) - f(y) | = | f'(c) (x - y) | \le M |x - y|
> $$
> This proves an earlier theorem in uniform continuity!

We will prove this theorem; but first, we define a variety of lemmas that will be useful to us.

> [!Abstract] Lemma
> Let $I$ be an open interval containing $x_0$, and $f : I \to \mathbb{R}$. Suppose $f'(x_0)$ exists,
>
> If $f(x_0)$ is a max (or min), then $f'(x_0) = 0$.
>
> > [!Note]- Proof
> >
> > Without loss of generality, assume $f(x_0)$ is a max. We show that the limit of slopes on the left and right bound $f'(x_0)$, forcing $f'(x_0) = 0$.
> >
> > Define the interval $I = (x_0 - 1/n, x_0 + 1/n)$ sufficiently close to our maximum. We have
> > $$
> > \frac{f \left( x_0 + \frac{1}{n} \right) - f(x_0)}{\left(x + \frac{1}{n} \right) - x_0} \le 0
> > $$
> > Take this from $n \to \infty$ to get $f'(x_0) \le 0$.
> >
> > Similarly, we define the sequence $x_n = x_0 - 1/n$ to show that $f'(x_0) \ge 0$, which forces $f'(x_0)$ as $0 \le f'(x_0) \le 0$.

> [!Abstract] Theorem: Rolle's Lemma
> Let $f$ be continuous on $[a,b]$, differentiable on $(a,b)$, and $f(a) = f(b)$. Then, $\exists c \in (a,b)$ such that $f'(c) = 0$.
>
> > This is a special case of MVT, but we will use it to prove MVT!
>
> > [!Note]- Proof
> > 
> > By the extreme value theorem, we know that the maximum and minimum of $f$ exist. We do a case analysis:
> > 1. Suppose the max and min both occur at the endpoints. Then, the function is constant - we can choose any point in the interior whose derivative is 0.
> > 2. Suppose a max (or min) appears in $(a,b)$. Then, we apply our previous lemma to guarantee that $\exists c \in (a,b)$ such that $f'(c) = 0$.

We now prove MVT. The idea of this proof is to create a function from $f$ whose endpoints are the same, and applying Rolle's theorem.

> [!Note]+ Proof (Mean Value Theorem)
> 
> Let $f$ be a function continuous on $[a,b]$, and differentiable on $(a,b)$. Let $h(x) = f(x) - mx$ for some $m \in \mathbb{R}$. We can choose an $m$ such that $h(a) = h(b)$ in order to apply Rolle's theorem.
> $$
> f(a) + ma = f(b) + mb \Longrightarrow m = \frac{f(b) - f(a)}{b - a}
> $$
> By Rolle's lemma, $\exists c \in (a,b)$ such that $h'(c) = 0$! Plugging this in and solving for $f'(c)$, this gives us
> $$
> f'(c) = \frac{f(b) - f(a)}{b - a}
> $$

> [!Example]+ Example: Mean Value Theorem
> Prove that $5x + \sin(x) = 0$ does not have more than one solution.
>
> Note that $f'(x) = 5 + \cos(x) \le 4 > 0$. If there were two or more solutions, by Rolle's lemme, $f'(x) = 0$ at some point, which is a contradiction.

> [!Info] Corollary 1
> If $f : I \to \mathbb{R}$ is differentiable, then $f'(x) = 0$ for all $x$ is true if and only if $f$ is constant.
>
> > [!Note]-  Proof
> > 
> > #### Proof ($\leftarrow$)
> > We can use limit definition to easily show that the derivative is 0.
> >
> > #### Proof ($\rightarrow$)
> > By contrapositive, suppose that $f$ is not constant. Then there exists two separate points $a,b \in I$ such that $f(a) \ne f(b)$.
> > 
> > By MVT, there exists a derivative such that 
> > $$
> > f'(c) = \frac{f(b) - f(a)}{b - a} \ne 0
> > $$
> > 
> > We apply the contrapositive to obtain our corollary.

> [!Info] Corollary 2
> Let $I$ be an open interval, and $f,g$ differentiable on $I$. Then, for some constant $C$, $f'(x) = g'(x)$ if and only if $f(x) = g(x) + C$. 
> 
> > This will be really important in integration!

> [!Info] Corollary 3
> Let $f : I \to \mathbb{R}$ be differentiable on $I$. For all $x \in I$, if $f'(x) > 0$ at $x \in I$, then $f$ is strictly increasing on $I$.

### Cauchy MVT
Below, we discuss a generalization of the Mean Value Theorem onto parametric curves. 

> [!Abstract] Theorem: Cauchy Mean-Value Theorem
> Suppose $f$ and $g$ are continuous and differentiable on $(a,b)$, creating a parametric curve $(f(t), g(t))$. If $g'(t) \ne 0$, then $\forall t \in (a,b)$, $\exists t_0 \in (a,b)$ such that
> $$
> \frac{f'(t_0)}{g'(t_0)} = \frac{f(b) - f(a)}{g(b) - g(a)}
> $$

Note that this is a generalization, as we can set $g(t) = t$ for any suitable $f$ to prove the Mean Value Theorem on $f$.

> [!Note]- Proof (Sketch)
> Let $h(t) = f(t) - m g(t)$.
> 
> Choose $m$ such that $h(a) = h(b)$ in order to apply Rolle's theorem to $h(t)$. We then follow a similar process to the MVT theorem proof.

This theorem is quite important! It sets the stage for the Taylor series Lagrange remainder theorem.

> [!Abstract] Theorem: Function Value Theorem
> Let $I$ be an open interval, let $n \in \mathbb{N}$, and suppose we have a differentiable function $f : I \to \mathbb{R}$ which is $n$-times differentiable.
> 
> Suppose that at $x_0$
> $$
> f(x_0) = f'(x_0) = f''(x_0) = \dots = f^{n-1} (x_0) = 0
> $$ 
> Then $\forall x \in I / \{x_0\}$, there exists a $z$ between $x_0$ and $x$ such that 
> $$
> f(x) = \frac{f^n (z)}{n!} (x - x_0)^n
> $$
>
> > [!Note]- Proof
> > 
> > Let $g(x) = (x - x_0)^n$. We have
> > $$
> > \begin{align*}
> >     &g(x_0) = 0 \\
> >     &g'(x_0) = n (x - x_0)^{n-1} \vert_{x=x_0} = 0 \\
> >     &g''(x_0) = n (n - 1) (x - x_0)^{n-2} \vert_{x=x_0} = 0 \\
> >     &\vdots \\
> >     &g^{n-1} (x_0) = n! (x - x_0) \vert_{x=x_0} = 0 \\
> >     &g^n (x_0) = n! \\
> > \end{align*}
> > $$
> > 
> > Then, because $f(x_0) = g(x_0) = 0$, we take (continuously applying to the $n^{th}$ derivative)
> > $$
> > \begin{align*}
> >     \frac{f(x)}{g(x)} 
> >     &= \frac{f(x) - f(x_0)}{g(x) - g(x_0)} = \frac{f'(x_1)}{g'(x_1)} &x_1 \text{ between } x_0, x \\
> >     & \frac{f'(x_1) - f'(x_0)}{g'(x_1) - g'(x_0)} = \frac{f''f(x_2)}{g''(x_2)} \\
> >     &\vdots \\
> >     &\frac{f^n (z)}{n!}
> > \end{align*}
> > $$
> > 
> > So, we find 
> > $$
> > f(x) = g(x) \frac{f^n (z)}{n!} = \frac{f^n (z)}{n!} (x - x_0)^n
> > $$

> [!Example]+ Example: Remainder Theorem
> Let $f : \mathbb{R} \to \mathbb{R}$ and $f(2) = f'(2) = 0$, and $|f''(x)| \le 3$ for all $x$. Give a bound on $f(5)$.
>
> By the remainder theorem,
> $$
> \begin{align*}
> f(5) = \frac{f^2 (z)}{2!} (5 - 2)^2  \\
> |f(5)| \le \frac{3}{2} \cdot 9 \le \frac{27}{2}
> \end{align*}
> $$
