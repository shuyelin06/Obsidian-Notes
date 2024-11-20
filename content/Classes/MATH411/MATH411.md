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

> [!Abstract] Theorem: Compositions of Limits
> Let $A \subseteq \mathbb{R}^n$, $x^* \in A$ be a limit point. Let $f : A \to \mathbb{R}$, $g : A \to \mathbb{R}$ be functions, $l_1, l_2 \in \mathbb{R}$ such that
> $$
> \lim_{x \to x^*} f(x) = l_1 \qquad 
> \lim_{x \to x^*} g(x) = l_2
> $$
> 
> Then:
> 1. $$
>    \lim_{x \to x^*} f(x) + g(x) = l_1 + l_2
>    $$
> 2. $$
>    \lim_{x \to x^*} f(x) g(x) = l_1 l_2
>    $$
> 3. If $g(x) \ne 0$ for all $x \in A$, and $l_2 \ne 0$,
>    $$
>    \lim_{x \to x^*} \frac{f(x)}{g(x)} = \frac{l_1}{l_2}
>    $$

The quotient rule for limits is the most interesting of the 3, and there is a broad study of limits of quotients
$$
\lim_{x \to x^*} \frac{f(x)}{g(x)}
$$
Where $\lim_{x \to x^*} f(x) = \lim_{x \to x^*} g(x) = 0$.

These limits can occur frequently, and we commonly ask if such limits exist (think of derivatives!).

> [!Example]+ Example: Limit Example
> $$
> \lim_{(x,y) \to (0,0)} \frac{x^3}{x^2 + y^2}
> $$
> 
> We ask if this limit exists. To determine this, we will establish a bound on the function.
> $$
> \left| \frac{x^3}{x^2 + y^2} \right| \le \left| \frac{x^3}{x^2} \right| = |x| 
> $$
> 
> For any $(x,y)$ where $x$ and $y$ are both not equal 0, our function is bounded by $|x|$! Thus, as $(x,y) \to (0,0)$, $|x| \to 0$, so by the Comparison Lemma, $| \frac{x^3}{x^2 + y^2} | \to 0$.
> 
> Thus, the limit exists and is equal to 0! 

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

We can also use the following property to show that such limits exist.

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

For $1 \le i \le n$, we define the **partial derivative of $f$ with respect to $x_i$ at $x$ as**
$$
\frac{\partial f}{\partial x_i} (x) = \lim_{t \to 0} \frac{f(x + t e_i) - f(x)}{t}
$$
if the latter limit exists. Note that $e_i$ is the $i^{th}$ basis vector, 
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

> [!Warning] Differentiability Need Not Imply Continuity
> In the single-variable case, a function with a derivative was continuous. However, this is no longer true in multiple variables! 
>
> A function with first-order derivatives need not be continuous. Consider the following example.

> [!Example]+ Example: Differentiability Need Not Imply Continuity
> Define
> $$
> f(x,y) = 
> \begin{cases}
> \frac{xy}{x^2 + y^2} & (x,y) \ne (0,0) \\
> 0 & (x,y) = (0,0)
> \end{cases}
> $$
> 
> We show that the partial derivatives of the function exist at $(0,0)$. For all $t$,
> $$
> f(0 + te_i) = f(t,0) = 0
> $$
> So,
> $$
> \frac{\partial f}{\partial x_i} (0,0) = \lim_{t \to 0} \frac{f(0 + t e_i) - f(0)}{t} = \lim_{t \to 0} \frac{f(t,0) - f(0,0)}{t} = 0
> $$
> 
> However, this function is not continuous! For sequence $\{(\frac{1}{k}, \frac{1}{k})\} \to 0$, $f(\frac{1}{k},\frac{1}{k}) = \frac{1}{2}$ for all $k$, but $f(0) = 0$!

It is only if all partials are continuous, that our theorems from the single-variable case hold.

We say that $f$ is **continuously differentiable, $C^1$** if it has first-order partial derivatives such that each partial derivative $\frac{\partial f}{\partial x_i}$ is continuous for $1 \le i \le n$.

---

Let's now consider second-order partial derivatives, denoted like
$$
\frac{\partial f}{\partial x_j \partial x_i}
$$
Where we apply the partial derivative of $x_i$ first, then $x_j$ after.
> Order matters! There are some functions where swapping the order of derivatives changes the result.

- We say $f$ has **second-order partial derivatives** of it has first-order partials, such that for $1 \le i \le n$, each $\frac{\partial f}{\partial x_i}$ also has first-order partial derivatives (of every variable).
- We say $f$ has **continuous second-order partial derivatives** if it has second-order partial derivatives, and each $\frac{\partial^2 f}{\partial x_i \partial x_j}$ are continuous.

> [!Abstract] Theorem: Partial Derivative Order
> Let $O \subseteq \mathbb{R}^n$ open, and let $f : O \to \mathbb{R}$ have continuous second-order partial derivatives. Then, for any two $1 \le i,j \le n$, and any $x \in O$,
> 
> $$
> \frac{d}{d x_i} \left( \frac{\partial f}{\partial x_j} \right) = \frac{d}{d x_j} \left( \frac{\partial f}{\partial x_i} \right)
> $$
>
> > [!Note]- Proof (TODO)
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
Recall that in the single variable case, we had the Mean Value Theorem.

> [!Abstract] Theorem: Mean Value Theorem 
> Let $f:[a,b] \to \mathbb{R}$ be continuous, and differentiable on $(a,b)$. Then, $\exists c \in (a,b)$ such that 
> $$
> f(b) - f(a) = f'(c) (b - a)
> $$

This is a really useful theorem! In this section, we generalize it to multiple variables.

This generalization requires we use the single-variable MVT! 

> [!Abstract] Lemma: Mean Value Lemma
> Let $O \subseteq \mathbb{R}^n$ open, and let $1 \le i \le n$. Let $f : O \to \mathbb{R}$ have a partial derivative with respect to $x_i$ for all $x \in O$.
>
> Let $x \in O$, and $a$ be a real number such that the segment between $x$ and $x + ae_i$ lies in $O$. Then, $\exists \theta, 0 < \theta < 1$ such that
> $$
> f(x + ae_i) - f(x) = \frac{\partial f}{\partial x_i} (x + \theta a e_i) a
> $$
> > Intuition: If we view our function along an axis, we get a function on one-variable. On this, we can apply single-variable MVT!
>
> > [!Note]- Proof
> > 
> > Let $I$ be the open interval of real numbers containing 0 and $a$. Note that by assumption, $\forall t \in I$, $x + te_i$ is in our open set $O$.
> > 
> > Now, define $\phi(t) = f(x + te_i)$. Then, as $f$ has a partial derivative with respect to $x_i$, we find that $\phi(t)$ is differentiable, whose derivative is given as
> > $$
> > \phi'(t) = \frac{\partial f}{\partial x_i} (x + te_i)
> > $$
> > 
> > Thus, we can apply the single-variable MVT to find a $0 < \theta < 1$ such that
> > $$
> > \begin{align*}
> > \phi(a) - \phi(0) = \phi'(\theta a) (a - 0) \\
> > f(x + ae_i) - f(x) = \frac{\partial f}{\partial x_i} (x + \theta a e_i) a
> > \end{align*}
> > $$

We use this Lemma to prove the following.

> [!Abstract] Proposition: Mean Value Proposition
> Let $f : \mathbb{R}^n \to \mathbb{R}$ be a function. Assume all partials $\frac{\partial f}{\partial x_i}$ exist $\forall x \in \mathbb{R}^n$, $\forall i \in \{1, \dots n\}$.
> 
> Choose an $x \in \mathbb{R}^n$, and an offset $h \ne 0, h \in \mathbb{R}^n$. Then, there exists a $z_1, \dots z_n$ in the ball around $x$ of radius $||h||$ ($B_{||h||} (x)$) such that
> $$
> f(x + h) - f(x) = \frac{\partial f}{\partial x_1} (z_1) h_1 + \dots + \frac{\partial f}{\partial x_n} (z_n) h_n
> $$
>
> > [!Note]- Proof
> > 
> > We prove this for $n = 2$, though the proof can very easily be extended to more dimensions.
> > 
> > Let $x = (x_1, x_2)$, $x + h = (x_1 + h, x_2 + h)$. Look at the difference. Our goal is to expand this difference into a sum of differences along one variable (only one variable changes), so that we can apply the Mean Value Lemma on each term!
> > $$
> > \begin{align*}
> > f(x_1 + h, x_2 + h) - f(x_1, x_2) 
> > &= f(x_1 + h, x_2 + h) - f(x_1, x_2 + h_2) \\
> > &\qquad + f(x_1, x_2 + h_2) - f(x_1, x_2)
> > \end{align*}
> > $$
> > 
> > This gives us two differences, where only one variable is changing in each. In other words, we have two differences in one-dimension!
> > $$
> > f(x_1 + h, x_2 + h) - f(x_1, x_2 + h_2) \qquad f(x_1, x_2 + h_2) - f(x_1, x_2)
> > $$
> > 
> > Thus, by the Mean Value Lemma, 
> > $$
> > \begin{align*}
> > f(x_1 + h, x_2 + h) - f(x_1, x_2 + h_2) = \frac{\partial f}{\partial x_1} (x_1 + \theta h_1, x_2 + h_2) h_1 \\
> > f(x_1, x_2 + h_2) - f(x_1, x_2) = \frac{\partial f}{\partial x_2} (x_1, x_2 + \theta_2 h_2) h_2 \\
> > f(x_1 + h, x_2 + h) - f(x_1, x_2) = \frac{\partial f}{\partial x_1} (x_1 + \theta h_1, x_2 + h_2) h_1 + \frac{\partial f}{\partial x_2} (x_1, x_2 + \theta_2 h_2) h_2
> > \end{align*}
> > $$
> > 
> > Let $z_1 = (x_1 + \theta_1 h_1, x_2 + h_2)$, and $z_2 = (x_1, x_2 + \theta_2 h_2)$. Note that each $z_i$ is within the ball of $B_{||h||} (x)$. We are done!

Recall that in our definitions of partial derivatives, we differentiate a function with respect to one of the axes
$$
\lim_{t \to 0} \frac{f(x + te_i) - f(x)}{t}
$$
But what if we wanted to differentiate in a direction that isn't aligned with the axes? This is where directional derivatives come in!

---

Let $O \subseteq \mathbb{R}^n$ open, and consider the function $f : O \to \mathbb{R}^n$. For a point $x \in O$, and direction $h$, we define the **directional derivative** as
$$
\frac{\partial f}{\partial h} (x) = \lim_{t \to 0} \frac{f(x + tp) - f(x)}{t}
$$

