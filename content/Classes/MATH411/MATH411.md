---
title: MATH411
tags:
- math411
---

MATH411 is a continuation of MATH410, but into $n$ dimensions ($\mathbb{R}^n$). 

$R^n$ is a vector space, with vectors and scalars (respectively) given as
$$
u = (u_1, u_2, \dots u_n) \in \mathbb{R}^n, u_i \in \mathbb{R}
$$
Satisfying vector addition and scalar multiplication.

with an inner product commonly known as the **dot product**
$$
<u, v> = u_1 v_1 + \dots + u_n v_n
$$
Satisfying the following axioms of a (real) inner product space:
- $<u,v> = <v,u>$
- $<\alpha u + \beta v, w> = \alpha <u, w> + \beta <v, w>$
- $<u, u> \ge 0$, and $<u, u> = 0$ if and only if $u = 0$.
- $|| u ||^2 = <u, u>$

> [!Abstract] Theorem: Inner Product in $\mathbb{R}^2$
> In $\mathbb{R}^2$, $<u, v> = || u || \cdot || v || \cos \theta$ where $\theta$ is the angle between the two vectors.
>
> > [!Note]- Proof
> > 
> > Using polar coordinates, we can convert our vectors into the polar space 
> > $$
> > u = ||u|| ( \cos \alpha, \sin \alpha ) \qquad
> > v = ||v|| ( \cos \beta, \sin \beta )
> > $$
> > Where $\alpha$ is the angle of $u$ to the $x$-axis, and $\beta$ is the angle of $v$ to the same axis.
> > 
> > We can find that
> > $$
> > <u,v> = ||u|| ||v|| (\cos \alpha \cos \beta + \sin \alpha \sin \beta) = ||u|| ||v|| \cos(\beta - \alpha)
> > $$

We say that $u$ is **orthogonal** to $v$, $u \perp v$, if $<u, v> = 0$.

> [!Abstract] Theorem: Properties of Orthogonality
> $$
> || u + v ||^2 = || u ||^2 + || v ||^2
> $$
> If and only if $\langle u, v \rangle = 0$.
> 
> > [!Note]- Proof
> >
> > $$
> > \begin{align*}
> > || u + v ||^2 &= \langle u + v, u + v \rangle = \langle u, u \rangle + \langle u, v \rangle + \langle v, u \rangle + \langle v,v \rangle \\
> > &= || u ||^2 + 2 \langle u, v \rangle + ||v||^2
> > \end{align*}
> > $$
> > Which is equal to $||u||^2 + ||v||^2$ if and only if $\langle u, v \rangle = 0$.

> [!Abstract] Cauchy-Schwarz Inequality
> Let $u, v \in \mathbb{R}^n$. Then, 
> $$
> | \langle u, v \rangle | \le || u || \cdot || v ||
> $$
>
> > We prove this using the axioms of inner products only (see above), making generalizable for any inner product!
> 
> > [!Note]- Proof
> > 
> > First, note that if either $u$ or $v$'s normals are 0, then this is trivially true.
> > 
> > Assume that both $||u|| \ne 0$ and $||v|| \ne 0$. Now, take the expression $|| u - \alpha v ||^2$, and note that this is (by an axiom) $\ge 0$.
> > 
> > By a previous proof,
> > $$
> > || u - \alpha v ||^2 = ||u||^2 - 2 \alpha \langle u, v \rangle + \alpha^2 ||v||^2 = ||u||^2 + \alpha(-2 \langle u, v \rangle + \alpha ||v||^2)
> > $$
> > We seek to minimize this with respect to $\alpha$. Ignoring the constants, we minimize
> > $$
> > 2 \langle u, v \rangle + \alpha ||v||^2 = 0 \to \alpha = \frac{\langle u, v \rangle}{||v||^2}
> > $$
> > 
> > Subbing this in, we have
> > $$
> > \begin{align*}
> > 0 &\le || u - \alpha v ||^2 = ||u||^2 - 2 \frac{\langle u, v \rangle}{||v||^2} \langle u, v \rangle + \left( \frac{\langle u, v \rangle}{||v||^2} \right)^2 ||v||^2 = ||u||^2 - \frac{\langle u, v \rangle^2}{||v||^2} \\
> > 0 &\le ||u||^2 - \frac{\langle u, v \rangle^2}{||v||^2} \\
> > \langle u, v \rangle^2 &\le ||u||^2 ||v||^2 \\
> > |\langle u, v \rangle| &\le ||u|| ||v|| \\
> > \end{align*}
> > $$

