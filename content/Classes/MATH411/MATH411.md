---
title: MATH411
tags:
- math411
---

MATH411 is a continuation of MATH410, but into higher dimensions.
- [[Generalizations | Generalizations to Rn]]
- [[Metric Spaces]]

# Derivatives in Several Variables
## Limits
Let $A \subseteq \mathbb{R}^n$. Then, $x^*$is a **limit point** of $A$ if there is a sequence  $\exists \{ x_k \} \subseteq A / \{x^*\}$ such that $\{x_k\} \to x^*$. 
> In other words, there is a sequence not containing $x^*$ converging to it.

If we have function $f : A \to \mathbb{R}$, and $x^*$ is a limit point of $A$, then **the limit of the function** is defined as 
$$
\lim_{x \to x^*} f(x) = l
$$ 
if $\forall \{x_k\} \subseteq A / \{x^*\}$, 
$$
\lim_{k \to \infty} f(x_k) = l
$$

> [!Example]+ Example: Existence of Limits (1)
> $$
> f(x,y) = \frac{xy}{x^2 + y^2}
> $$
>
> $f : \mathbb{R}^2 \to \{(0,0)\}$. 
>
> $\lim_{(x,y) \to (0,0)} f(x,y)$ does not exist, as we can chose $\{x_k\} = (1/k, 0)$, and $\{x_k\} = (1/k, 1/k)$, which have different limits as $k \to \infty$. 

> [!Example]- Example: Existence of Limits (2)
> $$
> g(x,y) = \frac{x^2 y}{x^2 + y^2}
> $$
> In this case, $\lim_{(x,y) \to (0,0)} g(x,y)$ exists and equals 0.
> 
> Let $(x_k, y_k) \to (0,0)$ not containing $(0,0)$. Then, 
> $$
> | g(x_k, y_k) | \le |x_k| \frac{ |x_k y_k| }{x_k^2 + y_k^2} \le |x_k| \frac{1}{2} \to 0
> $$

> [!Abstract] Theorem: Limit Equivalences
> Let $A \subseteq \mathbb{R}^n$ and let $x^*$ be a limit point of $A$. For a function $f : A \to \mathbb{R}$, and $l \in \mathbb{R}$, the following assertions are equivalent:
> 1. $$
>    \lim_{x \to x^*} f(x) = l
>    $$
>    In other words, for any $\{x_k\} \in A / \{x^*\}$, if $\lim_{k\to\infty} x_k = x^*$, then
>    $$
>    \lim_{k\to\infty} f(x_k) = l
>    $$
> 2. $\forall \epsilon > 0$, there exists some $\delta > 0$ such that
>    $$
>    d(x, x^*) < \delta \to | f(x) - l | < \epsilon \qquad x \in A / \{x^*\}
>    $$

A function $f : \mathbb{R}^n / \{0\} \to \mathbb{R}$ is **homogeneous of degree $k$** if
$$
f(tx) = t^k f(x) \qquad \forall t > 0, \forall x \in \mathbb{R}^n / \{0\}
$$
> Basically, we should be able to replace $x,y$ with $t$, and take out the $t$ into a $t^k$ term.

> [!Example]+ Example: Homogenoeus Functions
> $$
> g(x,y) = \frac{x^2 y}{x^2 + y^2}
> $$
> Is homogeneous of degree 1, because
> $$
> g(tx, ty) = \frac{t^3 xy}{t^2 (x^2 + y^2)} = t g(x,y)
> $$
> 
> $$
> f(x,y) = \frac{xy}{x^2 + y^2}
> $$
> Is homogeneous of degree 0, because
> $$
> f(tx, ty) = t^0 f(x,y)
> $$

Curiously, $g$ is homogeneous of degree 1 and has a limit to $(0,0)$, whereas $f$ is homogeneous of degree 0 and doesn't. Does there suggest some generalization?

> [!Abstract] Proposition: Limits of Homogeneous Functions
> If $f : \mathbb{R}^n / \{0\} \to \mathbb{R}$ is continuous, and homogeneous of degree $k > 0$, then
> $$
> \lim_{x \to 0} f(x) = 0
> $$
>
> > [!Note]- Proof
> > 
> > We look at $f(x)$, and we try to make the case that as $x \to 0$, $f(x) \to 0$.
> > $$
> > f(x) = f \left( ||x|| \frac{x}{||x||} \right)
> > $$
> > We write this as a product of something that approaches 0 and something that is bounded. 
> > 
> > By assumption, $f(x)$ is homogeneous of degree $k$, so letting $t = ||x||$,
> > $$
> > f \left( ||x|| \frac{x}{||x||} \right) = ||x||^k f \left( \frac{x}{||x||} \right)
> > $$
> > As $x \to 0$, $||x||^k \to 0$! Also, as $\frac{x}{||x||} \in S^{n-1}$ (the unit sphere of dimension $n - 1$), which is a sequentially compact, then continuous functions on sequentially compact sets are bounded. 
> > $$
> > ||x||^k f \left( \frac{x}{||x||} \right) \to 0 
> > $$

> [!Example]- Example: Continuity with Homogeneity
> $$
> f(x,y) = \frac{x^3 y}{x^2 + y^2} \qquad \frac{\partial f}{\partial x} (0,0) = 0
> $$
> 
> We show that $f$ is $C^1$ by homogeneity.
> 
> We know that $f$ is $C^{\infty}$ in $\mathbb{R}^n / \{(0,0)\}$ is homogeneous of degree 2. So, $\frac{\partial f}{\partial x}$ is homogeneous of degree 1.
> > It is a fact that if $f \in C^1 (\mathbb{R}^n / \{0\})$ and is homogeneous of degree $k$, then $\frac{\partial f}{\partial x_i}$ is homogeneous of degree $k - 1$.
> 
> Let $x \ne 0$, $t > 0$. Then, say $f$ is homogeneous degree $k$.
> $$
> \begin{align*}
> f(t,x) = t^k f(x) \\
> \frac{\partial}{\partial x_i} f(tx) = \frac{\partial}{\partial x_i} [t^k f(x)] = t^k \frac{\partial f}{\partial x_i} (x) \\
> t \frac{\partial f}{\partial x_i} (tx) = t^k \frac{\partial}{\partial x_i} t^k f(x) \Longrightarrow \frac{\partial f}{\partial x_i} (tx) = t^{k-1} f(x)
> \end{align*}
> $$
> By a theorem, homogeneous functions of positive degree go to 0 as $x \to 0$. So, $f \in C^1$.

This does not necessarily mean that homogeneous functions of degree $k = 0$ don't have a limit at 0! Just that some don't. 
> Any constant function (ex. $f(x) = 1$) have defined limits as $x \to 0$!

## Partial Derivatives
Let $f : O \to \mathbb{R}$, $x = (x_1, \dots x_n) \in O$. 

We define the **partial derivative of $f$ with respect to $x_i$ as**
$$
\frac{\partial f}{\partial x_i} (x) = \lim_{t \to 0} \frac{f(x + t e_i) - f(x)}{t}
$$
Where $e_i$ is the $i^{th}$ basis vector, if the latter limit exists.
> Keep all variables constant except $x_i$, and take $\frac{d}{dx_i}$!

> [!Example]+ Example: Partial Derivatives and Continuity
> Let $f : \mathbb{R}^2 \to \mathbb{R}$,
> $$
> f(x,y) = 
> \begin{cases}
> \frac{xy}{x^2 + y^2} & (x,y) \ne (0,0) \\
> 0 & (x,y) = (0,0)
> \end{cases}
> $$
> 
> We noticed that $f$ is not continuous at $(0,0)$, and $\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}$ exist (by the quotient rule) at all $(x,y) \ne (0,0)$.
> 
> Then, does $\frac{\partial f}{\partial x}$ exist at $(0,0)$?
> $$
> \lim_{t \to 0} \frac{f(t,0) - f(0,0)}{t} = \lim_{t \to 0} \frac{0 - 0}{t}
> $$
> Yes! It exists and is equal to 0.
> 
> Similarly, we can find $\frac{\partial f}{\partial y} = 0$.
> 
> This is very interesting! Even though $f(x,y)$ is not continuous at $(0,0)$, our partial derivatives still exist! This goes against our understanding of differentiability and continuity in the single variable case. 

Let $O \subseteq \mathbb{R}^n$ open, $f : O \mathbb{R}$. Then, we say $f$ has **first-order partial derivatives** if for all $1 \le i \le n$, the function has a partial derivative with respect to its $i^{th}$ component, at every point in its domain.

Furthermore, we say that $f$ is **continuously differentiable** if it has first-order partial derivatives such that each partial derivative $\frac{\partial f}{\partial x_i}$ is continuous for $1 \le i \le n$.

---

Let's now consider second-order partial derivatives, denoted like
$$
\frac{\partial f}{\partial x_j \partial x_i}
$$
Where we apply the partial derivative of $x_i$ first, then $x_j$ after.
> Order matters! There are some functions where swapping the order of derivatives changes the result.