If the limit exists.

Now let's define the **gradient** of the function, $\nabla f$, as the row vector
$$
\nabla f(x) = \left( \frac{\partial f}{\partial x_1}, \dots, \frac{\partial f}{\partial x_n} \right)
$$
In some cases, we can calculate the directional derivative using the gradient, which can be a lot easier than taking a limit!

> [!Abstract] Theorem: Directional Derivative Theorem
> Let $O \subseteq \mathbb{R}^n$ open, and let $f : \mathbb{R}^n \to \mathbb{R}$ be $C^1$.
> 
> Then, $\forall x \in O$, and all directions $\forall h \ne 0$, the function has a directional derivative at $x$ in the direction $h$, which can be calculated as
> $$
> \frac{\partial f}{\partial h} = \lim_{t \to 0} \frac{f(x + th) - f(x)}{t} = \langle \nabla f(x), h \rangle = \sum_{i=1}^n \frac{\partial f}{\partial x_i} (x) h_i
> $$
> In other words, the inner product of $h$ with the gradient of the function!
>
> > [!Note]- Proof
> > 
> > By the Mean Value Proposition, 
> > $$
> > \begin{align*}
> > \frac{f(x + th) - f(x)}{t} 
> > &= \frac{1}{t} \left( \frac{\partial f}{\partial x_1} (z_1) t h_1 + \dots + \frac{\partial f}{\partial x_n} (z_n) t h_n \right) \\
> > &= \frac{\partial f}{\partial x_1} (z_1) h_1 + \dots + \frac{\partial f}{\partial x_n} (z_n) h_n
> > \end{align*}
> > $$
> > For $z_1, \dots z_n \in B_{||th||} (x)$. Then, as $t \to 0$, the ball of $B_{||th||} (x)$ will shrink towards $x$, forcing all $z_i$'s to converge to $x$! Thus, as $t \to 0,$ we have
> > $$
> > \frac{\partial f}{\partial h} = \lim_{t to 0} \frac{f(x + th) - f(x)}{t} = \frac{\partial f}{\partial x_1} (x) h_1 + \dots + \frac{\partial f}{\partial x_n} (x) h_n
> > $$

> Note that sometimes the directional derivative may be denoted as
> $$
> \frac{\partial f}{\partial h} = \frac{d}{dt} \bigg|_{t=0} f(x + th)
> $$

> [!Abstract] Theorem: The Mean Value Theorem (Multi-Variable)
> Let $f : \mathbb{R}^n \to \mathbb{R}$ be continuously differentiable. Also let $x \in \mathbb{R}^n$, $h \in \mathbb{R}^n$ where $h \ne 0$.
> 
> Then, if the segment joining $x, x+h$ lies in $O$, then there exists $0 < \theta < 1$ such that
> $$
> f(x + h) - f(x) = \langle \nabla f(x + \theta h), h \rangle
> $$
>
> > This is the Mean Value Proposition, with the additional assertion that $z_1, \dots z_n$ are assumed to be at the same point.
>
> > [!Note]- Proof
> > 
> > Let $\phi : \mathbb{R} \to \mathbb{R}$, $\phi(t) = f(x + th)$. We know that for $t = 1, 0$, we have
> > $$
> > \phi(1) = f(x + h) \qquad \phi(0) = f(x)
> > $$
> > 
> > Then, $f(x + h) - f(x) = \phi(1) - \phi(0) = \phi'(\theta) (1 - 0)$, $0 < \theta < 1$, by the single-variable MVT, and furthermore, as the derivative of $\phi(t)$ is the directional derivative,
> > $$
> > f(x + h) - f(x) = \phi'(\theta) = \langle \nabla f(x + \theta h), h \rangle
> > $$

We can also use directional derivatives to make a few extra inferences.

Note that if $p$ is a vector of norm 1, we can interpret the directional derivative as the rate of change in a particular direction! 

> [!Abstract] Theorem: Fastest Rate of Change
> Let $f : \mathbb{R}^n \to \mathbb{R}$, $C^1$. Fix $x$, and assume $\nabla f(x) \ne 0$. Then, the maximum of the directional derivative at $x$ is given as
> $$
> \max_{||P|| = 1} \frac{\partial f}{\partial P} (x)
> $$
> Is attained for
> $$
> P = \frac{\nabla f(x)}{|| \nabla f (x) ||}
> $$
> In other words, the direction of the gradient.
> 
> > [!Note]- Proof
> > 
> > If $||P|| = 1$, we have
> > $$
> > \frac{\partial f}{\partial P} (x) = \langle \nabla f(x), P \rangle
> > $$
> > By Cauchy-Schwarz, this is
> > $$
> > \le || \nabla f(x) || \cdot || P || = || \nabla f(x) ||
> > $$
> > We have an upper bound on our directional derivative! We can attain our upper bound if $P = \frac{\nabla f(x)}{|| \nabla f(x) ||}$.
> > $$
> > \begin{align*}
> > \langle \nabla f(x), P \rangle 
> > &= \langle \nabla f(x), \frac{\nabla f(x)}{|| \nabla f(x) ||} \rangle \\ 
> > &= \frac{1}{|| \nabla f(x) ||} \langle \nabla f(x), \nabla f(x) \rangle \\
> > &= || \nabla f(x) ||
> > \end{align*}
> > $$
> > We've found a maximizer.

Furthermore, we can use directional dervatives to prove a notion of continuity on multiple variables.

> [!Abstract] Theorem: Partial Derivatives and Continuity
> Let $f : \mathbb{R}^n \to \mathbb{R}$, and assume $f$ is continuously differentiable. Then, $f$ is continuous.
> > Recall that if $f$ is $C^1$, then all partials exist and are continuous.
>
> > [!Note]- Proof
> > 
> > We look at $f(x + h) - f(x)$, and claim that as $h \to 0$, $f(x + h) \to f(x)$.
> > 
> > By MVT, for some $0 < \theta < 1$,
> > $$
> > | f(x + h) - f(x) | = | \langle \nabla f(x + \theta h), h \rangle |
> > $$
> > By Cauchy Schwarz, we can bound this by
> > $$
> > \le || \nabla f(x + \theta h) || \cdot || h ||
> > $$
> > But as $h$ is convergent, and the functions are continuous, we can find a bound for the first term!
> > $$
> > || \nabla f(x + \theta h) || \le \max || \nabla f(y) || \cdot || x - y || \le C
> > $$
> > So, this drops to 0.
> 
> By this proof, in fact, if all the partials exist $\forall x \in O$ and are bounded, then $f$ is still continuous!

---

We end with a small remark that will segway into the next section. Let $f : \mathbb{R}^n \to \mathbb{R}, C^1$. Then,
$$
\lim_{h \to 0} \frac{f(x + h) - f(x) - \langle \nabla f(x), h \rangle}{||h||} = 0
$$
>  This can be proven by using Cauchy-Schwarz.

We use this to define differentiable functions! $f : \mathbb{R}^n \to \mathbb{R}$ is **differentiable** at $x$ if $\exists Q \in \mathbb{R}^n$ such that
$$
\left\{ \frac{f(x + h) - f(x) - \langle Q, h \rangle}{||h||} \right\} \to 0
$$
as $h \to 0$.

This is a stronger notion than partial diffentiation! So,
- $f \in C^1$ implies that $f$ is differentiable
- $f$ differentiable implies that all parties of $f$ exist

But, the converses are not true!



# Local Approximation of Real-Valued Functions
## First Order Approximations
> [!Tip] Motivation
> Say we have some function, and we want to analyze the behavior of it in an area around the point $x$. One way to do this is to choose another function $g$ that approximates $f$, yet is simpler! We can then work with $g$ to see what properties it has (and inherits from $f$). 
 
Let $O \subseteq \mathbb{R}^n$, and $x \in O$. For a positive integer $k$, we say that functions $f,g : O \to \mathbb{R}$ are **$k^{th}$ order approximations** of one another at $x$ if
$$
\lim_{h \to 0} \frac{f(x+h) - g(x+h)}{||h||^k} = 0
$$

We ask, can we find a first-order approximation for a given function $f$?

> [!Abstract] Theorem: First Order Approximation Theorem
> Let $O \subseteq \mathbb{R}^n$ open, $f : O \to \mathbb{R}$ be $C^1$. Then, for $x \in O$, we have first order approximation of $f$
> $$
> \lim_{h \to 0} \frac{f(x+h) - [f(x) + \langle \nabla f(x), h \rangle]}{||h||} = 0
> $$
> 
> > [!Note]- Proof
> > 
> > Recall previously that by MVT, we find $0 < \theta < 1$ such that
> > $$
> > f(x + h) - f(x) = \langle \nabla f(x + \theta h), h \rangle
> > $$
> > 
> > We can subtract both sides by $\langle \nabla f(x), h \rangle$ and apply Cauchy Schwarz to obtain 
> > $$
> > \begin{align*}
> > f(x + h) - f(x) - \langle \nabla f(x), h \rangle 
> > &= \langle \nabla f(x + \theta h), h \rangle - \langle \nabla f(x), h \rangle \\
> > f(x + h) - f(x) - \langle \nabla f(x), h \rangle 
> > &= \langle \nabla f(x + \theta h) - \nabla f(x), h \rangle \\
> > | f(x + h) - f(x) - \langle \nabla f(x), h \rangle | &\le || \nabla f(x + \theta h) - \nabla f(x) || \cdot || h || \\
> > \frac{| f(x + h) - f(x) - \langle \nabla f(x), h \rangle |}{||h||} 
> > &\le || \nabla f(x + \theta h) - \nabla f(x) ||
> > \end{align*}
> > $$
> > 
> > Because $f$ is continuously differentiable, we know that 
> > $$
> > \lim_{h \to 0} || \nabla f(x + \theta h) - \nabla f(x) || = 0
> > $$
> > 
> > So by the Comparison Lemma, we can force our original limit to be 0. 

We can alternatively write this in a few ways.
- Let $E(x,h)$ denote some error depending on $x$ and $h$. Then, our approximation can be given as
  $$
  f(x + h) = f(x) + \langle \nabla f(x), h \rangle + E(x,h) \qquad \lim_{h\to 0} \frac{E(x,h)}{||h||} = 0
  $$
  As the error drops to 0 when dividing by $||h||$, we can also say that the error is of **first order**, $O(||h||)$. 