> [!Info] Corollary
> Note that equality holds if and only if $\exists \alpha \in \mathbb{R}$ such that $u = \alpha v$ (or $v = \alpha u$).
>
> > [!Note]- Proof ($\leftarrow$)
> > 
> > $$
> > u = \alpha v \to | \langle u, v \rangle | = |\alpha| ||v||^2 = ||\alpha v|| ||v|| = ||u|| ||v||
> > $$
> 
> > [!Note]- Proof ($\rightarrow$)
> > 
> > Let $||u|| ||v|| = | \langle u, v \rangle$. Then, if we repeat our original proof, we find that 
> > $$
> > ||u||^2 - \frac{\langle u, v \rangle^2}{||v||^2} = \frac{||u||^2 ||v||^2 - \langle u, v \rangle^2}{||v||^2} = 0
> > $$
> > Telling us that $||u - \alpha v|| = 0$ for our minimizer $\alpha = \frac{\langle u, v \rangle}{||v||^2}$. So, $u - \alpha v = 0$ by an axiom.

> [!Abstract] Theorem: Triangle Inequality
> $$
> || u + v || \le ||u|| + ||v|| \forall u, v \in \mathbb{R}^n
> $$
> 
> > [!Note]- Proof
> > 
> > We find that
> > $$
> > ||u + v||^2 = ||u||^2 + 2 \langle u, v \rangle + ||v||^2 =  ||u||^2 + 2 ||u||^2 ||v||^2 + ||v||^2
> > $$
> > Giving us our triangle inequality due to the Cauchy-Schwarz Inequality.

> [!Abstract] Theorem: Reverse Triangle Inequality
> $$
> || u \pm v || \le \left| ||u|| - ||v|| \right|
> $$
>
> > [!Note]- Proof ($-$)
> > 
> > $$
> > ||u|| = ||u - v + v|| \le ||u - v|| + ||v||
> > $$
> > We also know that
> > $$
> > ||u - v|| \ge ||u|| - ||v||
> > $$
> > Giving us
> > $$
> > ||v - u|| \le ||v|| - ||u||
> > $$

---

