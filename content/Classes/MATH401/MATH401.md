---
title: MATH401
tags:
- math401
---

This course, Applications in Linear Algebra, describes various ways we can use linear algebra in the real world.

We begin by describing a brief but important theorem for this course.

> [!Abstract] Theorem: Uniqueness of Invertible Linear Systems 
> Suppose we have a linear system
> $$
> A \vec{x} = \vec{b}
> $$
> with $n$ variables and $n$ equations. Then, if $A$ is an invertible $n \times n$ matrix, then the linear system has 1 and only 1 solution, and we can find it by taking
> $$
> \vec{x} = A^{-1} \vec{b}
> $$

# Notes
Notes for this course are given below.

- [[Leontief Input-Output]]
- [[Applications of Graphics]]
- [[Least Squares]]
- [[Markov Chains]]
- [[Heat Diffusion]]
- Matrix Exponentials and Rotations
- ..
- ..

---

# Matrix Exponentials and Rotations
## Contextualization
Suppose we want to solve 
$$
\vec{x}'(t) = 
\begin{bmatrix}
0 & -1 \\ 1 & 0
\end{bmatrix} \vec{x}(t) \qquad \vec{x}(0) = (2,-5)^T
$$
Recall that from [[Heat Diffusion]], we can find a solution $\vec{x}(t) = e^{tA} (2,-5)^T$, and to compute this, we want to diagonalize $A$ to find
$$
e^{tA} = P e^{tD} P^{-1}
$$
But when we try to compute this, we find complex eigenvalues with eigenvectors!
$$
\begin{align*}
&\lambda_1 = i &\vec{v}_1 = (i, 1) \\
&\lambda_2 = -i &\vec{v}_2 = (-i, 1)
\end{align*}
$$
This will give us diagonalization 
$$
A = P D P^{-1} = 
\begin{bmatrix}
i & -i \\ 1 & 1
\end{bmatrix}
\begin{bmatrix}
i & 0 \\ 0 & -i
\end{bmatrix}
\frac{1}{2i}
\begin{bmatrix}
1 & i \\ -1 & i
\end{bmatrix} =
\begin{bmatrix}
i & -i \\ 1 & 1
\end{bmatrix}
\begin{bmatrix}
i & 0 \\ 0 & -i
\end{bmatrix}
\begin{bmatrix}
-(1/2) i & 1/2 \\ (1/2) i & 1/2
\end{bmatrix}
$$
And subsequent solution
$$
\begin{align*}
P e^{tD} P^{-1} 
&=
P \begin{bmatrix}
e^{ti} & 0 \\ 0 & e^{-ti}
\end{bmatrix} P^{-1} = 
\begin{bmatrix}
i & -i \\ 1 & 1
\end{bmatrix}
\begin{bmatrix}
\cos t + i \sin t & 0 \\ 0 & \cos t - i \sin t
\end{bmatrix}
\begin{bmatrix}
-(1/2) i & 1/2 \\ (1/2) i & 1/2
\end{bmatrix} \\
&= 
\begin{bmatrix}
\cos t & -\sin t \\
\sin t & \cos t
\end{bmatrix}
\end{align*}
$$
> By a theorem (Euler's Formula), it is true that for any real number $x$, $e^{ix} = \cos x + i \sin x$. So,

This gives us final solution $\vec{x}(t) = (2 \cos t + 5 \sin t, 2 \sin t - 5 \cos t)^T$!

We make some interesting notes from this:
- Even though we had to work with imaginary numbers, our final answer is a real answer! This should make sense. as $e^{tA}$ has to be a real matrix given that $A$ is real (a series of real matrices must also be real).
- Our matrix $e^{tA}$ gives us a CCW rotation by $t$ radians! 

We ask, why does this happen? What proeprties of $A$ cause this to happen?
> It's not because $A$ started as a rotation matrix! If we tried this with another rotation matrix, we may not get the same answer.

## Matrix Exponentials
We first continue our discussion of matrix exponentials.

---

Analogous to $e^0 = 1$, for the $0$ matix, 
$$
e^{0_{n \times n}} = I_n
$$

---

What about $e^a e^b = e^{a + b}$? Is it true for matrices that $e^A e^B = e^{A + B}$?

No! And in fact, it occurs because matrix multiplication is not commutative. While in $e^A e^B$, all terms are of the form $A^i B^j$ (all $A$ matrices first, then $B$ matrices after), powers like
$$
(A + B)^2 = A^2 + AB + BA + B^2
$$
flip the order of the matrix multiplication!

However, if we have matrices $A$, $B$ whose product are commutative, then this property holds!

> [!Abstract] Proposition
> If $AB = BA$, then
> $$
> e^{AB} = e^{A + B}
> $$
>
> > [!Info] Corollary
> > 
> > Let $A$ be any $n \times n$ matrix. 
> > 1. For any scalars $s, t$,
> >    $$
> >    e^{tA} e^{sA} = e^{(t + s) A}
> >    $$
> > 2. $$
> >    e^A e^{-A} = I
> >    $$
> >    So, $e^A$ has an inverse, given as $(e^A)^{-1} = e^{-A}$ for any square matrix $A$.

> [!Abstract] Theorem
> For an $n \times n$ matrix $A$,
> $$
> (e^A)^T = e^{(A^T)}
> $$
> 
> > This happens because the transpose operation is linear and continuous, so we can transpose the series term-by-term!