- Letting $y = x+h$, $x$ fixed, we can also write our error as 
  $$
  f(y) = f(x) + \langle \nabla f(x), (y - x) \rangle + O( ||x - y|| )
  $$
  So if $x$ is fixed, and $y$ is sufficiently close to $x$, then we have a close approximation!

We can also interpret this formula geometrically. In fact, interestingly enough, our first order approximation is equivalent to a tangent plane approximation of our function!

> [!Note]- Proof
> Define $G$ to be the function $G = \{ (x_1, x_2, f(x_1, x_2)) \}$. This defines a surface in 3-dimensions. We will define the tangent plane at $(a,b)$.
> 
> At $(a, b)$, we find tangent directions by differentiating with respect to variables $x_1$ and $x_2$.
> $$
> T_1 = \left( 1, 0, \frac{\partial f}{\partial x_1} (a, b) \right) \qquad
> T_2 = \left( 0, 1, \frac{\partial f}{\partial x_2} (a, b) \right)
> $$
> 
> We take the cross product, to find a vector orthogonal to both. This will give us a vector that is a normal to our surface. 
> $$
> N = \left( -\frac{\partial f}{\partial x_1} (a, b), \frac{\partial f}{\partial x_2} (a, b), 1 \right)
> $$
> 
> We can use this to define the tangent plane at $(a, b, f(a, b))$ as
> $$
> \begin{align*}
> &(x_1 - a, x_2 - b, f(x_1, x_2) - f(a,b)) \cdot \left( -\frac{\partial f}{\partial x_1} (a, b), \frac{\partial f}{\partial x_2} (a, b), 1 \right) = 0 \\
> &f(x_1, x_2) - f(a, b) - \frac{\partial f}{d x_1} (a, b) (x_1 - a) - \frac{\partial f}{\partial x_2} (a, b) (x_2 - b) = 0 \\
> &f(x_1, x_2) - \left[ f(a, b) + \frac{\partial f}{d x_1} (a, b) (x_1 - a) + \frac{\partial f}{\partial x_2} (a, b) (x_2 - b) \right] = 0
> \end{align*}
> $$
> 
> Thus is the same as our first-order approximation formula! Simply redefine $(x_1, x_2)$ to be offsets $(a,b)$, $(x_1, x_2) + h$.

## Second Order Approximations and Second Derivatives
> [!Tip] Motivation
> In the single-variable case, we had the second-derivative test for determining minimums and maximums. Here, we develop the corresponding test for multiple variables.

### Definitions and Context
Let $A$ be an $n \times n$ matrix. Note that for any vector $\vec{x}$, the matrix-vector product
$$
Ax = y
$$
Is equivalent to the values inner products of the $i^{th}$ row of $A$ and $x$! If $A_i$ denotes the $i^{th}$ row of $A$, then
$$
Ax = ( \langle A_1, x \rangle, \dots, \langle A_i, x \rangle, \dots, \langle A_n, x \rangle )
$$
This fact will be useful later!

---

Let $A$ be an $n \times n$ matrix. Then, the function $Q : \mathbb{R}^n \to \mathbb{R}$ given by 
$$
Q(h) = \langle Ah, h \rangle
$$
Is known as the **quadratic function** associated with the matrix $A$.
> This function gives us a clean notation for generalizing directional derivatives into higher orders! 