We say $f$ has **second-order partial derivatives** of it has first-order partials, such that for $1 \le i \le n$, each $\frac{\partial f}{\partial x_i}$ also has first-order partial derivatives.

Furthermore, we say $f$ has **continuous second-order partial derivatives** if it has second-order partial derivatives, and each $\frac{\partial^2 f}{\partial x_i \partial x_j}$ are continuous.

> [!Abstract] Theorem: Order of Partial Derivatives
> If $\frac{d}{d x_i} \left( \frac{\partial f}{\partial x_j} \right)$ and $\frac{d}{d x_j} \left( \frac{\partial f}{\partial x_i} \right)$ exist and are continuous in $O$, then
> $$
> \frac{d}{d x_i} \left( \frac{\partial f}{\partial x_j} \right) = \frac{d}{d x_j} \left( \frac{\partial f}{\partial x_i} \right)
> $$
>
> > [!Note]- Proof 
> > 
> > Let $x = x_i, y = x_j$. Then,
> > $$
> > A = f(x_0 + r, y_0 + r) - f(x_0 + r, y_0) - f(x_0, y_0 + r) + f(x_0, y_0)
> > $$
> > Define $\phi(x) = f(x, y_0 + r) - f(x, y_0)$. Then,
> > $$
> > A = \phi(x_0 + r) - \phi(x_0)
> > $$
> > By the mean value theorem, this is equal to
> > $$
> > \begin{align*}
> > = \phi' (x_0 + \theta_1) * r = \frac{\partial}{\partial x} [ f(x_0 + \theta_1, y_0 + r) - f(x_0 + \theta_1, y_0) ] R 
> > \end{align*}
> > $$
> > > We create two equivalent functions that converge to the two partial derivatives, respectively, forcing equality.

## Directional Derivatives and MVT
From prior courses, we learned to define the **directional derivative** of a function $f$ as
$$
\frac{d}{dt} \bigg|_{t = 0} [ f(x + th) ] = \langle \nabla f(x), h \rangle
$$
For $x \in \mathbb{R}^n, h \in \mathbb{R}^n$. Where the **gradient** of the function**, $\nabla f$, is given as
$$
\nabla f(x) = \left( \frac{\partial f}{\partial x_1}, \dots, \frac{\partial f}{\partial x_n} \right)
$$

But this may not actually hold for all functions! Consider
$$
f(x,y) =
\begin{cases}
\frac{xy}{x^2 + y^2} & (x, y) \ne 0 \\
0 & (x,y) = 0
\end{cases}
$$
Then, for $x = (0,0)$, $h = (1,1)$, the directional derivative does not exist, even though $\langle \nabla f(x), h \rangle = 0$!

We prove the above definition, and show the conditions in which it holds.

> [!Abstract] Proposition
> Let $f : \mathbb{R}^n \to \mathbb{R}$, and assume all $\frac{\partial f}{\partial x_i}$ exist $\forall x \in \mathbb{R}^n$, $\forall i \in \{1, \dots n\}$.
> 
> Fix $x, h \ne 0$ ($h \in \mathbb{R}^n$). Then, there exists a $z_1, \dots z_n \in B_{||h||} (x)$ such that
> $$
> f(x + h) - f(x) = \frac{\partial f}{\partial x_1} (z_1) h_1 + \dots + \frac{\partial f}{\partial x_n} (z_n) h_n
> $$
>
> > [!Note]- Proof
> > 
> > We prove this for $n = 2$, though the proof can very easily be extended to more dimensions.
> > 
> > Consider the points $(x_1, x_2)$, $(x_1 + h, x_2 + h)$, and look at
> > $$
> > f(x_1 + h, x_2 + h) - f(x_1, x_2) = f(x_1 + h, x_2 + h) - f(x_1, x_2 + h_2) + f(x_1, x_2 + h_2) - f(x_1, x_2)
> > $$
> > 
> > By doing this, we convert our problem into 1 dimensions, where we can solve for the differences
> > $$
> > f(x_1 + h, x_2 + h) - f(x_1, x_2 + h_2) \qquad f(x_1, x_2 + h_2) - f(x_1, x_2)
> > $$
> > separately.
> > 
> > By the Mean Value Theorem, 
> > $$
> > \begin{align*}
> > f(x_1 + h, x_2 + h) - f(x_1, x_2 + h_2) = \frac{\partial f}{\partial x_1} (x_1 + \theta h_1, x_2 + h_2) h_1 \\
> > f(x_1, x_2 + h_2) - f(x_1, x_2) = \frac{\partial f}{\partial x_2} (x_1, x_2 + \theta_2 h_2) h_2 \\
> > f(x_1 + h, x_2 + h) - f(x_1, x_2) = \frac{\partial f}{\partial x_1} (x_1 + \theta h_1, x_2 + h_2) h_1 + \frac{\partial f}{\partial x_2} (x_1, x_2 + \theta_2 h_2) h_2
> > \end{align*}
> > $$
> > 
> > Let $z_1 = (x_1 + \theta_1 h_1, x_2 + h_2)$, and $z_2 = (x_1, x_2 + \theta_2 h_2)$. We are done.

If $f : O \to \mathbb{R}^n$, $O$ open, and all $\frac{\partial f}{\partial x_i} (x)$ exist $\forall x \in O$, and are continuous, $f$ is called **continuously differentiable**, called $C^1 (O)$.

> [!Abstract] Theorem: Formula for The Directional Derivative
> If $f : \mathbb{R}^n \to \mathbb{R}$ is $C^1$, then $\forall x \in \mathbb{R}^n$, $\forall h \ne 0$, the limit
> $$
> \frac{d}{dt} \bigg|_{t=0} f(x + th) = \lim_{t \to 0} \frac{f(x + th) - f(x)}{t}
> $$
> Exists and equals $\langle \nabla f(x), h \rangle$.
> $$
> \langle \nabla f(x), h \rangle = \sum_{i=1}^n \frac{\partial f}{\partial x_i} (x) h_i
> $$
>
> > [!Note]- Proof
> > 
> > By our previous proposition, 
> > $$
> > \begin{align*}
> > \frac{f(x + th) - f(x)}{t} 
> > &= \frac{1}{t} \left( \frac{\partial f}{\partial x_1} (z_1) t h_1 + \dots + \frac{\partial f}{\partial x_n} (z_n) t h_n \right) \\
> > &= \frac{\partial f}{\partial x_1} (z_1) h_1 + \dots + \frac{\partial f}{\partial x_n} (z_n) h_n
> > \end{align*}
> > $$
> > For $z_1, \dots z_n \in B_{||th||} (x)$. Let $t \to 0$. Then, the ball of $B_{||th||} (x)$ will shrink towards $x$, forcing all $z_i$'s to converge to $x$! Thus, as $t \to 0,$ we have
> > $$
> > \frac{\partial f}{\partial x_1} (x) h_1 + \dots + \frac{\partial f}{\partial x_n} (x) h_n
> > $$

Let $P \ne 0$, $P \in \mathbb{R}^n$, $f : \mathbb{R}^n \to \mathbb{R}$. Then, **the partial derivative in direction $P$** of $f$ is given as
$$
\frac{\partial f}{\partial P} (x) = \frac{d}{dt} \bigg|_{t=0} f(x + tP)
$$
If it exists. By the previous theorem, the partial derivative of $f$ in the direction $P$ exists and equals $\langle \nabla f, P \rangle \rangle$ if $f \in C^1$.

> [!Abstract] Proposition
> Let $f : \mathbb{R}^n \to \mathbb{R}, C^1$, $x \in \mathbb{R}^n$, $h \in \mathbb{R}^n$ where $h \ne 0$. 
> 
> Then, there exists $0 < \theta < 1$ such that
> $$
> f(x + h) - f(x) = \langle \nabla f(x + \theta h), h \rangle
> $$
>
> > This is similar to the first proposition we have, except all $z_1, \dots z_n$ are assumed to be at the point.
>
> > [!Note]- Proof
> > 
> > Let $\phi : \mathbb{R} \to \mathbb{R}$, $\phi(t) = f(x + th)$ so that 
> > $$
> > \phi(1) = f(x + h) \qquad \phi(0) = f(x)
> > $$
> > 
> > Then, $f(x + h) - f(x) = \phi(1) - \phi(0) = \phi'(\theta) (1 - 0)$ by the mean value theorem (for $0 < \theta < 1$) and furthermore, as the derivative of $\phi(t)$ is the directional derivative,
> > $$
> > f(x + h) - f(x) = \phi'(\theta) = \langle \nabla f(x + \theta h), h \rangle
> > $$