# Sequences and Limits in $\mathbb{R}^n$
Consider a sequence in $\mathbb{R}^n$ $\{u_k\}$, $k \in \mathbb{N}$. In other words, each entry in the sequence is a point in $\mathbb{R}^n$.
> Note that we will denote $u^i$ as the projection of the $i^{th}$ element of $u$ ($u$'s $i^{th}$ element).

If $\{u_k\}$ is a sequence in $\mathbb{R}^n$, $u \in \mathbb{R}^n$, then we define the **limit**
$$
\lim_{k\to\infty} u_k = u \quad \text{if} \quad \lim_{k\to\infty} || u_k - u || = 0
$$
We alternatively can write this as **$\{u_k\} \to u$ in the norm**. This is similar in idea to convergence in 1-dimensional series!

But in higher dimensions, this is not the only notion of convergence that we have! We can also say that $\{u_k\} \to u$ **componentwise**, if each $u_k^i \to u^i$ as $k \to \infty$.

> [!Abstract] Theorem: Notions of Convergence
> $\{u_k\} \to u$ in norm if and only if $\{u_k\} \to u$ componentwise.
>
> > [!Note]-  Proof
> > 
> > #### Proof $\rightarrow$
> > Assume that $\{u_k\} \to u$ in norm. Then, for each $1 \le i \le n$, 
> > $$
> > 0 \le | u_k^i - u^i | \le \sqrt{ (u_k^1 - u^1)^2 + \dots + (u_k^n - u^n)^2 } = || u_k - u || \to 0
> > $$
> > So by the squeeze theorem, $|u_k^i - u^i| \to 0$.
> > 
> > #### Proof $\leftarrow$
> > Assume that $\{u_k^i\} \to u^i$. Then,
> > $$
> > || u_k - u || = \sqrt{ (u_k^1 - u^1)^2 + \dots + (u_k^n - u^n)^2 }
> > $$
> > As each component converges to 0 by definition, and sums of sequences converging to 0 also converge to 0, we know that $|| u_k - u || \to 0$.

Note that this does not hold for infinite dimensions! In particular, component-wise convergence does not imply convergence in norm.

For example, say we have a sequence $\{u_k\}$, where for any $k$ the $k^{th}$ element is 1, all other 0. So,
$$
\begin{align*}
    u_1 &= (1, 0, 0 \dots) \\
    u_2 &= (0, 1, 0, \dots)
\end{align*}
$$
We can see that as $k \to \infty$, $\{u_k\} \to \vec{0}$, the 0 vector! However, $||u_k|| \to 1$, so it does not converge in norm to 0.

# Closed and Open Sets in $\mathbb{R}^n$
Let $r > 0$, $u \in \mathbb{R}^n$. We define the **open ball of radius $r$, centered at $u$** as
$$
B_r(u) = \{ v \in \mathbb{R}^n : || u - v || < \mathbb{R} \}
$$
In other words, the set of all $n$-dimensional points that are within some predetermined hypersphere of $u$.

We say that a set $A \subseteq \mathbb{R}^n$ is **open** if $\forall u \in A$, $\exists r > 0$ such that $B_r(u) \subseteq A$. In other words, for all vectors in $A$, we can find an open ball around the vector such that all vectors in the ball are in $A$.

> [!Abstract] Open Balls and Open Sets
> For $r > 0$, $u \in \mathbb{R}^n$, the open ball $B_r(u)$ is an open set.
> > Intuitively, this makes sense as for any vector inside the open ball, we can find a ball contained within our original ball. As our vectors get closer and closer to the ball's edge, our containing ball will shrink!
>
> > [!Note]- Proof
> > 
> > We want to show that $\forall v \in B_r(u)$, $\exists p > 0$ such that $B_p (v) \le B_r(u)$.
> > 
> > We know that for $v$, $|| u - v || \mathbb{R}$ by definition. We define the distance from $v$ to the ball's edge, $p = r - || u - v ||$. This will be the radius of our new ball around $v$.
> > 
> > We now show that $B_p(v) \subseteq B_r (u)$. Pick any $w \in B_p(v)$. By definition, 
> > $$
> > || v - w || < p \Longrightarrow || v - w || < r - || u - v ||
> > $$
> > Look at $|| u - w ||$. We know that
> > $$
> > \begin{align*}
> > || u - w || &= || u - v + v - w || \\
> > &\le || u - v || + || v - w || \\
> > &< || u - v || + p \\
> > &< || u - v || + (r - ||u - v||) \\
> > &< r
> > \end{align*}
> > $$
> > Thus, $w \in B_r (u)$!

We say that a set $A \subseteq \mathbb{R}^n$ is **closed** if for any sequence in $A$ $\{u_k\} \subseteq A$ such that $\{u_k\} \to u$, $u \in \mathbb{R}^n$, then $u \in A$. 

Furthermore, if $A \in \mathbb{R}^n$, then we call $A^c$ the **complement** of $A$, 
$$
A^c = \mathbb{R}^n \backslash A = \{ u \in \mathbb{R}^n | u \not\in A \}
$$

> [!Abstract] Theorem: Properties of Open Sets
> $A$ is an open set if and only if it's complement, $A^c$, is closed.
> > The statement that "$A$ is open if and only if it is not closed" is NOT TRUE. There exist sets that are neither open or closed, and there exist sets that are both open and closed (ex. the empty set and $\mathbb{R}^n$)!