Let $f$ be $C^2$. We define the **Hessian Matrix** of $f$, denoted $\nabla^2 f$, as the $n \times n$ matrix where for each pair of indices $i,j$,
$$
(\nabla^2 f(x))_{ij} = \frac{\partial f}{\partial x_j \partial x_i} (x)
$$
In other words,
$$
\nabla^2 f(x) = 
\begin{bmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \dots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\
\vdots & \ddots & \vdots \\
\frac{\partial^2 f}{\partial x_n \partial x_1} & \dots & \frac{\partial^2 f}{\partial x_n^2}
\end{bmatrix}
$$
> Note that if $f$ has continuous second-order partials, then the Hessian Matrix is symmetric because the $ij$ entry would equal the $ji$ entry!

We use the quadratic function notation to define higher order directional derivatives. If $f \in C^2 (\mathbb{R})$, $x,h$ fixed, then
1. $$
   \frac{d}{dt} f(x + th) = \langle \nabla f(x + th), h \rangle = \sum_{i=1}^n \frac{\partial f}{\partial x_i} (x + th) h_i
   $$
2. $$
   \frac{d^2}{dt^2} f(x + th) = \langle \nabla^2 f(x + th, h) \rangle = \sum_{i,j=1}^n \frac{\partial^2 f}{\partial x_i \partial x_j} (x + th) h_i h_j
   $$

Notice the pattern!

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

> [!Info] Remark
> If $f \in C^3$, then
> $$
> \frac{d^3}{dt^3} f(x + th) = \sum_{i,j,k=1}^n \frac{\partial^3 f}{\partial x_i \partial x_j \partial x_k} (x + th) h_i h_j h_k
> $$

In the above formulas, (2) will be quite useful in establishing a second-derivative criterion for the multi-variable case. However, we will also need some way to estimate the sizes of the values that quadratic functions can take on! These tools are given as follows.

---

Let $A$ be an $n \times n$ matrix, $A = (a_{ij})$. The **Hilbert-Schmidt norm** of $A$ is given as
$$
||A||_\text{HS} = \left( \sum_{i,j=1}^n a_{ij}^2 \right)^{1/2}
$$
> We think of the matrix as a long vector, and take the vector norm.

With this norm for a matrix, we can generalize the Cauchy-Schwarz Inequality!

> [!Abstract] Theorem: Generalized Cauchy Schwarz Inequality
> Let $A$ be $n \times n$, and $h \in \mathbb{R}^n$. Then,
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

We can also define the **operator norm** of $A$ as
$$
||A||_\text{op} = \max_{||h|| = 1} || Ah || 
$$
Based on this, and the Generalized Cauchy-Schwarz Inequality, we can find that for $||h|| = 1$,
$$
||Ah|| \le ||A||_{HS} \qquad ||A||_{op} \le ||A||_{HS}
$$

---

Let $A$ be a $n \times n$ matrix. $A$ is **positive definite** if 
$$
\langle Au, u \rangle > 0 \qquad u \ne 0
$$
Similarly, $A$ is **negative definite** if
$$
\langle Au, u \rangle < 0 \qquad u \ne 0
$$

> [!Abstract] Proposition: Properties of Positive Definite Matrices
> Let $A$ be a positive definite matrix. Then, there exists a $c > 0$ such that
> $$
> Q(u) = \langle Au , u \rangle \ge c ||u||^2
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

### Second Order Approximation and Second Derivative Test
Let $A \subseteq \mathbb{R}^n$, $f : A \to \mathbb{R}$. Also, let $x \in A$. Then, we have the following definitions:
- $x$ is a **local minimizer** if there exists a $\delta > 0$ such that
  $$
  f(x) \le f(x + h) \qquad (x + h) \in A, \forall 0 < ||h|| < \delta
  $$
- $x$ is a **local maximizer** if there exists a $\delta > 0$ such that
  $$
  f(x) \ge f(x + h) \qquad \forall 0 < ||h|| < \delta
  $$
- $x$ is a **local extreme point** if it is either a local minimizer or a local maximizer for $f$.

> Note that $x$ is a strict minimizer / maximizer if the inequality is strictly less than or greater than.

In the single-variable case, we found that for a local extremum to occur, the derivative must be 0. We define the analogous case for multiple variables.

> [!Abstract] Theorem: Necessity for Local Extremum
> Let $O \subseteq \mathbb{R}^n$ open, and let $f : O \to \mathbb{R}$ have first-order partial derivatives. If $x \in O$ is a local extreme point for $f$, then
> $$
> \nabla f(x) = 0
> $$

But unlike the single variable case, finding the $x$'s such that this holds is very difficult, as we get a system of equations! To help us with this, we need a more formal way to define the behaviors of functions! We define a test analogous to the single-variable Second-Derivative Test to help us with this.

By the Lagrange Remainder Theorem, recall that if $f : \mathbb{R} \to \mathbb{R}$, $f''(x)$ exists for every $x$, then for all $x,h \in \mathbb{R}$, there exists a $0 < \theta < 1$ such that
$$
f(x + h) = f(x) + f'(x) h + \frac{1}{2} f''(x + \theta h) h^2 
$$
We can generalize this to the multi-variable case!

> [!Abstract] Theorem: Multi-Variable Remainder Theorem
> Let $f : \mathbb{R}^n \to \mathbb{R}$, $C^2$. Then, for $x,h \in \mathbb{R}^n$, there exists $0 < \theta < 1$ such that 
> $$
> f(x + h) = f(x) + \langle \nabla f(x), h \rangle + \frac{1}{2} \langle \nabla^2 f(x + \theta h) h, h \rangle
> $$
>
> > [!Note]- Proof
> > 
> > Let $\phi(t) = f(x + th)$. Then,
> > $$
> > \phi(1) = \phi(0) + \phi' (0) + \frac{1}{2} \phi''(\theta)
> > $$
> > For some $0 < \theta < 1$.
> > 
> > Notice that this holds only because we assumed the second order derivatives are continuous. We find each term to be
> > $$
> > \begin{align*}
> > \phi'(0) = \frac{d}{dt}_{t=0} f(x + th) = \langle \nabla f(x), h \rangle \\
> > \phi''(t) = \frac{d^2}{dt^2} f(x + th) = \langle \nabla^2 f(x + th) h, h \rangle
> > \end{align*}
> > $$

This is in fact a second order approximation of $f$! 

> [!Abstract] Theorem: Second Order Approximation Theorem
> Let $f : \mathbb{R}^n \to \mathbb{R}$, $C^2$. Then,
> $$
> \lim_{h \to 0} \frac{f(x + h) - [f(x) + \langle \nabla f(x), h \rangle + \frac{1}{2} \langle \nabla^2 f(x) h, h \rangle ]}{||h||^2} = 0
> $$
> 
> > [!Note]- Proof
> >
> > $$
> > \begin{align*}
> > &\frac{f(x + h) - [f(x) + \langle \nabla f(x), h \rangle + \frac{1}{2} \langle \nabla^2 f(x) h, h \rangle ]}{||h||^2} \\
> > &= \frac{| \frac{1}{2} \langle (\nabla^2 f(x + \theta h) - \nabla^2 f(x)) h, h \rangle | }{||h||^2} \\
> > &\le \frac{\frac{1}{2}|| (\nabla^2 f(x + \theta h) - \nabla^2 f(x)) h || ||h||}{||h||^2} \\
> > &\le \frac{1}{2} || \nabla^2 f(x + \theta h) - \theta^2 f(x) || \to 0 
> > \end{align*}
> > $$

With the Second-Order Approximation Theorem, we can define a multi-variable analogy to the Second-Derivative test.

> [!Abstract] Theorem: Second Derivative Test
> Let $f : \mathbb{R}^n \to \mathbb{R}$, $C^2$. 
> 
> Let $x$ be a point such that $\nabla f(x) = 0$.
> - If the Hessian Matrix $\nabla^2 f(x)$ is positive definite, then $x$ is a **strict** local minimizer.
> - If the Hessian Matrix $\nabla^2 f(x)$ negative definite, then $x$ is a **strict** local maximizer.
>
> > [!Note]- Proof (TODO)
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

Is the converse of this theorem also true? In other words, let $f : \mathbb{R}^n \to \mathbb{R}, C^2$. Assume $x$ is a local minimizer. Then $\nabla f(x) = 0$. But what about $\nabla^2 f(x)$? Does it have to be positive definite? 

No! As a counterexample, let $f(x,y) = x^4 + y^4$. Then, we have a strict local minimizer at $0$, but the $\nabla^2 f(x)$ is not positive definite.

But then, what's a necessary condition for a minimizer? We discuss this below.

Let $A$ be a symmetric $n \times n$ matrix. 
- $A$ is **positive semi-definite** if $\langle Ah, h \rangle \ge 0$ for all $h \in \mathbb{R}^n$. 
- $A$ is **negative semi-definite** if $\langle Ah, h \rangle \ge 0$ for all $h \in \mathbb{R}^n$.

> Note that the inner product can now be 0, where it couldn't be before!

> [!Abstract] Theorem: Necessity Condition for Extremum
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

> [!Abstract] Proposition (IMPORTANT FOR EXAM)
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

## Higher Order Approximations
Let $x \in \mathbb{R}^n$, and let there be a multi-index $\alpha = (\alpha_1, \dots, \alpha_n)$ where $\alpha_i \in \{0,1\}$ (a vector of 1's and 0's).
> The multi-index will be used to "select" things we want later on!

With the multi-index, we define operations
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

# Linear Map Approximations of Non-Linear Mappings
> [!Tip] Motivation
> Before, we studied linear mappings, or in other words, functions that can be expressed as linear transformations. Now, we turn to examine mappings that may not necessarily be linear!

## Linear Mappings
We say a function $T : \mathbb{R}^n \to \mathbb{R}^m$ is **linear** if for all $\alpha, \beta \in \mathbb{R}$, $u,v \in \mathbb{R}^n$
$$
T(\alpha u + \beta v) = \alpha T(u) + \beta T(v) 
$$

> [!Abstract] Theorem: Linear Mappings as Matrices
> If $T : \mathbb{R}^n \to \mathbb{R}^m$ is linear, then there exists a unique $m \times n$ matrix $A$ such that
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

As given above, linear transformations can be given as their matrices, and in fact, many of their properties can be expressed in terms of matrices as well!

First, we consider compositions of transformations. Let us have linear transformations $T : \mathbb{R}^n \to \mathbb{R}^m$, $S: \mathbb{R}^m \to \mathbb{R}^k$. Let $A,B$ be matrices such that
$$
T(u) = Au \qquad S(u) = Bu
$$
Then, the matrix of the composition of these transformations is
$$
T(S(u)) = A(Bu) = (AB) u \qquad S(T(u)) = B(Au) = (BA) u
$$
Which is the product of the matrices!

Let's now consider inverses of transformations.

> [!Abstract] Theorem: Invertible Transformations
> $T: \mathbb{R}^n \to \mathbb{R}^n$ linear, is invertible (as a function) if and only if the corresponding matrix $A$ is invertible as a matrix if and only if $\det(A) \ne 0$.
> > We commonly determine that transformations are invertible by checking the matrices!

> [!Abstract] Theorem: Properties of Invertible Matrices
> Let $A$ be an $n \times n$ matrix. Then, $A$ is invertible if and only if $\exists c > 0$ such that 
> $$
> || Au || \ge c ||u|| \qquad u \in \mathbb{R}^n
> $$
> > By definition, $A$ is invertible if there exists a matrix $A^{-1}$ such $A A^{-1} = I$.
>
> > [!Note]- Proof 
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

> [!Note]- Proof
> We know that $(v_1 \dots v_n) = (w_1, \dots w_n) C$, then
> $$
> \begin{align*}
> (T(v_1), \dots T(v_n)) = (T(w_1), \dots T(w_n)) C \\
> (v_1, \dots v_n) A = (w_1, \dots w_n) CA 
> \end{align*}
> $$
> 
> So, $A = C^{-1} B C$.

## The Derivative Matrix and Differential
We consider the following classes of mappings. These are mappings that may be non-linear, and are approximatable by linear mappings.

Let $O \subseteq \mathbb{R}^n$, and consider mapping $F : O \to \mathbb{R}^m$ represented as component functions
$$
F = (F_1, \dots, F_m)
$$
We have the following definitions for $F$
1. $F$ is said to have **first-order partial derivatives at $x \in O$**, provided that for all $1 \le i \le m$, $F_i$ has first-order partial derivatives at $x$.
2. $F$ is said to have **first-order partial derivatives**, if it has first-order partial derivatives for all $x \in O$.
3. $F$ is said to be **continuously differentiable** provided that all of the $F_i$'s are continuously differentiable.

> [!Abstract] Theorem: Continuity on Mappings
> Let $O \subseteq \mathbb{R}^n$, and $F : O \to \mathbb{R}^m$. 
>
> Let $F$ be continuously differentiable. Then, $F$ is continuous.

Now, define $F: O \to \mathbb{R}^m$ with first-order partials at $x \in O$. We define the **derivative matrix** of $F$ at $x$, denoted $DF(x)$, as the matrix whose $ij$th entry is given by
$$
\begin{align*}
DF(x)_{ij} = \frac{\partial F_i}{\partial x_j} (x)
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
\end{align*}
$$
> We define the gradient of a function as a row vector.

We use this derivative matrix to generalize our findings in earlier sections.

> [!Abstract] Theorem: Mean Value Theorem for Mappings
> Let $F : \mathbb{R}^m \to \mathbb{R}^n, C^1$. Then, for $x, h \in \mathbb{R}^n$, we find $0 < \theta_1 < 1, \dots, 0 < \theta_m < 1$ such that
> $$
> F(x + h) - F(x) = 
> \begin{bmatrix}
> \nabla F_1(x + \theta_1 h) \\
> \vdots \\
> \nabla F_m (x + \theta_m h)
> \end{bmatrix} h
> $$
> > This is the multi-variable MVT applied to each component!
> 
> > [!Note]- Proof
> > 
> > Apply the MVT for each $F_i : \mathbb{R}^n \to \mathbb{R}, C^1$.

> [!Warning] Mean Value Theorem Misconception
> Note that above, if we chose all $\theta_i$'s to be equal, then we would have
> $$
> F(x+h) - F(x) = DF(x + \theta h) h
> $$
> Which seems like a very clean generalization of the MVT! However, it is not guaranteed that we can find a single $\theta$ that works for each $\theta_i$. 

> [!Abstract] Theorem: First-Order Approximation Theorem for Mappings
> Let $F : \mathbb{R}^n \to \mathbb{R}^m, C^1$. Then,
> $$
> \lim_{h \to 0} \frac{|| F(x+h) - [F(x) + DF(x) h] ||}{||h||} = 0
> $$
> 
> > [!Note]- Proof
> > 
> > The $i^{th}$ component of the above quantity, from the previous chapter, is
> > $$
> > \frac{F_i (x+h) - F_i (x) - \langle \nabla F_i (x), h \rangle}{||h||} \to 0
> > $$
 
It can be shown that at $x$, $DF(x)$ is the only matrix in which this limit holds.

> [!Abstract] Theorem
> Let $F : \mathbb{R}^n \to \mathbb{R}^m$. Fix $x$, and suppose there exists an $m \times n$ matrix $A$ such that
> $$
> \lim_{h \to 0} \frac{|| F(x+h) - [F(x) + Ah] ||}{||h||} = 0
> $$
> 
> Then, the mapping $F$ has first-order partial derivatives at $x$, and $A = DF(x)$.
> 
> > [!Note]- Proof
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

We also say $F : \mathbb{R}^n \to \mathbb{R}^m$  is **differentiable** at $x$ if there exists an $A$, $m \times n$ matrix such that
$$
\lim_{h \to 0} \frac{|| F_i (x + h) - [F_i (x) + Ah]||}{||h||} = 0
$$
So, $F \in C^1 (\mathbb{R}^n)$ implies that F is differentiable $\forall x \in \mathbb{R}^n$, which implies that $DF(x)$ exists $\forall x \in \mathbb{R}^n$. 
> These are strict implications! See the examples below.

> [!Example] Example: Counterexamples
> The below function is an example of $f : \mathbb{R}^2 \to \mathbb{R}$ for which $Df(x)$ exists $\forall x \in \mathbb{R}^2$, but there does not exist an $A$ such that
> $$
> \begin{align*}
> \frac{f(x+h) - f(x) - [a_1 h_1 + a_2 h_2]}{||h||} = 0 \\
> f(x_1, x_2) = \begin{cases}
> \frac{x_1 x_2}{x_1^2 + x_2^2} & (x_1, x_2) \ne (0,0) \\
> 0 & (x_1, x_2) = (0,0)
> \end{cases}
> \end{align*}
> $$

> [!Example]- Example
> Let $F : \mathbb{R}^n \to \mathbb{R}^m, C^1$. Assume $F(0) = 0, DF(0)$ satisfies $|| DF (0) h || \ge ||h||, \forall h \in \mathbb{R}^n$.
>
> Prove that $\exists \delta > 0$ such that $|| F(h) || \ge \frac{1}{2} ||h||, \forall ||h|| < \delta$.
>
> We know that
> $$
> \lim_{h \to 0} \frac{F(x+h) - F(0) - DF(0) h}{||h||} = 0
> $$
> 
> $$
> \begin{align*}
> || F(h) || = || F(h) - DF(0) h + DF(0) h || \ge || DF(h) || - || F(h) - DF(0) h || \\
> \frac{|| F(h) ||}{|| h ||} = \frac{|| F(h) - DF(0) h + DF(0) h ||}{|| h ||} \ge \frac{|| DF(h) ||}{|| h ||} - \frac{|| F(h) - DF(0) h ||}{|| h ||} \ge 1/2 \\
> \end{align*}
> $$
> 
> Since
> $$
> \lim_{h \to 0} \frac{F(x+h) - F(0) - DF(0) h}{||h||} = 0
> $$
> We know that $\exists \delta > 0$ such that 
> $$
> \frac{|| F(h) - DF(0) h ||}{|| h ||} \le \frac{1}{2}
> $$

## The Chain Rule
From the single-variable case, recall that for $g, f$, we can find the derivative of $(g \circ f)' (x)$ as
$$
(g \circ f)' (x) = \frac{d}{dx} g(f(x)) = g'(f(x)) f'(x)
$$

We can generalize this rule to higher dimensions!

> [!Abstract] Theorem: The Chain Rule
> Let $O \subseteq \mathbb{R}^n$, and let $F : O \to \mathbb{R}^m$ be continuously differentiable. Also let $U \subseteq \mathbb{R}^m$ to define $g : U \to \mathbb{R}$ continuously differentiable. 
> 
> Suppose that $F(O) \subseteq U$. Then, the composition $g \circ F$ is also continuously differentiable, and for $1 \le i \le n$, we can find its partial derivative as
> $$
> \frac{\partial}{\partial x_i} (g \circ F) (x) 
> = \nabla (g \circ F) (x) = \nabla g(F(x)) DF(x)
> $$

> [!Abstract] Theorem: The Chain Rule for General Mappings
> Let $O \subseteq \mathbb{R}^n$ open. Let $F : O \to \mathbb{R}^m$, and let $U \subseteq \mathbb{R}^m$ open to define $G : U \to \mathbb{R}^k$. Let $F,G$ be continuously differentiable.
> 
> Suppose that $F(O) \subseteq U$. Then, their composition $G \circ F$ is also continuously differentiable, and for each $x$, we can find
> $$
> D(G \circ F) (x) = DG (F(x)) \cdot DF(x)
> $$





TODO
---

# The Inverse Function Theorem

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

---

We give a second proof of the inverse function theorem based on the contraction mapping principle.

Let $F : \mathbb{R}^n \to \mathbb{R}^n, C^1$. Let $x^* \in \mathbb{R}^n$ where $DF(x^*)$ is invertible. We will show that $\exists \delta_0 > 0$ such that if $|| f(x^*) - y || < \frac{\delta_0}{2 || DF(x^*)^{-1} ||}$, then $\exists !x \in \bar{B}_{\delta_0} (x^*)$ such that $F(x) = y$.
> In other words, $F$ is locally one-to-one and onto in a local neighborhood of $x^*$!

We want to solve $F(x) = y$ if and only if $x = x - (DF(x^*))^{-1} (F(x) - y) = T(x)$. We will use the contraction mapping principle to show that there exists a fixed point of $T(x)$. 

Create a sequence 
$$
x_{k+1} = T(x_k) = x_k - (DF(x^*))^{-1} (F(x_k) - y)
$$

> [!Info] Remark
> Notice the similarity to Newton's method, which had root-finding formula (for $f : \mathbb{R} \to \mathbb{R}$)
> $$
> x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}
> $$