> [!Abstract] Theorem: Partial Derivatives and Continuity
> Let $f : \mathbb{R}^n \to \mathbb{R}$, and assume all $\frac{\partial f}{\partial x_i} (x)$ exist and are continuous. 
>
> Then, $f$ is continuous.
>
> > [!Note] Proof (? Missing something) 
> > 
> > Look at $f(x + h) - f(x)$. We would like to claim that as $h \to 0$, $f(x + h) \to f(x)$.
> > 
> > By the previous proposition, for some $0 < \theta < 1$
> > $$
> > | f(x + h) - f(x) | = | \langle \nabla f(x + \theta h, h) \rangle |
> > $$
> > By Cauchy Schwarz, this is less than or equal to
> > $$
> > \le || \nabla f(x + \theta h) || \cdot || h ||
> > $$
> > But as c, we can bound the first term! 
> > $$
> > || \nabla f(x + \theta h) || \le \max || \nabla f(y) || \cdot || x - y || \le C
> > $$
> > So, this drops to 0.
> 
> > By this proof, in fact, if all the partials exist $\forall x \in O$ and are bounded, then $f$ is still continuous!

Let $f : \mathbb{R}^n \to \mathbb{R}$, $C^1$. Fix $x$, and assume $\nabla f \ne 0$. Then, the maximum of the directional derivative at $x$ is given as
$$
\max_{||P|| = 1} \frac{\partial f}{\partial P} (x)
$$
Is attained for
$$
P = \frac{\nabla f(x)}{|| \nabla f (x) ||}
$$
In other words, the direction of the gradient.

> [!Note] Proof
> If $||P|| = 1$, we have
> $$
> \frac{\partial f}{\partial P} (x) = \langle \nabla f(x), P \rangle
> $$
> By Cauchy-Schwarz, this is
> $$
> \le || \nabla f(x) || \cdot || P || = || \nabla f(x) ||
> $$
> We have an upper bound on our directional derivative! We can attain our upper bound if $P = \frac{\nabla f(x)}{|| \nabla f(x) ||}$.
> $$
> \begin{align*}
> \langle \nabla f(x), P \rangle 
> &= \langle \nabla f(x), \frac{\nabla f(x)}{|| \nabla f(x) ||} \rangle \\ 
> &= \frac{1}{|| \nabla f(x) ||} \langle \nabla f(x), \nabla f(x) \rangle \\
> &= || \nabla f(x) ||
> \end{align*}
> $$
> We've found a maximizer.

We end with a small remark that will segway into the next section. Let $f : \mathbb{R}^n \to \mathbb{R}, C^1$. Then,
$$
\lim_{h \to 0} \frac{f(x + h) - f(x) - \langle \nabla f(x), h \rangle}{||h||} = 0
$$
>  This can be proven by using Cauchy-Schwarz.

We use this to define differentiable functions!

$f : \mathbb{R}^n \to \mathbb{R}$ is **differentiable** at $x$ if $\exists Q \in \mathbb{R}^n$ such that
$$
\frac{f(x + h) - f(x) - \langle Q, h \rangle}{||h||} \to 0
$$
as $h \to 0$.

This is a stronger notion than partial diffentiation! So, $f \in C^1$ implies that $f$ is differentiable, which implies that all partials of $f$ exist. But, the converses are not true!

--- Chapter 14 ---

# Local Approximation of Real-Valued Functions
## First Order Approximation
Recall previously that if $f \in C^1 (\mathbb{R}^n)$, then
$$
f(x + h) - f(x) = \langle \nabla f(x + \theta h), h \rangle
$$
For some $0 < \theta < 1$.

A consequence of this is that
$$
\lim_{h\to 0} \frac{f(x+h) - f(x) - \langle \nabla f(x), h \rangle}{h} = 0
$$
Known as the **first order approximation formula**. In other words,
$$
f(x + h) = f(x) + \langle \nabla f(x), h \rangle + E(x,h) \qquad \lim_{h\to 0} \frac{E(x,h)}{||h||} = 0
$$
As the error drops to 0 when dividing by $||h||$, we can also say that the error is of **first order**, $O(||h||)$.

Letting $y = x+h$, $x$ fixed, this can alternatively be written as
$$
f(y) = f(x) + \langle \nabla f(x), (y - x) \rangle + O( ||x - y|| )
$$
So if $x$ is fixed, and $y$ is cloed to $x$, then we have a close approximation!

How does this relate to the tangent plane of $g$?