The main step is as follows: $\exists \delta_0 > 0$ such that
$$
|| x - z - DF(x^*)^{-1} (F(x) - F(z)) || < \frac{1}{2} || x - z || \qquad \forall x,z \in \bar{B}_{\delta_0} (x^*)
$$
The left hand side equals
$$
\begin{align*}
&|| (DF(x^*))^{-1} ( F(x) - F(z) - DF(x^*) (x - z) ) || \\
&\qquad \le || DF(x^*)^{-1} || ||
\left( \begin{bmatrix}
\nabla F_1 (P_1) \\ \vdots \\ \nabla F_n (P_n)
\end{bmatrix}
- DF(x^*) \right) (x - z) ||
\end{align*}
$$
Choose $\delta_0 > 0$ such that
$$
|| DF(x^*)^{-1} || ||
\left( \begin{bmatrix}
\nabla F_1 (P_1) \\ \vdots \\ \nabla F_n (P_n)
\end{bmatrix}
- DF(x^*) \right) < \frac{1}{2} \qquad \forall P_1, \dots P_n \in B_{\delta_0}(x^*)
$$
So, we found a $\delta_0$ such tha
$$
|| T(x) - T(z) || \le \frac{1}{2} || x - z ||
$$

Next, we will show that $T$ maps its domain onto itself.
$$
T : \bar{B}_{\delta_0} (x^*) \to \bar{B}_{\delta_0} (x^*)
$$
Let $|| x - x^* || \le \delta_0$. Look at $T(x) - x^*$. This is equal to
$$
\begin{align*}
&|| x - x^* - (DF)(x^*)^{-1} [ F(x) - F(x^*) + F(x^*) - y] || \\
&\qquad \le || x - x^* - DF(x^*)^{-1} [F(x) - F(x^*)] || + || DF(x^*)^{-1} [F(x^*) - y] || \\
&\qquad \le \frac{1}{2} || x - x^* || + \frac{1}{2} || x - x^* || \le \delta_0
\end{align*}
$$

So, $T$ is a contraction, and has a fixed point.


---

16.3, 11

Let $F : \mathbb{R}^n \to \mathbb{R}^n, C^1$, $\exists C$ such that
$$
|| F(x) - F(y) || \ge C || x - y ||
$$
1. Show that $DF(x)$ is invertible in $R^n$. We use the first order approximation theorem.
2. Show that $F(\mathbb{R}^n)$ is open. We use the inverse function theorem to show that $F$ is onto some neighborhood of the point.
3. Show that $F(R^n)$ is closed. 

To show this, let $y_k$ be a sequence of points in $F(R^n)$, and assume $y_k \to y$. Show $y \in F(R^n)$. We know $\exists x_k$, $F(x_k) = y_k$.

If $x_k \to x$, then $F(x_k) \to F(x)$ by continuity. So, By the uniqueness of limits, $y_k = F(x)$. We show $x_k \to x$ by using the assumption and applying the Comparison Lemma on Cauchy sequences, to show that $x_k$ is Cauchy.


4. Show that $F(R^n) = R^n$. Because both open and closed, and its not the empty set, must be $R^n$.


--- Next: Implicit Function Theorem..

Let us have function $f : \mathbb{R}^2 \to \mathbb{R}, C^1$. We ask, when is the set
$$
\{ (x,y) : f(x,y) = 0 \} 
$$
A $C^1$ curve?

> [!Example]+ Counterexamples
> $$
> f(x,y) = x^2 + y^2 + 1 = 0
> $$
> This will yield an empty set, so we don't have a $C^1$ curve.
> 
> $$
> f(x,y) = x^2 + y^2 = 0
> $$
> This will yield 1 point, so we don't have a $C^1$ curve.

We say $C \subseteq \mathbb{R}^2$ is a $C^1$ curve if  $\forall (x_0, y_0) \in C$, there exists a $U$ neighborhood of $(x_0, y_0)$, and function $g : \mathbb{R} \to \mathbb{R}, C^1$ such that
$$
C \cap U = \{ \text{Graph y = g(x) or x = g(y)} \} \cap U
$$

We can find that $\forall C \in \mathbb{R}^2$, closed, there exists a function $f \in C^1 (\mathbb{R}^2)$ such that
$$
C = \{ (x,y) : f(x,y) = 0 \}
$$

And furthermore, if $f : \mathbb{R}^2 \to \mathbb{R}$ is $C^1$, and $nabla f(x,y) \ne 0$ $\forall (x,y)$ such that $f(x,y) = 0$,then $C = \{ (x,y) : f(x,y) = 0\}$.

> [!Abstract] Theorem: Dini's Theorem
> Let $O$ open in $\mathbb{R}^2$, $f : O \to \mathbb{R}, C^1$. Let $(x_0, y_0)$ be a point in $O$, and assume $f(x_0, y_0) = 0, \frac{\partial f}{\partial y} (x_0, y_0) \ne 0$.
>
> Then, $\exists r, R > 0$, and a function $g : (x_0 - r, x_0 + r) \to (y_0 - R, y_0 + R), C^1$ such that $f(x,g(x)) = 0, \forall | x - x_0 | < r$, and if 
> $$
> (x,y) \in (x_0 - r, x_0 + r) \times (y_0 - R, y_0 + R)
> $$
> 
> And $f(x,y) = 0$, then $y = g(x)$.
> > We're basically saying, in this box, the 0-set of $f$ takes on a $C^1$ function $g(x)$.
>
> > [!Note] Proof
> > 
> > We know
> > $$
> > f(x_0, y_0) = 0, \frac{\partial f}{\partial y} (x_0, y_0) \ne 0
> > $$
> > Without loss of generality, suppose $\frac{\partial f}{\partial y} (x_0, y_0) > 0$. Then, $\exists R > 0,c > 0$ such that
> > $$
> > \frac{\partial f}{\partial y} \ge c > 0
> > $$
> > in the box $[x_0 - R, x_0 + R] \times [y_0 - R, y_0 + R]$. So, because $f(x_0, y_0) = 0$, we know that along the vertical line $(x_0, y \pm k)$, $f$ is strictly increasing, so 
> > $$
> > f(x_0, y - R) < 0 \qquad f(x_0, y + R) > 0
> > $$
> > 
> > We can find an interval around this vertical line where it is always negative around $f(x, y - R)$ and positive around $f(x, y + R)$. In other words, $\exists r > 0$ such that $f(x, y_0 - R) < 0$ if $|x - x_0| < r$, and $f(x, y_0 + r) > 0$ if $|x - x_0| < r$.
> > 
> > By IVT, for we can find a $y$ such that for all fixed $x$ in our interval $|x - x_0| < r$, we find a $y$ in the vertical line such that $f(x,y) = 0$. Define $g(x) = y$, the unique $y$ such that $f(x,y) = 0$, $y - y_0 < R$.
> > > Basically, we find a 0 by IVT for every vertical line in this interval!
> > 
> > We have constructed a $g : (x_0 - r, x_0 + r) \to (y_0 - r, y_0 + r)$ such that
> > $$
> > f(x, g(x)) = 0 \qquad \forall x
> > $$
> > And if $f(x,y) = 0$ in our box, then $y = g(x)$.
> > 
> > We have our function $g$. We must now show that $g$ is $C^1$, a we cannot guarantee our $y$'s on every sliver on the interval will form a continuous function or not. 
> > 
> > To do this, we first show that $g$ is continuous. Let $x, x+h \in (x_0 - r, x_0 + r)$. We look at $f(x + h, g(x + h)) - f(x, g(x))$ as the difference between two points $f(B) - f(A)$, and apply MVT. So, $\exists P$ on the line from $A$ to $B$ such that
> > $$
> > \begin{align*}
> > 0 = f(x + h, g(x + h)) - f(x, g(x)) 
> > &= \langle \nabla f(P), (h, g(x+h) - g(x)) \rangle \\
> > &= \frac{\partial f}{\partial x} (P) \cdot h + \frac{\partial f}{\partial y} (P) (g(x+h) - g(x))
> > \end{align*}
> > $$
> > 
> > So, we get
> > $$
> > g(x+h) - g(x) = - \frac{\frac{\partial f}{\partial x}(P)}{\frac{\partial f}{\partial y} (P)} h
> > $$
> > We can find an upper bound for the numerator as we have a continuous function on a compact set! As we assumed that the numerator is positive, we can find a bound for the fraction, so $\exists M$ such that
> > $$
> > | g(x + h) - g(x) | \le \frac{|\frac{\partial f}{\partial x}(P)|}{|\frac{\partial f}{\partial y} (P)|} |h| \le M |h|
> > $$
> > Thus, $g$ is continuous, as $h \to 0$, $P \to (x, g(x))$ and thus
> > $$
> > \lim_{h \to 0} \frac{g(x + h) - g(x)}{h} =  - \frac{\frac{\partial f}{\partial x}(x,g(x))}{\frac{\partial f}{\partial y} (x,g(x))}
> > $$
> > > This also gives us a formula for $g$!

If we know $g$ is $C^1$, differentiate 
$$
\frac{d}{dx} [f(x,g(x))] = 0
$$
To get
$$
\frac{\partial f}{\partial x} (x, g(x)) + \frac{\partial f}{\partial y} (x, g(x)) \cdot g'(x) = 0
$$
And we can solve for $g'(x)$ with this!

> [!Info] Remark
> We can generalize this!
> 
> Let $f : \mathbb{R}^{n+1} \to \mathbb{R}, C^1$, 
> $$
> f(x_0, y_0) = 0 \qquad x_0 \in \mathbb{R}^n, y_0 \in \mathbb{R}
> $$
> 
> And assume the gradient at this point is not 0. Then, by the same proof, we can find $R, r > 0$ such that $g: B_r (x_0) \to (y_0 - R, y_0 + R), C^1$ such that $f(x, g(x)) = 0$!

> [!Abstract] Theorem: The Implicit Function Theorem
> We look at points $(x,y) \in \mathbb{R}^{n+k}$, where $x \in \mathbb{R}^n$, $y \in \mathbb{R}^k$. Let $O$ be open in $\mathbb{R}^{n+k}$, $F : O \to \mathbb{R}^k, C^1$. 
>
> Let $(x_0, y_0) \in O$ such that $F(x_0, y_0) = 0$, $D_y F (x_0, y_0)$ invertible. Then, $\exists R, r > 0$, and a function
> $$
> G : B_r (x_0) \to B_R (x_0), C^1
> $$
> Such that
> $$
> F(x, G(x)) = 0 \qquad \forall x \in B_r (x_0)
> $$
> And if $x \in B_r (x_0), y \in B_R (y_0)$, and $F(x,y) = 0$, then $y = G(x)$. Also, $DG(x)$ can be computed by the chain rule.
>
> > [!Note] Proof
> > 
> > Let $H : O \to \mathbb{R}^{n+k}$,
> > $$
> > H(x,y) = (x, F(x,y))
> > $$
> > 
> > Clearly, $H(x_0, y_0) = (x_0, 0)$, and 
> > $$
> > DH(x_0, y_0) = 
> > \begin{bmatrix}
> > I_n & 0 \\
> > D_x (x_0, y_0) & D_y (x_0, y_0)
> > \end{bmatrix}
> > $$
> > Because $D_y F(x_0, y_0)$ is invertible, this matrix has a non-zero determinant, so the inverse function theorem applies!
> > 
> > So, $\exists R > 0$ and a neighborhood $V$ of $(x_0, 0)$ such that $H : \mathbb{R}(x_0) \times B_R (y_0) \to V$ is is 1-1, onto with a $C^1$ inverse $H^{-1} = V \to \mathbb{R}^{n+k}$. We define this inverse as
> > $$
> > H^{-1} (x,y) = (M(x,y), N(x,y))
> > $$
> > We the fact that $H(M(x,y), N(x,y)) = (x,y)$. By plugging $M,N$ into $H$, we get
> > $$
> > (M(x,y), F(M(x,y), N(x,y))) = (x,y)
> > $$
> > So, $M(x,y) = x$
> > $$
> > (x, F(x,N(x,y))) = (x,y)
> > $$
> > Define $G(x) = N(x,0)$. Pick $0 < r < R$ such that $B_r (x_0) \times \{0,\} \subseteq V$. Because $G(x) = N(x,0)$ which is $C^1$, $G(x)$ is too $C^1$. Subbing this in, we get
> > $$
> > F(x, N(x,0)) = 0
> > $$
> > Now, if $x \in B_r (x_0), y \in B_R (y_0)$, and $F(x,y) = 0$, we write that $H^{-1} ( H(x,y) ) = 0$
> > $$
> > \Longrightarrow ( M(x, F(x,y)), N(x, F(x,y)) ) = (x,y)
> > $$
> > If $F(x,y) = 0$, then $y = N(x, 0) = G(x)$.

Finally, we will show a formula for $DG(x)$, $x \in B_r (x_0)$. We use the property that $F(x, G(x)) = 0$. We know that starting with $x$, we map
$$
x \to (x, G(x)) \to F(x, G(x)) = 0
$$
So, by chain rule,
$$
\begin{align*}
D_{x,y} F (x, G(x)) \cdot D (x, G(x)) = 0 \\
( D_x F (x, G(x)) \quad D_y (x, G(x)) ) 
\begin{bmatrix}
I & DG(x)
\end{bmatrix} = 0 \\
(D_x F) (x, G(x)) + D_y (x, G(x)) DG(x) = 0
\end{align*}
$$
We can use this to solve for $DG(x)$!
$$
DG(x) = -\left[ D_y (x, G(x)) \right]^{-1} D_x F (x, G(x))
$$

> [!Example] Example
> Describe solutions to
> $$
> \begin{align*}
> (x^2 + y^2 + z^2)^3 - x + z = 0 \\
> \cos(x^2 + y^2) + e^z - 2 = 0
> \end{align*}
> $$
> 
> On the LHS, we have $F(x,y,z), F : \mathbb{R}^{1 + 2} \to \mathbb{R}^2, F(0,0) = 0$.
> 
> We expect this to be a curve through $(0,0,0)$. We will try to describe this curve locally. We find
> $$
> DF(0) = 
> \begin{bmatrix}
> \partial F_1 / \partial x & \partial F_1 / \partial y & \partial F_1 / \partial z \\
> \partial F_2 / \partial x & \partial F_2 / \partial y & \partial F_2 / \partial z \\
> \end{bmatrix} = 
> \begin{bmatrix}
> -1 & 0 & 1 \\
> 0 & 0 & 1
> \end{bmatrix}
> $$
> Define $F(X,Y), X \in \mathbb{R}, Y \in \mathbb{R}^2$. We need $D_y F (0)$ invertible, so we choose $X = (y), Y = (x,z)$ (as column $x$ and $z$ in $DF(0)$ will give us an invertible matrix).
> 
> We get $F(X, G(X)) = 0$, or in other words, $F(y, G(y)) = 0, G(y) \in \mathbb{R}^2$, so our solutions look like $(g_1 (y), y, g_2 (y))$.

--- 17.3

Let $f : \mathbb{R}^3 \to \mathbb{R}, C^1$. Look at the level set of this function, the set of points where the function is 0.
$$
S = \{ (x,y,z) : f(x,y,z) = 0 \}
$$

Assume $\nabla f(x,y,z) \ne 0$ for all $x,y,z \in S$. Then $S$ is a $C^1$ surface
> Recall, that for $S \subseteq \mathbb{R}^3$ to be a $C^1$ surface, $\forall x \in S$, there exists a $W$ neighborhood of $x$ such that $S \cap W$ is a $C^1$ function.