Define $G = \{ (y_1, y_2, f(y_1, y_2)) \}$. Define the tangent directions at $(x_1, x_2)$, as
$$
\begin{align*}
&\gamma_1 (t) = (x_1 + t, x_2, f(x_1 + t, x_2)) &\gamma_1'(0) = (1, 0, \frac{\partial f}{\partial x_1} (x_1, x_2)) \\
&\gamma_2 (t) = (x_1, x_2 + t, f(x_1, x_2 + t)) &\gamma_1'(0) = (0, 1, \frac{\partial f}{\partial x_2} (x_1, x_2)) \\
\end{align*}
$$
We can find a vector orthogonal to both of these, giving us a vector that is normal to our function.
$$
N = \left( -\frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, 1 \right)
$$
We use this to define the tangent plane at $(x_1, x_2, f(x_1, x_2)$ as
$$
\begin{align*}
&(y_1 - x_1, y_2 - x_2, y_3 - f(x_1,x_2)) \cdot \left( -\frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, 1 \right) = 0 \\
&y_3 - f(x_1, x_2) - \frac{\partial f}{d x_1} (x_1, x_2) (y_1 - x_1) - \frac{\partial f}{\partial x_2} (x_1, x_2) (y_2 - x_2) = 0 \\
&= y_3 = f(x_1, x_2) + \frac{\partial f}{d x_1} (x_1, x_2) (y_1 - x_1) + \frac{\partial f}{\partial x_2} (x_1, x_2) (y_2 - x_2)
\end{align*}
$$
Thus, we find that $f(y)$ defined before is actually a tangent plane approximation of our function!

## Second Order Approximation
Let $A$ be an $n \times n$ symmetric matrix (so, $a_{ij} = a_{ji}$ for all $i,j$). Define the function 
$$
Q(h) = \langle Ah, h \rangle = \sum_{i,j=1}^n a_{ij} h_i h_j
$$
This is the quadratic form for $A$. The main application of this, is when we for when we have the Hessian Matrix of a function (assuming $f \in C^2$)
$$
A = \nabla^2 f(x) = 
\begin{bmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \dots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\
\vdots & & \vdots \\
\frac{\partial^2 f}{\partial x_n \partial x_i} & \dots & \frac{\partial^2 f}{\partial x_n^2}
\end{bmatrix}
$$

If $f \in C^2 (\mathbb{R})$, $x,h$ fixed, then
1. $$
   \frac{d}{dt} f(x + th) = \langle \nabla f(x + th), h \rangle = \sum_{i=1}^n \frac{\partial f}{\partial x_i} (x + th) h_i
   $$
2. $$
   \frac{d^2}{dt^2} f(x + th) = \langle \nabla^2 f(x + th, h) \rangle = \sum_{i,j=1}^n \frac{\partial^2 f}{\partial x_i \partial x_j} (x + th) h_i h_j
   $$
   
> [!Info] Remark
> If $f \in C^3$, then
> $$
> \frac{d^3}{dt^3} f(x + th) = \sum_{i,j,k=1}^n \frac{\partial^3 f}{\partial x_i \partial x_j \partial x_k} (x + th) h_i h_j h_k
> $$

> [!Note]- Proof 
> For (1), this is a chain rule.
> 
> For (2), we have
> $$
> \begin{align*}
> \frac{d}{dt} \left[ \frac{d}{dt} f(x + th) \right] 
> &= \frac{d}{dt} \left[ \sum_{i=1}^n \left( \frac{\partial f}{\partial x_i} \right) (x + th) h_i \right] \\
> &= \sum_{i=1}^n \left[ \sum_{j=1}^n \frac{\partial}{\partial x_j} \frac{\partial f}{\partial x_i} (x + th) h_j \right] h_i
> \end{align*}
> $$

Let $A$ be an $n \times n$ matrix, $A = (a_{ij})$. Define the **Hilbert-Schmidt norm** of $A$ to be
$$
||A|| = \left( \sum_{i,j=1}^n a_{ij}^2 \right)^{1/2}
$$
In other words, we think of the matrix as a long vector, and take the vector norm.

> [!Abstract] Generalized Cauchy Schwarz Inequality
> $$
> || Ah || \le ||A|| \cdot ||h||
> $$
> 
> > [!Note]- Proof
> > 
> > $$
> > \begin{align*}
> > Ah 
> > &= 
> > \begin{bmatrix}
> > \text{Row 1} \\ \vdots \\ \text{Row n}
> > \end{bmatrix} h \\
> > &= 
> > \begin{bmatrix}
> > \langle r_1, h \rangle \\ \vdots \\ \langle r_n, h \rangle
> > \end{bmatrix} \\
> > ||Ah||^2 &= \left( \langle r_1, h \rangle^2 + \dots + \langle r_n, h \rangle^2 \right) \\
> > &\le (||r_1||^2 + \dots + ||r_n||^2) ||h||^2 \\
> > &\le ||h||^2 \sum_{i,j=1}^n a_{ij}^2 \\
> > &= ||A||^2 ||h||^2
> > \end{align*}
> > $$

Let $A : \mathbb{R}^n \to \mathbb{R}^m$. We define the **operator norm** of $A$ as
$$
||A||_\text{op} = \max_{||h|| = 1} || Ah || 
$$
Based on this, we can find that for $||h|| = 1$,
$$
||Ah|| \le ||A||_{HS} \qquad ||A||_{op} \le ||A||_{HS}
$$

Let $A$ be an $n \times m$, symmetric matrix. $A$ is **positive definite** if 
$$
\langle Au, u \rangle > 0
$$
For all $u \ne 0$. Similarly, $A$ is negative definite if $\forall u \ne 0$,
$$
\langle Au, u \rangle < 0
$$

> [!Abstract] Lemma
> Let $A$ be symmetric positive definite matrix. Then, there exists a $c > 0$ such that
> $$
> \langle Au , u \rangle \ge c ||u||^2
> $$
> For all $u \in \mathbb{R}^n$.
>
> > [!Note]- Proof
> > 
> > Note that the LHS and the RHS are both homogeneous degree 2.
> > $$
> > \langle A(tu), tu \rangle = t^2 \langle Au, u \rangle \qquad ||tu||^2 = t^2 ||u||^2 \quad \forall t > 0, \forall u \in \mathbb{R}^n
> > $$
> > Thus, our equation is true for $u$ if and only if it is true for any other $tu$, $(t > 0)$.
> > 
> > Thus, it suffices to show that our equation is true for unit vectors $\frac{u}{||u||}$, as by the earlier proposition, the argument applies for all $u$. Then,
> > $$
> > \langle Au, u \rangle \ge c \qquad \forall ||u|| = 1
> > $$
> > This creates a continuous function along a $S^{n-1}$ hypersphere in $\mathbb{R}^n$, which is sequentially compact. Thus, it must have a minimum and maximum. Choose the minimum to find our $c$.
> > > In fact, we can find $c$ by taking the minimum of the eigenvalues.

Recall if we have $f : \mathbb{R} \to \mathbb{R}$, $f''(x)$ exists for every $x$, then $\forall x,h \in \mathbb{R}$, we have
$$
f(x + h) = f(x) + f'(x) h + \frac{1}{2} f''(x + \theta h) h^2 
$$
For some $0 < \theta < 1$.

> [!Abstract] Theorem:
> Let $f : \mathbb{R}^n \to \mathbb{R}$, $C^2$, and $x,h \in \mathbb{R}^n$. Then, 
> $$
> f(x + h) = f(x) + \langle \nabla f(x), h \rangle + \frac{1}{2} \langle \nabla^2 f(x + \theta h) h, h \rangle
> $$
> 
> For some $0 < \theta < 1$.
>
> > [!Note] Proof
> > 
> > Let $\phi(t) = f(x + th)$. Then,
> > $$
> > \phi(1) = \phi(0) + \phi' (0) + \frac{1}{2} \phi''(\theta)
> > $$
> > For some $0 < \theta < 1$.
> > 
> > Notice that this holds only because we assumed the second order derivatives are continuous.
> > $$
> > \begin{align*}
> > \phi'(0) = \frac{d}{dt}_{t=0} f(x + th) = \langle \nabla f(x), h \rangle \\
> > \phi''(t) = \frac{d^2}{dt^2} f(x + th) = \langle \nabla^2 f(x + th) h, h \rangle
> > \end{align*}
> > $$

> [!Abstract] Theorem
> Let $f : \mathbb{R}^n \to \mathbb{R}$, $C^2$. Then,
> $$
> \lim_{h \to 0} \frac{f(x + h) - [f(x) + \langle \nabla f(x), h \rangle] + \frac{1}{2} \langle \nabla^2 f(x) h, h \rangle}{||h||^2} = 0
> $$
> 
> > [!Note] Proof
> >
> > $$
> > \begin{align*}
> > &\frac{f(x + h) - [f(x) + \langle \nabla f(x), h \rangle] + \frac{1}{2} \langle \nabla^2 f(x) h, h \rangle}{||h||^2} \\
> > &= \frac{| \frac{1}{2} \langle (\nabla^2 f(x + \theta h) - \nabla^2 f(x)) h, h \rangle | }{||h||^2} \\
> > &\le \frac{\frac{1}{2}|| (\nabla^2 f(x + \theta h) - \nabla^2 f(x)) h || ||h||}{||h||^2} \\
> > &\le \frac{1}{2} || \nabla^2 f(x + \theta h) - \theta^2 f(x) || \to 0 
> > \end{align*}
> > $$

Let $f : O \to \mathbb{R}$, $O$ open in $\mathbb{R}^n$. Then, $x$ is a strict local minmizer if there exists a $\delta > 0$ such that
$$
f(x) < f(x + h) \qquad \forall 0 < ||h|| < \delta
$$
Similarly, $x$ is a strict local maximizer if $\exists \delta > 0$ such that
$$
f(x) > f(x + h) \qquad \forall 0 < ||h|| < \delta
$$

> [!Abstract] Theorem: Strict Local Minimizers
> Let $f : \mathbb{R}^n \to \mathbb{R}$, $C^2$. If $x$ is such that $\nabla f(x) = 0$ and the Hassian Matrix $\nabla^2 f(x)$ is positive definite, then $x$ is a strict local minimizer.
> > If $\nabla  f(x) = 0, \nabla^2 f(x)$ negative definite, then $x$ is a strict local maximizer.
>
> > [!Note]- Proof
> > 
> > We know 
> > $$
> > f(x + h) = f(x) + \langle \nabla f(x), h \rangle + \frac{1}{2} \langle \nabla^2 f(x) h, h \rangle + R(h)
> > $$
> > With $\lim_{h \to 0} \frac{R(h)}{||h||^2} = 0$.
> > 
> > By assumption, $\nabla f(x) = 0$, and $\nabla^2 f(x)$ is positive definite matrix. By definition, $\exists c$ such that $\langle \nabla^2 f(x) h, h \rangle \ge c ||h||^2$.
> > 
> > So, 
> > $$
> > f(x + h) \ge f(x) + 0 + \frac{c}{2} ||h||^2 + R(h)
> > $$
> > But we can't guarantee that $R(h)$ is positive, and in fact, it can be negative! So now, we show that $R(h)$ could be negative, but its magnitude cannot be too large.
> > 
> > Since $\lim_{h \to 0$ \frac{R(h)}{||h||} = 0$, $\exists \delta > 0$ such that 
> > $$
> > | R(h) | < \frac{c}{2} ||h||^2 \qquad ||h|| < \delta
> > $$
> > Thus,
> > $$
> > f(x + h) \ge f(x) + \frac{c}{2} ||h||^2 > f(x) \qquad 0 < ||h|| < \delta
> > $$
> > By definition, $x$ is a strict local minimizer. 

Is the converse of this theorem also true?

Let $f : \mathbb{R}^n \to \mathbb{R}, C^2$. Assume $x$ is a local minimizer. Then $\nabla f(x) = 0$. But what about $\nabla^2 f(x)$? Does it have to be positive definite? No. As a counterexample, let $f(x,y) = x^4 + y^4$. Then, we have a strict local minimizer at $0$, but the $\nabla^2 f(x)$ is not positive definite.

Let $A$ be a symmetric $n \times n$ matrix. $A$ is **positive semi-definite** if $\langle Ah, h \rangle \ge 0$ for all $h \in \mathbb{R}^n$. Similarly, $A$ is negative semi-definite if $\langle Ah, h \rangle \ge 0$ for all $h \in \mathbb{R}^n$.
> Note that the inner product can now be 0, compared to the positive definite definition!

> [!Abstract] Theorem
> If $f : \mathbb{R} \to \mathbb{R}, C^2$ has a minimizer at $x$, then $f'(x) = 0$, $f''(x) \ge 0$ (can be 0). In other words, $\nabla^2 f(x)$ has to be positive semi-definite.
> 
> > [!Note]- Proof
> > 
> > Look at $\phi(t) = f(x + th)$. Then, $\phi(t) \in C^2$, and has a minimizer at $t = 0$. So, $\phi'(0) = \langle \nabla f, h \rangle = 0$, and $\phi''(0) = \langle \nabla^2 f(x) h, h \rangle \ge 0$. In other words, the matrix is positive semi-definite.

In particular, if $f : \mathbb{R}^n \to \mathbb{R}, C^2$, has a local minimum at $x$, then all
$$
\frac{\partial^2}{\partial x_i^2} f(x) \ge 0
$$
And similarly, if $f$ has a local maximum at $x$, then all 
$$
\frac{\partial^2}{\partial x_i^2} f(x) \le 0
$$

> [!Abstract] Proposition: (IMPORTANT FOR EXAM)
> Let $U$ be open in $\mathbb{R}^n$, $f : U \to \mathbb{R}, C^2$. Assume the **Laplacian** of $f$ at $x$ is positive for all $x \in U$.
> $$
> \Delta f(x) = \frac{\partial^2 f}{\partial x_1^2} (x) + \dots + \frac{\partial^2 f}{\partial x_n^2} (x) > 0 \qquad \forall x \in U
> $$
>
> Then, $f$ has no maximizer in $U$.
>
> > [!Note]- Proof
> > 
> > Assume by contradiction that $f$ has a maximizer in $U$, given as $x$. Then, $\nabla f(x) = 0$, and $\nabla^2 f$ is positive semi-definite. So, $\frac{\partial^2 f}{\partial x_i^2} \le 0$, meaning
> > $$
> > \Delta f(x) = \frac{\partial^2 f}{\partial x_1^2} (x) + \dots + \frac{\partial^2 f}{\partial x_n^2} (x) \le 0
> > $$
> > 
> > Which is a contradiction.

> [!Abstract] Theorem
> Let $U$ be a bounded open set, $\bar{U} = U \cup \text{Boundary of U}$ (giving us a sequentially compact set).
> 
> Let $f \in C^2 (U)$, $f$ continuous on $\bar{U}$, satisfy
> $$
> \Delta f(x) = 0 \qquad \forall x \in U
> $$
> 
> Then,
> $$
> \max_{\bar{U}} f = \max_{\text{Boundary U}} f
> $$
> In other words, the maximum always occurs at the boundary.
>
> > [!Note]- Proof
> > 
> > Because $U \subseteq \bar{U}$, $\max_{\text{Boundary U}} f \le \max_{\bar{U}} f$ trivially.
> > 
> > Look at $f_\epsilon (x) = f(x) + \epsilon ||x||^2$. Note that by this, $f_\epsilon \ge f$. Then,
> > $$
> > \Delta f_\epsilon (x) = \nabla f(x) + 2n\epsilon > 0
> > $$
> > Thus, $f_\epsilon$ has no interior maximum, and so the maximum of $f_\epsilon$ occurs at the boundary of $U$.
> > $$
> > \max_{\bar{U}} f \le \max_{\bar{U}} f_\epsilon \le \max_{\text{Boundary U}} f + \epsilon ||x||^2 \le \max_{\text{Boundary U}} f + \epsilon K
> > $$
> > Where $K$ depends on $U$. Let $\epsilon \to 0$ to get
> > $$
> > \max_{\bar{U}} f \le \max_{\text{Boundary U}} f
> > $$
> > 
> > We showed the inequalities in both directions, so we have equality. We are done.

---

## Higher Order Approximations
Let $x \in \mathbb{R}^n$, and let there be a multi-index $\alpha = (\alpha_1, \dots, \alpha_n)$ where $\alpha_i \in \{0,1\}$.

Define
$$
\begin{align*}
|\alpha| = \alpha_1 + \dots + \alpha_n \\ \alpha ! = \alpha_1 ! \dots \alpha_n ! \\
x^\alpha = x_1^{\alpha_1} \dots x_n^{\alpha_n} \\
\partial^\alpha f = \left( \frac{\partial^{|\alpha|}}{\partial x_1^{\alpha_1} \dots \partial x_n^{\alpha_n}} f \right) (x)
\end{align*}
$$

> [!Abstract] Proposition: Multinomial Formula
> $$
> (x_1 + \dots + x_n)^k = \sum_{|\alpha| = k} \frac{k!}{\alpha!} x^\alpha
> $$
>
> > [!Note]- Proof
> > 
> > We prove this by induction. Start with $n = 2$. Then, we have
> > $$
> > (x_1 + x_2)^k = \sum_{i=0}^k \frac{k!}{i! (k - i)!} x_1^i x_2^{k-i}
> > $$
> > 
> > Now, suppose that our formula is true for $n - 1$ ($n \ge 3$). Prove it for $n$.
> > $$
> > \begin{align*}
> > ((x_1 + \dots + x_{n-1}) + x_n)^k
> > &= \sum_{i=0}^k \frac{k!}{i! (k - i)!} (x_1 + \dots + x_{n-1})^i x_n^{k-i} \\
> > &= \sum_{i=0}^k \frac{k!}{i! (k - i)!} \left[ \sum_{|\beta| = i} \frac{i!}{\beta!} \tilde{x}^\beta \right]  x_n^{k-i}
> > \end{align*}
> > $$
> > 
> > Define $\alpha = (\beta, k - i)$, $\beta$ having length $i$. Then, $\alpha$ has length $k$, and
> > $$
> > \begin{align*}
> > \frac{1}{(k-i)! (\beta)!} = \frac{1}{\alpha!} \\
> > \tilde{x}^\beta x_n^{k-i} = x_1^{\beta_1} \dots x_{n-1}^{\beta_{n-1}} x_n^{k-i} = x^\alpha
> > \end{align*}
> > $$
> > 
> > So, 
> > $$
> > \sum_{i=0}^k \frac{k!}{i! (k - i)!} \left[ \sum_{|\beta| = i} \frac{i!}{\beta!} \tilde{x}^\beta \right]  x_n^{k-i} = \sum_{|\alpha| = k} \frac{k!}{\alpha!} x^\alpha
> > $$

Let $f \in C^k (\mathbb{R}^n)$. Look at
$$
\phi(t) = f(x + th), \phi : \mathbb{R} \to \mathbb{R}, C^1
$$

We know that
$$
\phi(1) = \phi(0) = \phi'(0) + \frac{1}{2} \phi''(0) + \dots + \frac{1}{(k-1)!} \phi^{k-1} (0)
$$
> The one dimensional Taylor expansion!

Express $\phi^k (t)$ in terms of partials of $f$, $k \in \mathbb{N}$.
$$
\begin{align*}
\phi' (t) 
&= \langle \nabla f (x + th), h \rangle 
= (h \cdot \nabla) (x + th) 
= h_1 \frac{\partial f}{\partial x_1} (x_1 + th) + \dots + h_n \frac{\partial f}{\partial x_n} (x + th) \\
&= [(h_1 \partial_1 + \dots + h_n \partial_n) f ] (x + th) \\
\phi''(t) 
&= \langle \nabla^2 f(x + th) h, h \rangle \\
&= [(h_1 \partial_1 + \dots + h_n \partial_n)^2 f ] (x + th) \\
\phi^k (t)
&= [(h_1 \partial_1 + \dots + h_n \partial_n)^k f ] (x + th) 
= \sum_{|\alpha| = k} \frac{k!}{\alpha!} (h^\alpha \partial^\alpha f) (x + th) \\
\end{align*}
$$

Let $t = 0$. Then, we have
$$
\frac{1}{i!} \phi^i (0) = \sum_{|\alpha| = i} \frac{1}{\alpha!} \partial^\alpha f(x) h^\alpha
$$

We have proven the following.

> [!Abstract] Theorem: Higher Order Approximations
> Let $f : \mathbb{R}^n \to \mathbb{R}, C^k$. Then,
> $$
> \begin{align*}
> f(x + th) 
> &= \sum_{j=0}^{k-1} \sum_{|\alpha| = j} \frac{1}{\alpha!} \partial^\alpha f(x) h^\alpha + \sum_{|\alpha| = k} \frac{1}{\alpha!} \partial^\alpha f(x + \theta h) h^\alpha \\
> &= \sum_{j=0}^{k-1} \sum_{|\alpha| \le k - 1} \frac{1}{\alpha!} \partial^\alpha f(x) h^\alpha + \sum_{|\alpha| = k} \frac{1}{\alpha!} \partial^\alpha f(x + \theta h) \\
> \end{align*}
> $$
>
> For some $0 < \theta < 1$
>
> > Notice the similarity with $\phi : \mathbb{R} \to \mathbb{R}, C^k$.
> > $$
> > \phi(x + h) = \sum_{i=0}^{k-1} \frac{1}{i!} \phi^i (x) h^i + \frac{1}{k!} \phi^k (x + \theta h) h^k
> > $$
> > For $0 < \theta < 1$, which is the 1-dimensional approximation formula!

--- 15

# Linear Algebra Review
Function $T : \mathbb{R}^n \to \mathbb{R}^n$ is linear if
$$
T(\alpha u + \beta v) = \alpha T(u) + \beta T(v) 
$$
For all $\alpha, \beta \in \mathbb{R}$, $u,v \in \mathbb{R}^n$.

> [!Abstract] Theorem
> If $T : \mathbb{R}^n \to \mathbb{R}^n$ is linear, then there exists a unique $m \times n$ matrix $A$ such that
> $$
> T(u) = Au
> $$
>
> > [!Note]- Proof
> > 
> > #### Uniqueness
> > Let $A,B$ be two non-unique matrices satisfying our property. Then,
> > $$
> > Au - Bu = T(u) - T(u) = 0 \Longrightarrow (A - B)u = 0
> > $$
> > 
> > Now, observe that for any row of $(A - B)$, we are taking the dot product of $u$ with that row. Let $u$ be the row, to see that the norm must be 0. This is only possible if the row is the 0 vector.
> > 
> > #### Existence
> > Let $e_1, \dots e_n$ be the standard basis. Represent $u$ as
> > $$
> > u = u_1 e_1 + \dots + u_n e_n
> > $$
> > 
> > Then,
> > $$
> > \begin{align*}
> > T(u) 
> > &= T(u_1 e_1 + \dots + u_n T(e_n) \\
> > &= u_1 T(e_1) + \dots + u_n T(e_n) \\
> > &= (T(e_1), \dots T(e_n)) 
> > \begin{pmatrix}
> > u_1 \\ \vdots \\ v_n
> > \end{pmatrix}
> > \end{align*}
> > $$

Let us have linear transformations $T : \mathbb{R}^n \to \mathbb{R}^m$, $S: \mathbb{R}^m \to \mathbb{R}^k$. Let $A,B$ be matrices such that
$$
T(u) = Au \qquad S(u) = Bu
$$

Then, the matrix of the composition of these transformations is
$$
T(S(u)) = A(Bu) = (AB) u \qquad S(T(u)) = B(Au) = (BA) u
$$
Which is the product of the matrices!

> [!Abstract] Theorem: Invertible Transformations
> $T: \mathbb{R}^n \to \mathbb{R}^n$, linear, is invertible (as a function) if and only if the corresponding matrix $A$ is invertible as a matrix if and only if $\det(A) \ne 0$.
> > We commonly determine that transformations are invertible by checking the matrices!

> [!Abstract] Theorem
> Let $A$ be an $n \times n$ matrix. Then, $A$ is invertible if if and only if $\exists c > 0$ such that 
> $$
> || Au || \ge c ||u|| \qquad u \in \mathbb{R}^n
> $$
> > By definition, $A$ is invertible if there exists a matrix $A^{-1}$ such $A A^{-1} = I$.
>
> > [!Note] Proof 
> > 
> > #### Proof ($\leftarrow$)
> > If $||Au|| \ge c||u||$ for all $u \in \mathbb{R}^n$, then the null space of $A$ is $\{0\}$, as if $Au = 0$, then $||Au|| \ge c||u||$ forces $u = 0$.
> > 
> > From linear algebra, we know that if $A$ is on finite dimensions $n \times n$, and the null space is $\{0\}$, then the range of $A$ is $\mathbb{R}^n$ and $A$ is invertible.
> > 
> > #### Proof ($\rightarrow$)
> > Conversely, if $\exists A^{-1}$ such that $A A^{-1} = A^{-1} A$, then we wish to find a $c > 0$ such that $||Au|| \ge c ||u||$.
> > 
> > Because $A^{-1} A = I$, then $A^{-1} Au = u$. 
> > $$
> > u = || A^{-1} A u || \le ||A^{-1}|| ||Au||
> > $$
> > This is the generalized Cauchy Schwarz inequality! 
> > 
> > Thus,
> > $$
> > ||Au|| \ge \frac{1}{||A^{-1}||} ||u|| 
> > $$
> > 
> > Let $c = \frac{1}{||A^{-1}||}$.
> > > Recall that $||A|| = (\sum a_{ij}^2)^{1/2}$.

Is $V$ is a vector space with bases $v_1, \dots v_n$, and also $w_1, \dots w_n$, and the bases are related by $(v_1, \dots v_n) = (w_1, \dots w_n) C$

If the matrix of $T$ with respect to $\{v_1, \dots v_n\}$ is $A$, $\{w_1, \dots w_n\}$ is $B$, then $A = C B C^{-1}$.

> [!Note] Proof
> We know that $(v_1 \dots v_n) = (w_1, \dots w_n) C$, then
> $$
> \begin{align*}
> (T(v_1), \dots T(v_n)) = (T(w_1), \dots T(w_n)) C \\
> (v_1, \dots v_n) A = (w_1, \dots w_n) CA 
> \end{align*}
> $$
> 
> So, $A = C^{-1} B C$.

-- 15.1

Let $F: \mathbb{R}^n \to \mathbb{R}^m$. Assume all partials exist. Now, define
$$
DF(x) = 
\begin{bmatrix}
\frac{\partial F_1}{\partial x_1} (x) & \dots & \frac{\partial F_1}{\partial x_n} \\
&\vdots & &\vdots \\
\frac{\partial F_m}{\partial x_1} (x) & \dots & \frac{\partial F_m}{\partial x_n} 
\end{bmatrix} =
\begin{bmatrix}
\nabla F_1(x) \\
\vdots \\
\nabla F_m (x)
\end{bmatrix}
$$
> We define the gradient of a function as a row vector.

> [!Abstract] Theorem: Mean Value Theorem
> Let $F : \mathbb{R}^m \to \mathbb{R}^n, C^1$. Fix $x, h \in \mathbb{R}^n$. Then,
> $$
> F(x + h) - F(x) = 
> \begin{bmatrix}
> \nabla F_1(x + \theta_1 h) \\
> \vdots \\
> \nabla F_m (x + \theta_m h)
> \end{bmatrix} h
> $$
> For some $0 < \theta_1 < 1, \dots, 0 < \theta_m < 1$.
> 
> > [!Note] Proof
> > 
> > Apply the MVT for each $F_i : \mathbb{R}^n \to \mathbb{R}, C^1$.

> [!Abstract] Theorem
> Let $F : \mathbb{R}^n \to \mathbb{R}^m, C^1$. Then,
> $$
> \lim_{h \to 0} \frac{F(x+h) - F(x) - DF(x) h}{||h||} = 0
> $$
> 
> > [!Note]- Proof
> > 
> > The $i^{th}$ component of the above quantity, from the previous chapter, is
> > $$
> > \frac{F_i (x+h) - F_i (x) - \langle \nabla F_i (x), h \rangle}{||h||} \to 0
> > $$
 
> [!Abstract] Theorem
> Let $F : \mathbb{R}^n \to \mathbb{R}^m$. Fix $x$, assume $\exists A$ $m \times n$ matrix such that 
> $$
> \lim_{h \to 0} \frac{F(x+h) - F(x) - Ah}{||h||} = 0
> $$
> 
> Then, all partials $\frac{\partial F_i}{\partial x_j} (x)$ exist, and $A = DF(x)$.
> 
> > [!Note] Proof
> >
> > Look at the $i^{th}$ component.
> > $$
> > \begin{align*}
> > \lim_{h \to 0} \frac{F_i (x+h) - F_i (x) - \langle \nabla F_i (x), h \rangle}{||h||} \to 0 \\ 
> > \lim_{h \to 0} \frac{F_i (x+h) - F_i (x) - \langle (a_{i1}, \dots a_{in}), (h_1, \dots h_n) \rangle}{||h||} \to 0
> > \end{align*}
> > $$
> > 
> > In particular, for $h = t e_j$, $t \to 0$, we get
> > $$
> > \begin{align*}
> > \lim_{t \to 0} \frac{F_i (x + te_j) - F_i (x) - t a_{ij}}{|t|} = 0 \\
> > \lim_{t \to 0} \frac{F_i (x + te_j) - F_i (x) - t a_{ij}}{t} = 0 \\
> > \lim_{t \to 0} \frac{F_i (x + te_j) - F_i (x)}{t} = a_{ij} \\
> > \frac{\partial F_i}{\partial x_j} (x) = a_{ij}
> > \end{align*}
> > $$

$F : \mathbb{R}^n \to \mathbb{R}^m$  is **differentiable** at $x$ if there exists an $A$, $m \times m$ matrix such that
$$
\lim_{h \to 0} \frac{F_i (x + h) - F_i (x) - Ah}{||h||} = 0
$$
So, $F \in C^1 (\mathbb{R}^n)$ $\to$ F is differentiable $\forall x \in \mathbb{R}^n$ $\to$ $DF(x)$ exists $\forall x \in \mathbb{R}^n$. These are strict implications!

> [!Example] Example: Counterexamples
> Example of $f : \mathbb{R}^2 \to \mathbb{R}$ for which $Df(x)$ exists $\forall x \in \mathbb{R}^2$, but there does not exist an $A$ such that
> $$
> \frac{f(x+h) - f(x) - [a_1 h_1 + a_2 h_2]}{||h||} = 0
> $$
>
> Is
> $$
> f(x_1, x_2) = \begin{cases}
> \frac{x_1 x_2}{x_1^2 + x_2^2} & (x_1, x_2) \ne (0,0) \\
> 0 & (x_1, x_2) = (0,0)
> \end{cases}
> $$

> [!Example] Example
> Let $F : \mathbb{R}^n \to \mathbb{R}^m, C^1$. Assume $F(0) = 0, DF(0)$ satisfies $|| DF (0) h || \ge ||h||, \forall h \in \mathbb{R}^n$.
>
> Prove that $\exists \delta > 0$ such that $|| F(h) || \ge \frac{1}{2} ||h||, \forall ||h|| < \delta$.
>
> We know that
$$
\lim_{h \to 0} \frac{F(x+h) - F(0) - DF(0) h}{||h||} = 0
$$

$$
\begin{align*}
|| F(h) || = || F(h) - DF(0) h + DF(0) h || \ge || DF(h) || - || F(h) - DF(0) h || \\
\frac{|| F(h) ||}{|| h ||} = \frac{|| F(h) - DF(0) h + DF(0) h ||}{|| h ||} \ge \frac{|| DF(h) ||}{|| h ||} - \frac{|| F(h) - DF(0) h ||}{|| h ||} \ge 1/2 \\
\end{align*}
$$

Since
$$
\lim_{h \to 0} \frac{F(x+h) - F(0) - DF(0) h}{||h||} = 0
$$
We know that $\exists \delta > 0$ such that 
$$
\frac{|| F(h) - DF(0) h ||}{|| h ||} \le \frac{1}{2}
$$

...

---

15.3 - 5

We have two functions $(u,v) : \mathbb{R}^2 \to \mathbb{R}^2, C^2$. Furthermore, we have a function $w : \mathbb{R}^2 \to \,mathbb{R}$.

By slight abuse of notation, call $w$ a function of $u,v$, and $u,v$ a function of $x,y$.

By assumption, $w$ is harmonic, so
$$
\frac{\partial^2 w}{\partial u^2} (u,v) + \frac{\partial^2 w}{\partial v^2} (u,v) = 0
$$
And we have the Cauchy-Remainder EQuations
$$
\begin{align*}
\frac{\partial u}{\partial x} (x,y) = \frac{\partial v}{\partial y} (x,y) \\
\frac{\partial v}{\partial x} (x,y) = - \frac{\partial u}{\partial y} (x,y)
\end{align*}
$$

We wish to show that
$$
\left( \frac{d^2}{dx^2} + \frac{d^2}{dy^2} \right) (w(u,v)) (x,y) = 0
$$

$$
\begin{align*}
\frac{\partial}{\partial x} w(u(x,y), v(x,y)) 
&= \frac{\partial w}{\partial u} (u,v) \frac{\partial u}{\partial x} + \frac{\partial w}{\partial v} (u,v) \frac{\partial v}{\partial x} \\
\frac{\partial^2}{\partial x^2} w(u(x,y), v(x,y)) 
&= \left[ \frac{\partial^2 w}{\partial u^2} (u,v) \frac{\partial u}{\partial x} + \frac{\partial^2 w}{\partial u \partial v} (u,v) \frac{\partial v}{\partial x} \right] \frac{\partial u}{\partial x} \\
&\quad + \frac{\partial w}{\partial u} (u,v) \frac{\partial^2 u}{\partial x^2} + \left[ \frac{\partial^2}{\partial u \partial v} (u,v) \frac{\partial u}{\partial x} + \frac{\partial^2 w}{\partial v^2} (u,v) \frac{\partial v}{\partial x} \right] \frac{\partial v}{\partial x} \\
&\quad + \frac{\partial w}{\partial v} (u,v) \frac{\partial^2 u}{\partial x^2}
\end{align*}
$$
> The $y$ case is the same, just replace the $x$'s with $y$'s.

We claim that the sum of these terms is 0, and with our assumptions we can show that this is true. 
> There is a theorem, if $u$ and $v$ satisfy the Cauchy Riemann equations, then they too are Harmonic individually. We can find this by differentiating the Cauchy Riemann equations

Just show 3 cancellations and we're done T-T


---

Inverse Function Theorem / Implicit Function Theorem
> Functions on R^n to R^n.

# 16.1
> [!Abstract] Theorem: Inverse Function Theorem (One Dimension)
> Let $f : \mathbb{R} \to \mathbb{R}, C^1$, let $x_0 \in \mathbb{R}$ such that $f'(x) \ne 0$.
>
> Then, there exists a **neighborhood** $U$ around $x_0$ (open set containing $x_0$) and a **neighborhood** $V$ around $f(x_0)$ such that
> $$
> f : U \to V
> $$
> Is 1-1, onto, $f^{-1} : V \to U$ is $C^1$ and $f^{-1} (y)' = \frac{1}{f'(f^{-1}(y))}$ for all $y \in V$.
>
> > [!Note] Proof
> > 
If we know that $f^{-1} : V \to C$ is $C^1$, then the formula is immediate.

Note that proving the formula is just a chain rule.

WLOG, $f'(x_0) > 0$. Let $U = (x_0 - R, x_0 + R)$ be such that 
$$
f'(t) > 0 \qquad t \in [x_0 - R, x_0 + R]
$$
In other words, take the open set such that $f$ is strictly increasing on it.

Then $f : [x_0 - R, x_0 + R] \to [ f(x_0 - R), f(x_0 + R) ]$ is 1-1, onto because of the IVT, and
$$
f : (x_0 - R, x_0 + R) \to ( f(x_0 - R), f(x_0 + R) )
$$
Is also 1-1 and onto. Furthermore, $f^{-1}$ is $C^1$ as the function is strictly increasing and continuous over the entire interval.

> [!Abstract] Theorem: Inverse Function Theorem (Two Dimensions)
> Let $F : \mathbb{R}^2 \to \mathbb{R}^2$, $C^1$. Assume we have a point $(x_0, y_0)$ such that the derivative matrix $DF$ of $f$ at this point is invertible (the derivative is 0).
>
> Then, there exists a neighborhood $U$ of $(x_0, y_0)$, $V$ of $F(x_0, y_0)$ such that
$$
F : U \to V
$$
Is 1-1, onto, $F^{-1} : V \to U$ is $C^1$, and 
$$
D(F^{-1}) (y) = \left( DF ( F^{-1}(y)) \right)^{-1}
$$

> If we know that $F^{-1}$ is $C^1$, then the formula follows from the chain rule.

> [!Example] Example
$$
F(x,y) = (x^2 - y^2, 2xy)
$$
We can also represent this function with complex numbers like as
$$
F(x + iy) = (x + iy)^2 = x^2 - y^2 + 2ixy
$$

Now, 
$$
\det DF(x,y) = \det
\begin{bmatrix}
2x & -2y \\ 2y & 2x
\end{bmatrix} = 4 (x^2 +  y^2) \ne 0 \qquad \forall (x,y) \ne (0,0)
$$
Thus, if $(x_0, y_0) \ne (0,0)$, there exists a neighborhood $U$ of $(x_0, y_0)$, $V$ of $(x_0^2 - y_0^2, 2 x_0 y_0)$ such that
$$
F : U \to V
$$
Is 1-1, onto.

What about $(0,0)$? Does there exist a neighborhood $U$ of $(0,0$ such that $F$ is 1-1 on $U$? 

No. $F(x,y) = F(-x,-y)$, so we cannot find any such neighborhood. 

---

Let $F : \mathbb{R}^2 \to \mathbb{R}^2, C^1$. Assume $(x_0, y_0)$ is such that $DF(x_0, y_0)$ is invertible. Then there exists a neighborhood $U$ of $(x_0, y_0)$ and neighborhood $V$ of $F(x_0,y_0)$ such that
- $F : U \to V$ is 1-1 and onto
- $F^{-1} : V \to U$ is $C^1$

> [!Example] 
$$
F(x,y) = (x^2 - y^2, 2xy)
$$

Our hypotheses hold at any $(x_0, y_0) \not> (0,0)$, but fails at $(0,0)$.

Previously, we showed that there does not exist a $U$ neighborhood of $(0,0)$ such that $F$ is 1-1 on $U$, as $F(x,y) = F(-x,-y)$. 

However, $F(B_1 (0)) = B_1 (0)$, so 2 holds!

> [!Note] Proof
> 
> Let $x = r \cos \theta, y = r \sin \theta$. 
> $$
> F(x,y) = (r^2 (\cos^2 \theta - \sin^2 \theta), 2 r \sin\theta \cos\theta) = (r^2 \cos(2\theta), r^2 \sin(2\theta))
> $$
> 
> So we always remain within our ball!

---

> [!Example] Example: 
$$
F(x,y) = (e^x \cos y, e^x \sin y)
$$

We have
$$
DF (x,y) =
\begin{bmatrix}
e^x \cos y & -e^x \sin y \\
e^x \sin y & e^x \cos y
\end{bmatrix}
$$
Where $\det (DF) = e^{2x} \ne 0$. So, our hypothesis holds everywhere! However, note that our theorem does not hold globally, just locally!
- $F$ is not 1-1 globally as we can find $F(x,y) = F(x, y + 2k\pi)$. 
- $F$ is not onto globally, as there does not exist any $(x,y)$ such that $F(x,y) = (0,0)$.

> [!Example] Example
Let $\phi : \mathbb{R}^2 \to \mathbb{R}, C^1$, and
$$
F(x,y) = (\phi(x,y), \phi^2 (x,y))
$$

We find derivative matrix
$$
F(x,y) = 
\begin{bmatrix} 
\frac{\partial \phi}{\partial x} & \frac{\partial \phi}{\partial y} \\
2 \phi \frac{\partial \phi}{\partial x} & 2 \phi \frac{\partial \phi}{\partial y}
\end{bmatrix} 
$$
As the determinant of this matrix is always 0, we find that $F$ is not invertible anywhere.

> [!Example] Example
We want a $F : \mathbb{R}^2 \to \mathbb{R}^2, C^1$ such that
$$
\det (DF(x_0, y_0)) = 0
$$
Yet $F$ is 1-1 and onto.

Let $F(x,y) = (x^3, y^3)$. Then, even though the determinant of the derivative matrix is $x = 0$ or $y = 0$, $F$ is 1-1 and onto.

Let $F : \mathbb{R}^2 \to \mathbb{R}^2, C^1$ and assume that $DF(0,0)$ is not invertible, ad $F$ is 1-1, $F$ is onto. Is it possible for $F^{-1}$ to be $C^1$, so all 3 conclusions of our theorem hold while the hypothesis does not?

No! By way of contradiction, as
$$
F \circ F^{-1} (x,y) = (x,y)
$$
Then $(DF) F^{-1} (x,y) \circ (DF^{-1}) (x,y) = I$, but $DF$ is not invertible at some point, which is not possible, as its inverse exists!

---

16.2


> [!Note] Proof
Recall that the following are equivalent. For an $n \times n$ matrix $A$, 
- $A$ is invertible
- $\exists c > 0$ such that $|| A h || \ge c ||h||$, $\forall h \in \mathbb{R}^n$.

We say that $F : O \to \mathbb{R}^n$ is **stable** if $\exists c > 0$ such that
$$
|| F(x) - F(y) || \ge c || x - y || \qquad \forall (x,y) \in O
$$
> [!Info] Remark
> $F$ stable implies that $F$ is 1-1.
> 
> As a brief proof, if $F(x) = F(y)$, then $|| F(x) - F(y) || \ge || x - y || \to x = y$.
> > Note that $F$ is stable if and only if $F^{-1}$ is Lipschitz (as the inequalities are flipped!)

> [!Abstract] Proposition:
> Let $A$ be an $n \times n$ matrix, and assume that $\exists c > 0$ such that
> $$
> || A h || \ge c || h || \qquad h \in \mathbb{R}^n
> $$
> Let $B$ be an $n \times n$ matrix such that $|| A - B || \le \frac{c}{2}$. Then, $|| Bh || \ge \frac{c}{2} || h ||$. In other words, if a matrix is 1-1, then all other matrices sufficiently close to it are also 1-1.
>
> > [!Note] Proof
> > 
> > $$
> > || Bh || = || Ah + (B - A) h || \ge || Ah || - || (B - A) h || \ge c ||h|| - \frac{c}{2} ||h|| \ge \frac{c}{2} ||h||
> > $$

We now prove the 1-1 part of the inverse function theorem.

> [!Abstract] Theorem
Let $F : O \to \mathbb{R}^n, C^1$, $O$ open. Assume that we have a point $x^*$ such that the derivative matrix at $x^*$, $DF(x^*)$, is invertible. Then there exists a neighborhood of $x^*$ such that
- The derivative matrix of $F$ is invertible. $\forall x \in U$.
- $F$ is stable on $V$, implying $F$ is 1-1 on $U$.

For point 1, look at $\det DF(x^*) \ne 0$. Thus, $\exists U$ neighborhood of $x^*$ such that $\det DF(x) \ne 0$ on $U$.

For point 2, look at $F : B_r (x^*) \to \mathbb{R}^n$. If $x,y$ belong to the ball $B_r (x^*)$, we have
$$
F(x) - F(y) = 
\begin{bmatrix}
\nabla F_1 (p_1) \\
\vdots \\
\nabla F_n (p_n) 
\end{bmatrix} (x - y)
$$
For some $p_1, \dots p_n$ on the line from $x$ to $y$.

As we know that $DF(x^*)$ is invertible, then $\exists c > 0$ such that
$$
|| DF(x^*) h || \ge c || h || \qquad \forall h
$$
If $r$ is so small that 
$$
|| DF(x^*) - \begin{bmatrix}
\nabla F_1 (p_1) \\
\vdots \\
\nabla F_n (p_n) 
\end{bmatrix} || < \frac{c}{2}
$$
For all $p_1, \dots p_n \in B_r (x^*)$. Then,
$$
|| B (x - y) || \ge \frac{c}{2} || x - y ||
$$

---

16.3

> [!Info] Lemma
> Let $U$ open in $\mathbb{R}^n$, $F : U \to \mathbb{R}^n$ of $C^1$. Assume that the derivative matrix of $F$ is invertible $\forall x \in U$.
>
> Let $E(x) = || F(x) - y ||^2$, the distance between $F(x)$ and $y$. If $E$ has an (interior) minimizer at $x \in U$, then $F(x) = y$.
>
> > [!Note]- Proof
> > 
> > Suppose we have:
> > - A function $G$ that transforms $x$ to $F(x) - y$.
> > - A function $\phi$ that takes the squared norm of its input, $\phi(z) = \langle z, z \rangle$
> > 
> > Then, $E(x) = (\phi \circ G) (x) = \phi(G(x))$. Assume $x$ is a minimizer of $E$. Then, $\nabla E(x) = 0$
> > $$
> > \nabla E(x) = (\nabla \phi) (G(x)) * DG(x) = (\nabla \phi) (G(x)) * DF(x) = 0
> > $$
> > Because $DF(x)$ is invertible, then
> > $$
> > (\nabla \phi) (G(x)) = 0
> > $$
> > 
> > Note that because $\phi(z) = \langle z, z \rangle$, $\nabla \phi(z) = 2z$. So,
> > $$
> > (\nabla \phi) (G(x)) = 2 G(x) = 0 \Longrightarrow G(x) = 0
> > $$
> > And as $G(x) = F(x) - y = 0, F(x) = y$.

Recall that we have a $F : O \to \mathbb{R}^n, C^1$, $O$ open, and $x^* \in O$ where $DF(x^*)$ is invertible. We know (from the previous section) that there exists a neighborhood $U$ of $x^*$ such that $DF(x)$ is invertible for $x \in U$ and $\exists $c > 0$ such that
$$
|| F(x) - F(y) || \ge c || x || \qquad \forall x,y \in U
$$

> [!Abstract] Theorem
> Assume the above. Then, $F(U)$ is open. 
>
> > [!Note] Proof
> > 
> > Let $y_0 \in F(U)$. By assumption, we know that $\exists x_0 \in U$ such that $F(x_0) = y_0$.
> > 
> > Let $S = \{ x \in U : ||x - x_0|| = R\}$, the sphere of radius $R$ centered around $x_0$. We know that all points along this sphere are greater than $||F(x) - F(x_0)|| \ge c || x - x_0 || = cR$.
> > 
> > We will show that if $|| y - y_0 || < \frac{cR}{2}$, then there exists an $x \in B_R (x_0)$ such that $F(x) = y$.
> > 
> > Look at $\min_{x \in \bar{B}_R (x_0)} || F(x) - y ||$, where $\bar{B}_R (x_0)$ is the closed ball of radius $R$ around $x_0$ (includes the border). A minimizer exists, because we have a continuous function on a compact set. We furthermore rule out a boundary minimizer.
> > 
> > Let $x \in S$ (so, $||x - x_0|| = R$). We know that $||F(x) - y_0|| = ||F(x) - F(x_0)|| \ge cR$. So,
> > $$
> > || F(x) - y || \ge || F(x) - F(x_0) || - || F(x_0) - y || > \frac{cR}{2}
> > $$
> > 
> > But $|| F(x_0) - y || < \frac{cR}{2}$, $x_0 \in B_R (x_0)$, so no point on $S$ can be the minimizer. So, the minimizer must be in the interior, so by the previous lemma, the minimizer must be such that $F(x) = y$.

Thus, there exists a neighborhood $U$ of $x^*$ such that $DF(x)$ is invertible for all $x \in U$, $\exists c$ such that
$$
|| F(x) - F(y) || \ge c || x - y || \qquad \forall x,y \in U
$$
And $F(U) = V$. By general proprties of functions, $F^{-1} : V \to U$ is well defined. To show that it is $C^1$, we will prove that
$$
(DF^{-1} (y)) = ( DF(x) )^{-1}
$$

To prove this, it suffices to show that 
$$
\lim_{k \to 0} \frac{|| F^{-1}(y + k) - F^{-1}(y) - [ DF(x) ]^{-1} (k) ||}{||k||} = 0
$$
We use the notation $F(x) = y, F(x + h) = y + k$. On the LHS, we have 
$$
\begin{align*}
&\lim_{k \to 0} \frac{|| (x + h) - x - [DF(x)]^{-1} [F(x+h) - F(x)] ||}{||k||} \\
&\qquad = \lim_{k \to 0} \frac{|| [DF(x)]^{-1} [ DF(x) [h] - [F(x+h) - F(x)]] ||}{||k||} \\
&\qquad \le \lim_{k \to 0} \frac{|| [DF(x)]^{-1} [F(x+h) - F(x) - DF(x) h] ||}{||k||} \\
\end{align*}
$$

We want to show that $||k|| \ge C ||h||$.
$$
|| F(x+h) - F(x) || \ge C ||h|| \Longrightarrow ||k|| \ge C ||h||
$$

So, we have
$$
\le \lim_{k \to 0} \frac{ [DF(x)]^{-1}}{c} \frac{|| [F(x+h) - F(x) - DF(x) h] ||}{||h||} \to 0
$$
This is a first order approximation! So, this goes to 0 as $k \to \infty$, as then $h \to 0$.