> [!Note] Proof
> Let $(x_0, y_0, z_0) \in S$. Without loss of generality, assume that $\frac{\partial f}{\partial z} (x_0, y_0, z_0) \ne 0$.
> 
> By the implicit function theorem, there exists a $r, R > 0$ and a function $g : B_r (x_0, y_0) \to B_R (z_0)$ such that
> $$
> f(x,y, g(x,y)) = 0 \qquad \forall (x,y) \in B_r (x_0, y_0)
> $$
> And furthermore, these are the only solutions to $f(x,y,z) = 0$ in $B_r (x_0, y_0) \times (z_0 - R, z_0 + R)$. 
> 
> So we have a transformation $(x,y) \to (x,y, g(x,y))$ paramterizing $S$ near $(x_0, y_0, z_0)$. To figure out the tangent vectors at $(x_0, y_0, z_0)$, look at the change in one variable along a particular direction.
> 1. Fixing $y$, we differentiate in the $x$ direction to get tangent
>    $$
>    T_1 : (1, 0, \frac{\partial g}{\partial x} (x_0, y_0))
>    $$
> 2. Fixing $x$, we differentiate in the $y$ direction to get tangent
>    $$
>    T_2 : (0, 1, \frac{\partial g}{\partial y} (x_0, y_0))
>    $$
> 
> We claim that $\nabla f(x_0, y_0, z_0) \perp T_1, T_2$. Look at $f(x, y, g(x,y)) = 0$ for all $(x,y)$. By the chain rule,
> $$
> \begin{align*}
> 0 
> &= \frac{\partial}{\partial x} \bigg\vert_{x = x_0} f(x,y_0, g(x, y_0)) \\
> &= \frac{\partial f}{\partial x} (x_0, y_0, z_0) + \frac{\partial f}{\partial z} (x_0, y_0, z_0) \cdot \frac{\partial g}{\partial x} (x_0, y_0) = 0 \\
> &= \langle \nabla f(x_0, y_0, z_0), (1, 0, \frac{\partial g}{\partial x} (x_0, y_0) \rangle
> \end{align*}
> $$
> 
> So, $\nabla f(x_0, y_0, z_0) \perp T_1$. By a similar argument, it is also orthogonal to $T_2$. 
> 
> We can find another vector orthogonal to $T_1, T_2$ by taking the cross product! Take $T_1 \times T_2 \ne 0$. Then, $\exists \lambda \ne0$ such that
> $$
> \nabla f(x_0, y_0, z_0) = \lambda (T_1 \times T_2)
> $$

## Curves in $\mathbb{R}^3$ defined by the intersection of two surfaces
Let $g,h : \mathbb{R}^3 \to \mathbb{R}, C^1$. Define the intersection of the two function's level sets, 
$$
C = \{ (x,y,z) : g(x,y,z) = h(x,y,z) = 0 \}
$$
> Intuitively, we're intersecting 2 2-dimensional surfaces. So we should expect a 1-dimensional curve!

A sufficient condition for $C$ to be a 1-dimensional curve in $\mathbb{R}^3$ is 
$$
\nabla g (x_0, y_0, z_0) \times \nabla h (x_0, y_0, z_0) \ne 0
$$
Equivalently, let $G : \mathbb{R}^3 \to \mathbb{R}^2, G(x,y,z) = ( g(x,y,z), h(x,y,z) )$. The, we require 
$$
DG(x_0, y_0, z_0) = 
\begin{bmatrix}
\dots & \nabla g & \dots \\
\dots & \nabla h & \dots
\end{bmatrix}
$$
Has rank 2 for all $(x_0, y_0, z_0) \in C$.

If so, without loss of generality, the derivative matrix with repect to $y,z$, $D_{y,z} G (x_0, y_0, z_0)$ is invertible. By the implicit function theorem, $\exists r, R$, and 
$$
\gamma : (x_0 - r, x_0 + r) \to B_R (y_0, z_0)
$$
Such that $G(x, \gamma(x)) = 0$ for all $|x - x_0| < R$, and these are the only solutions in $B_r(x_0) \times B_R (y_0, z_0)$.

Thus, $C$ agrees with the graph $\{ (x, \gamma(x)) : |x - x_0| < r \}$ in $(x_0 - r, x_0 + r) \times B_R (x_0, y_0)$, and we can parameterize it as 
$$
x \to (x, \gamma(x))
$$
With tangent vector at $(x_0, y_0, z_0)$ given as $T = (1, \gamma' (x_0))$, and 
$$
\nabla g (x_0, y_0, z_0) \perp T \qquad \nabla h (x_0, y_0, z_0) \perp T
$$
> These are two normals to our curve!

So, $\nabla g (x_0, y_0, z_0) \times \nabla h (x_0, y_0, z_0)$ is a non-zero tangent vector to the curve, so $\exists \lambda \ne 0$ such that
$$
\nabla g \times \nabla h = \lambda T
$$

---

We generalize.

An $n$-dimentional manifold embedded in $\mathbb{R}^N$, $N = n + k$. Let $F : \mathbb{R}^{n+k} \to \mathbb{R}^k, C^1$, and assume that $k \times (n + k)$ matrix $DF(x_0)$ has maximimal rank $k$ if $F(x_0) = 0$. 

If so, we will represent the level set 
$$
M = \{ X : F(X) = 0 \}
$$
Locally, as a graph.

Let $X_0 = (x_0, y_0) \in M$, $x_0 \in \mathbb{R}^n, y_0 \in \mathbb{R}^k$. Without loss of generality, $D_y F (x_0, y_0)$ (the rightmost $k \times k$ entries) is invertible. Thus, $\exists r, R > 0$ and $G : B_r (x_0) \to B_R (y_0)$ such that
$$
F(x, G(x)) = 0
$$
And these are the only solutions if $x \in B_r (x_0), y \in B_R (y_0)$. Thus, $M \cap B_r (x_0) \times B_R (y_0)$ agrees with the graph $(x, G(x)) : x \in B_r (x_0)$.
> This is an $n$-dimentional manifold!

We need $n$ linearly independent tangent vectors at $(x_0, y_0)$. The process of doing this is the same-- fix $n - 1$ variable, and differentiate with respect to our last variable. These are our tangent vectors!
$$
\begin{align*}
(1, 0, \dots, \frac{\partial G}{\partial x_1} (x_0) \\
(0, 1, \dots, \frac{\partial G}{\partial x_2} (x_0) \\
\vdots \\
&(0, \dots, 1, \frac{\partial G}{\partial x_n} (x_0)
\end{align*}
$$
The range of $DF(x, G(x))$ at $x_0$ is the tangent space above, as
$$
\begin{align*}
D_x (F(x, G(x)) = 0 \\
(DF) (x_0, y_0) \cdot 
\begin{bmatrix}
I \\ DG(x_0) 
\end{bmatrix} = 0
\end{align*}
$$
So, the tangent space to $M$ at $(x_0, y_0)$ is the null space of $DF(x_0)$.

---

We have $f : \mathbb{R}^n \to \mathbb{R}^3, C^1$, and an open set $O \subseteq \mathbb{R}^2$. We want to know if $F(O)$ looks like a smooth surface.

Recall that we say that if
$$
\frac{\partial F}{\partial x} (x,y) \times \frac{\partial F}{\partial y} (x,y) \ne 0
$$
Then $F(O)$ is a smooth surface at $F(x,y)$.
> This is equivalent to saying the derivative matrix of $F$ has rank 2, as the first and second row are linearly independent!

> [!Abstract] Theorem
> In the general case, let $O \subseteq \mathbb{R}^k$,
> $$
> F : O \to \mathbb{R}^N, C^1
> $$
> Assume that $DF(x_0)$ has rank $k$ $(N \ge k)$. Denote $F = (F_1, F_2), F_1 \in \mathbb{R}^k, F_2 \in \mathbb{R}^N$. Without loss of generality, assume $DF_1 (x_0)$ is invertible.
> 
> Then, $\exists U$ neighborhood of $x_0$ and $\exists V$ neighborhood of $F_1(x_0)$ such that
> $$
> F(U) = \{ (y, G(y)) : y \in V \}
> $$
> For some $G : V \to \mathbb{R}^{N - k}, C^1$.
>
> > [!Note] Proof
> > 
> > We know that $DF_1 (x_0)$ is invertible. By the inverse function theorem, $\exists U$ neighborhood of $x_0$ and $V$ neighborhood of $F_1 (x_0)$ such that $F_1 : U \to V$ is one-to-one, onto, and has a $C^1$ inverse $F^{-1} : V \to U$.
> > 
> > We compose
> > $$
> > F(x) = (F_1 (x), F_2 (x)) = (F_1 (F_1^{-1} (y)), F_2 (F_1^{-1} (y))) = (y, G(y)), y \in V
> > $$

---

Problem 28

> [!Example] Example: Implicit Function Theorem
> Let $F : \mathbb{R}^3 \to \mathbb{R}^2, C^1$. Assume $F(0,0) = (0,0)$ and 
> $$
> DF(0,0) = 
> \begin{bmatrix}
> 0 & 0 & 1 \\
> 1 & 0 & 0
> \end{bmatrix}
> $$
> Which of the following is true? $\exists g,h \in C^1, g,h : (-r, r) \to \mathbb{R}$, $g(0) = h(0) = 0$, such that
> 1. $F(x,g(x),h(x)) = (0,0), \forall |x| < r$
> 2. $F(g(y),y,h(y)) = (0,0), \forall |y| < r$
> 3. $F(g(z), h(z), z) = (0,0), \forall |z| < r$
> 
> The second one! In the implicit function theorem, we need a $Y$ such that $D_Y (F)$ is invertible. So, choose them to be $x,z$, with free variable $X = y$. Then, we can apply our implicit function theorem to get result (2).
> 
> We ask, is it possible for $F(x,g(x),h(x)) = (0,0), \forall |x| < r$? No. If the above holds, then by the chain rule, we find
> $$
> \begin{align*}
> \frac{d}{dx} F(x,g(x),h(x))
> &= DF(x,g(x),h(x)) 
> \begin{bmatrix}
> 1 \\ g'(x) \\ h'(x)
> \end{bmatrix} = 0
> \end{align*} 
> $$
> And at $(0,0,0)$,
> $$
> DF(0,g(0),h(0)) 
> \begin{bmatrix}
> 1 \\ g'(0) \\ h'(0)
> \end{bmatrix} = 0
> $$
> But this gives us $1 = 0$, which is impossible!

> [!Example] Example
> Let $F : \mathbb{R}^2 \to \mathbb{R}^2, C^1$. Assume that $DF(x)$ is positive definite for every $x \in \mathbb{R}^2$.
> 
> Prove $F$ is 1-1.
> 
> Assume that $F(x) = F(x + h)$. We wish to show that if $h \ne 0$, then we obtain a contradiction. 
> 
> Let $\theta(t) = \langle F(x + th), h \rangle$. By the one-dimensional MVT, we find
> $$
> \theta(1) - \theta(0) = \theta' (\theta) = \langle DF(x + th) h, h \rangle > 0
> $$
> So, $\theta(1) - \theta(0) > 0$, which is a contradiction!
> $$
> \theta(1) - \theta(0) > 0 \Longrightarrow 0 > 0
> $$

> [!Example] 
Does there exist an $F : \mathbb{R}^n \to \mathbb{R}^n, C^1$ with $DF(x)$ invertible for all $x \in \mathbb{R}^n$, and $F(\mathbb{R}^n)$ compact?

No. $F(\mathbb{R}^n)$ is open, so it cannot be compact.

--- Lagrange Multipliers

# Lagrange Multipliers
## Case 1: Surfaces in $\mathbb{R}^3$
Let $X = (x,y,z) \in \mathbb{R}^3$, and let $g : \mathbb{R}^3 \to \mathbb{R}, C^1$. Furthermore, define surface
$$
S = \{ x \in \mathbb{R}^3 : g(X) = 0 \}
$$
Where $\nabla g(X) \ne 0$ if $g(X) = 0$ ($X \in S$).

Let $f : \mathbb{R}^3 \to \mathbb{R}, C^1$, and let $X_0$ be such that $f(X_0) \le f(X)$ (or $f(X_0) \ge f(X)$), $\forall X \in S$. Then, $\exists \lambda \in \mathbb{R}$ such that
$$
\nabla f(x_0) = \lambda \nabla g(x_0)
$$

> [!Note]- Proof
> Without loss of generality, we have that
> $$
> \frac{\partial g}{\partial z} (x_0, y_0, z_0) \ne 0
> $$
> 
> By the implicit function theorem, there exists a function $h : B_r (x_0, y_0) \to \mathbb{R}$ such that
> $$
> \{ x,y,h(x,y) \}
> $$
> Is equal to $S$ in the neighborhood of $X_0$. Then, look at the composition $\phi : B_r (x_0, y_0) \to \mathbb{R}$, $\phi (x,y) = f(x, y, h(x,y))$, which has an unconstrained (interior) minimum (or maximum) at $(x_0, y_0)$. Thus, $\nabla \phi(x_0, y_0) = 0$.
> 
> Let $H(x,y) = (x,y,H(x,y))$. By the Chain Rule, 
> $$
> \begin{align*}
> \nabla \phi (x_0, y_0)
> &= \nabla f (x_0, y_0, z_0) \cdot DH(x_0, y_0) \\
> &= \nabla f (x_0, y_0, z_0)
> \begin{bmatrix}
> 1 & 0 \\
> 0 & 1 \\
> \frac{\partial h}{\partial x} (x_0, y_0) & \frac{\partial h}{\partial y} (x_0, y_0)
> \end{bmatrix}
> \end{align*}
> $$
> Each column of the derivative matrix is a tangent vector! So, $\nabla f(x_0)$ is orthogonal to both columns.
> 
> We know that $\nabla g(x_0)$ is also normal to our surface at $X_0$. So,
> $$
> \nabla g(X_0) \in (\text{span} \{T_1, T_2\})^\perp
> $$
> But the orthogonal set to the span of the tangent vectors is 1-dimensional! So, $\nabla g(X_0)$ is a basis for $(\text{span} \{T_1, T_2\})^\perp$. As a basis, if $\nabla f(X_0)$ is in this space, then we can form $\nabla f(X_0)$ as a linear combination of $\nabla g(X_0)$.
> $$
> \nabla f(X_0) = \lambda \nabla g(X_0)
> $$

Note that this same argument works for the case of $g : \mathbb{R}^n \to \mathbb{R}, C^1$,
$$
M = \{ x : g(x) = 0 \}
$$
Assuming $\nabla g(x) \ne 0$ if $g(x) = 0$ (then $M$ is an $n - 1$ dimensional manifold in $\mathbb{R}^n$).

If $f : \mathbb{R}^n \to \mathbb{R}, C^1$ and $X_0$ is such that $f(x_0) \ge f(x)$ (or $f(x_0) \le f(x)$), then $\exists \lambda \in \mathbb{R}$ such that
$$
\nabla f(x_0) = \lambda \nabla g(x_0)
$$

## Case 2: Curves in $\mathbb{R}^3$
Let $g,h : \mathbb{R}^3 \to \mathbb{R}, C^1$. Define curve
$$
C = \{ X \in \mathbb{R}^3 : g(X) = h(X) = 0 \}
$$

And assume
$$
\text{Rank} 
\begin{bmatrix} \nabla g(X) \\ \nabla h(X) \end{bmatrix} = 2
$$
If $X \in C$ (then $C$ is a $C^1$ curve in $\mathbb{R}^3$).

Let $f : \mathbb{R}^3 \to \mathbb{R}, C^1$. Let $X_0 \in C$ such that $f(X_0) \le f(X)$ (or $f(X_0) \ge f(X)$) for all $x \in C$. Then there exists $\lambda_1, \lambda_2 \in \mathbb{R}$ such that
$$
\nabla f(X_0) = \lambda_1 \nabla g(X_0) + \lambda_2 \nabla h(X_0)
$$

> [!Note] Proof 
> Without loss of generality, say $D_{y,z} (g,h) (x_0, y_0,z_0)$ is invertible. By the implicit function theorem, $\exists \gamma : (x_0 - r, x_0 + r) \to \mathbb{R}^2, C^1$ such that $(x, \gamma(x))$ is equal to $C$ in a neighborhood $X_0$.
> 
> Let $\phi(x) = f(x, \gamma(x))$, $\gamma : (x_0 - r, x_0 + r) \to \mathbb{R}$, $\gamma$ has an unconstrainer min (or max) at $x_0$, $\gamma' (x_0) = 0$. 
> 
> By the Chain Rule,
> $$
> \nabla f(x_0, \gamma (x_0)) 
> \begin{bmatrix}
> 1 \\ \gamma' (x_0)
> \end{bmatrix} = 
> \nabla f(x_0, \gamma (x_0)) \cdot T = 0
> $$
> Is a basis for the tangent space to $C$ at $x_0$. 
> 
> Recall $\nabla g(x_0), \nabla h(x_0)$ are linearly independent vectors orthogonal to $T$. So, 
> $$
> \text{Span} (\nabla g(x_0), \nabla h(x_0)) = ( \text{Span} T )^\perp
> $$
> We also know $\nabla f(x_0)$ is in this space. Thus, there exists a linear combination of $\nabla g(x_0), \nabla h(x_0)$ that form $\nabla f(x_0)$.

---

Let $A$ be an $n \times n$ symmetric real matrix. Let 
$$
\lambda = \min_{||x|| = 1} \langle Ax, x \rangle
$$
> We look at the minimum of the quadratic function in the compact set given by the unit sphere.

Let $x_0$ be a minimizer ($||x_0|| = 1$). Then, $A x_0 = \lambda x_0$

> [!Note]- Proof
> $g(x) = ||x||^2$. We try to minimize the function $f(x) = \langle Ax, x \rangle$. By the above theorem, at a minimizer, $\exists \lambda$ such that $\nabla f(x_0) = \lambda \nabla g(x_0) = \lambda 2x$.
> 
> We show that $\nabla f(x_0) = 2 A x_0$. This completes our proof.
> 
> > [!Info]- Lemma
> > 
> > If $f(x) = \langle Ax, x \rangle$, then $\nabla f(x) = 2Ax$.
> > 
> > We find
> > $$
> > \begin{align*}
> > \lim_{t \to 0} \frac{f(x + te_i) - f(x)}{t} 
> > &= \lim_{t \to 0} \frac{\langle A (x + te_i), x + te_i \rangle - \langle Ax, x \rangle}{t} \\
> > &= \lim_{t \to 0} \frac{\langle Ax, x \rangle + t \langle A x, e_i \rangle + t \langle A e_i, x \rangle + t^2 \langle A e_i, e_i \rangle - \langle Ax, x \rangle}{t} \\
> > &= \langle A x, e_i \rangle + \langle A e_i, x \rangle \\
> > &= 2 \langle Ax, e_i \rangle
> > \end{align*}
> > $$
> > This is the ith component of $2Ax$!
> > > The last equality is because $\langle A e_i, x \rangle = \langle e_i, A x \rangle$!

END OF CONTENT! :D 

---

Let $p > 1, q > 1$. Prove that
$$
\frac{x^p}{p} + \frac{y^q}{q} \ge \frac{1}{p} + \frac{1}{q}
$$
If $g(x,y) = xy = 1, x > 0, y > 0$.

At $Q$ minimizer, we have that
$$
\nabla f = \lambda \nabla g, xy = 1
$$

We find the minimizer at $(1,1)$ proving this inequality.

Prove 
$$
ab \le \frac{a^p}{p} + \frac{b^q}{q}
$$ 
If $a,b > 0$, $p,q > 1$, and $\frac{1}{p} + \frac{1}{q} = 1$.

With the earlier part, if $ab = 1$ Then we are done.

In general, 
$$
1 = \frac{ab}{a^{1/p + 1/q} b^{1/p + 1/q}} = \frac{a}{(ab)^{1/p}} \frac{b}{(ab)^{1/q}}
$$
Using part a again,
$$
\frac{(a / (ab)^{1/p})^p}{p} + \frac{(b / (ab)^{1/q})^q}{q} \ge \frac{1}{p} + \frac{1}{q} = 1
$$

---

A better proof for this is as follows. If $f : I \to \mathbb{R}$ is convex if
$$
f( (1 - \theta) x + \theta y) \le (1 - \theta) f(x) + \theta f(y)
$$
For all $0 < \theta < 1$, $x,y \in \mathbb{R}$.
> This is what we know as concave up!

> [!Abstract]
> If $f : I \to \mathbb{R}$ is differentiable, and $f'(x)$ is increasing on $I$, then $f$ is convex.

With this theorem, we can prove the above problem as follows. Let $a = e^A, b = e^B$. Use $f(x) = e^x$, convex. Then,
$$
ab = e^{A + B} = e^{pA / p + qB / q} \le \frac{1}{p} e^{pA} + \frac{1}{q} e^{qB} = \frac{1}{p} a^p + \frac{1}{q} b^q
$$

> [!Info] Motivation
Recall if $x_i, y_i > 0$,
$$
\sum_{i=1}^n x_i y_i \le (\sum x_i^2)^{1/2} (\sum y_i^2)^{1/2}
$$

> [!Abstract] Holder's Inequality
Let $p,q > 1$, $\frac{1}{p} + \frac{1}{q} = 1$. Then, the sum
$$
\sum_{i=1}^n x_i y_i \le (\sum_{i=1}^n x_i^p)^{1/p} (\sum_{i=1}^n y_i^q)^{1/q}
$$

> [!Note] Proof
> 
If $(x_1, \dots x_n)$ or $(y_1, \dots y_n)$ are the zero vector, we are done.

Assume that both vectors are non-zero. So,
$$
(\sum_{i=1}^n (x_i^p))^{1/p} > 0 \qquad (\sum_{i=1}^n (y_i^q))^{1/q} > 0
$$
Both the LHS and RHS are homogeneous of degree 1 in $x$ and $y$. 

> [!Abstract] Theorem
> Let $f,g : [a,b] \to \mathbb{R}$ continuous. Then,
> $$
> \int_a^b |fg| \le \left( \int_a^b |f|^p \right)^{1/p} \left( \int_a^b |g|^q \right)^{1/q}
> $$
> 
> > [!Note] Proof
> > 
> > If this is true for some $f$, then it is true for $tf$ (for $t > 0$). Without loss of generality, say
> > $$
> > (\int_a^b |f|^p)^{1/p} = 1, (\int_a^b |g|^q)^{1/q} = 1
> > $$
> > For each fixed $x$, we find
> > $$
> > \begin{align*}
> > \int_a^b |fg| 
> > &\le \int_a^b (\frac{1}{p} |f|^p + \frac{1}{q} |g|^q) dx \\
> > &\le \frac{1}{p} \int_a^b |f|^p + \frac{1}{q} \int_a^b |g|^q \\
> > &\le \frac{1}{p} + \frac{1}{q} = 1 = \left( \int_a^b |f|^p \right)^{1/p} \left( \int_a^b |g|^q \right)^{1/q}
> > \end{align*}
> > $$

Back to our original proof. It suffices to show that for $x_1 < x < x_2$, then $f(x) \le l(x)$, $l$ being our line.
> We show that our function's slope is less than the lines slope!
