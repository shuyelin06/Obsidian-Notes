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

Analogous to $e^0 = 1$, for the $0$ matrix, 
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

> [!Abstract] Theorem
> Let $A$ be an $n \times n$ matrix.
> 1. If $\lambda$ is an eigenvalue for $A$, then $e^\lambda$ is an eigenvalue for $e^A$.
> 2. More precisely, if $\vec{v}$ is an eigenvector for $A$ with eigenvalue $\lambda$, then $\vec{v}$ is an eigenvector for $e^A$ with eigenvalue $e^\lambda$.

The **trace** of an $n \times n$ matrix is the sum of the diagonal entries of $A$ denoted $\text{tr} A$.
$$
\text{tr} A = \sum_{i=1}^n a_{ii}
$$

> [!Abstract] Theorem
> For an $n \times n$ matrix $A$, 
> 1. $\text{tr} A$ equals the sum of the eigenvalues of $A$.
> 2. $\det{A}$ equals the product of the eigenvalues of $A$.

Using these facts, we can explain the following.

> [!Abstract] Theorem
> $$
> \det (e^A) = e^{\text{tr} A}
> $$
> In particular, if $A$ has real entries, then the determinant of $e^A$ will always strictly be positive.
> > We can also use this to know if a matrix isn't an exponential of any matrix!
> 
> > [!Note]- Proof 
> > 
> > If the eigenvalues of $A$ are $\lambda_1, \dots \lambda_n$, then the eigenvalues of $e^A$ are $e^{\lambda_1}, \dots e^{\lambda_n}$, and as the determinant is the product of eigenvalues,
> > $$
> > \det{e^A} = e^{\lambda_1} \dots e^{\lambda_n} = e^{\lambda_1 + \dots + \lambda_n} = e^{\text{tr} A}
> > $$

## Rotations
So, for what $A$ is $e^A$ a rotation? To answer this question, we must first define what exactly a "rotation" matrix is.

An $n \times n$ matrix $Q$ is **orthogonal** if $Q$ satisfies
$$
Q^T Q = I_n
$$

> [!Abstract] Theorem
> Let $Q$ be $n \times n$. The following are equivalent:
> 1. $Q$ is an orthogonal matrix.
> 2. $Q^{-1} = Q^T$
> 3. The columns of $Q$ form an **orthonormal basis** for $\mathbb{R}^n$, meaning they are orthogonal to each other and are unit vectors.
> 4. $||Q \vec{v}|| = || \vec{v} ||$ for all $\vec{v} \in \mathbb{R}^n$. In other words, $Q$ preserves the length of vectors.

Rotations and reflections are orthogonal matrices by condition (4) of the theorem! How do we know what an orthogonal matrix is classified as?

Note that every orthogonal $Q$ satisfies
$$
\det{Q} = \pm 1
$$

> [!Note]- Proof
> $$
> \begin{align*}
> Q^T Q = I_n \\
> \det{Q^T Q} = \det{I_n} = 1 \\
> \det{Q^T} \det{Q} = 1 \\
> \det{Q}^2 = 1 \\
> \det{Q} = \pm 1
> \end{align*}
> $$

It turns out, rotations have determinant 1, and reflections have determinant -1.

So, we can define a **rotation matrix** as an orthogonal matrix with determinant 1. So, for $A$ such that $e^A$ is a rotation, we need $e^A$ to be orthogonal with $\det{e^A} = 1$. 

We know that $\det{e^A} > 0$ for any $A$. Furthermore, for $e^A$ to be orthogonal, we need that
$$
(e^A)^T = (e^A)^{-1} \iff e^{A^T} = e^{-A}
$$
So, this relation holds whenever $A^T = -A$. $A$ is called **skew-symmetric** if $A^T = -A$.

> [!Abstract] Theorem
> If $A$ is skew-symmetric, then $e^{tA}$ will be a rotation matrix for any real $t$!

> [!Example]+ Example: 2-Dimensional Rotations
> $$
> A = \begin{bmatrix} 0 & -1 \\ 1 0 \end{bmatrix}
> $$
> Observe that this is a skew-symmetric matrix, and we saw that
> $$
> e^{tA} =
> \begin{bmatrix} 
> \cos t & - \sin t \\
> \sin t & \cos t
> \end{bmatrix}
> $$

We ask, are there any other $2 \times 2$ skew-symmetric matrices? For $A$ to be skew-symmetric,
$$
\begin{bmatrix} a & c \\ b & d \end{bmatrix} = 
\begin{bmatrix} -a & -b \\ -c & -d \end{bmatrix}
$$
So, we need $a = -a$, $c = -b$, $b = -c$, and $d = -d$. Thus forces $a = d = 0$, and $b,c$ must be opposites of each other. So, we have general form
$$
A = \begin{bmatrix} 0 & -c \\ c & 0 \end{bmatrix} = 
c \begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix}
$$
So, there are no other skew-symmetric matrices!

---

Similarly, for the 3-dimensional case, we can find general form
$$
A = 
\begin{bmatrix}
0 & -d & -g \\ 
d & 0 & -h \\
g & h & 0
\end{bmatrix}
$$

So, $e^{tA}$ will give us a family of rotations! But what rotation does it actually represent? In other words, what is the rotations' axis and angle?
> Note that the axis must always go through the origin, as the transformation is linear.

Consider a skew-symmetric matrix $A$ of the form
$$
A = 
\begin{bmatrix}
0 & -z & y \\ 
z & 0 & -x \\
-y & x & 0
\end{bmatrix}
$$
Observe that we can make a vector $\vec{v} = (x,y,z)$, which is an eigenvector for matrix $A$ with eigenvalue 0! This implies that $\vec{v}$ is also an eigenvector for $e^{A}$ (similarly, $e^{tA}$), with eigenvalue $e^0 = 1$.

This means that the transformation $e^{tA}$ does nothing to the vector $\vec{v}$! Meaning, if $e^{tA}$ is a rotation matrix, then $\vec{v}$ must be the axis of rotation!

So, the family of rotations given by $e^{tA}$ has the axis of rotation given as the line through the origin given by vector $\vec{v} = (x,y,z)$. Furthermore, as $t$ changes, so does the angle of rotation.
> $t$ may not be exactly the angle of rotation though, since $A$ may stretch the vectors!

> [!Abstract] Theorem: 3D Rotation Matrices
> Let $\vec{u} = (x,y,z)$ be a unit vector, and let
> 
> $$
> A = 
> \begin{bmatrix}
> 0 & -z & y \\
> z & 0 & -x \\
> -y & x & 0 
> \end{bmatrix}
> $$
> 
> Then, the rotation about the line through the origin in the direction of $\vec{u}$ by $\theta$ radians is given by $e^{\theta A}$!
> > This theorem is 3D specific! Don't try to generalize it to higher dimensions.

> [!Example]+ Example: Rotation Matrices
> Use the above theorem to find $RZ(\theta)$.
> 
> Here, we want to rotate about unit vector $\vec{u} = (0,0,1)^T$. We can find our rotation by taking
> $$
> A = 
> \begin{bmatrix}
> 0 & -1 & 0 \\
> 1 & 0 & 0 \\
> 0 & 0 & 0
> \end{bmatrix}
> $$
> 
> And taking the exponential
> $$
> e^{\theta A} = 
> \begin{bmatrix} 
> \cos \theta & -\sin \theta & 0 \\
> \sin \theta & \cos \theta & 0 \\
> 0 & 0 & 1
> \end{bmatrix}
> $$

> [!Example]- Example: Rotation Matrices (2)
> Find the matrix for rotation by 27 degrees around axis through origin in the direction of $\vec{v} = (3,2,-6)^T$
> 
> First, we take a unit vector in the same direction
> $$
> \vec{u} = \frac{\vec{v}}{||\vec{v}||} = (3/7, 2/7, -6/7)^T
> $$
> Furthermore, we have angle $\frac{27 \pi}{180} = \frac{3\pi}{20}$
> 
> We can use this to find
> $$
> A = 
> \begin{bmatrix}
> 0 & 6/7 & 2/7 \\ 
> -6/7 & 0 & -3/7 \\
> -2/7 & 3/7 & 0
> \end{bmatrix}
> $$
> 
> And find our rotation matrix as
> $$
> e^{\frac{3\pi}{20} A}
> $$

> [!Example]+ Example: Rotation Matrices (3)
> $$
> A =
> \begin{bmatrix}
> 0 & 1 & 2 \\
> -1 & 0 & 3 \\
> -2 & -3 & 0
> \end{bmatrix}
> $$
> 
> We know $e^A$ is some 3D rotation. What is it's axis / angle?
> 
> We can use the theorem to find this. First, we need to recognize $A$ as the matrix built from a unit vector, by finding scalar multiple
> $$
> A = 
> \sqrt{14} \begin{bmatrix}
> 0 & 1/\sqrt{14} & 2/\sqrt{14} \\
> -1/\sqrt{14} & 0 & 3/\sqrt{14} \\
> -2/\sqrt{14} & -3/\sqrt{14} & 0
> \end{bmatrix} 
> $$
> 
> So, we find that we have a rotation about
> $$
> \vec{u} = (-3/\sqrt{14}, 2/\sqrt{14}, -1/\sqrt{14})
> $$
> With rotation $\sqrt{14}$ radians.

# Singular Value Decomposition
## Review: Symmetric Matrices and the Spectral Theorem
An $n \times n$ matrix $A$ is **symmetric** if
$$
A^T = A
$$

> [!Abstract] Theorem: Spectral Theorem for Real Symmetric Matrices
> Let $A$ be an $n \times n$ symmetric matrix with real entries. Then,
> 1. It has all real eigenvalues
> 2. Any pair of eigenvectors for $A$ with different eigenvalues are going to be orthogonal
> 3. $A$ is diagonalizable
> 4. There is an orthonormal basis for $\mathbb{R}^n$ that consists of eigenvectors for this matrix.
> 5. $A$ can be **orthogonally diagonalized**, in other words, for orthogonal matrix $P$,
>    $$
>    A = P D P^T
>    $$
>    > Recall that $P^T = P^{-1}$ is equivalent to having orthonormal columns.

> [!Example]+ Example: Orthogonally Diagonalizing a Symmetric Matrix 
> $$
> A = 
> \begin{bmatrix}
> 13 & -6 \\ -6 & -3
> \end{bmatrix}
> $$
> 
> Notice how $A$ is a symmetric matrix, so its orthogonally diagonalizable. Let's orthogonally diagonalize it.
> - We find eigenvalues $\lambda_1 = -5, \lambda_2 = 15$.
> - We find eigenvectors $\vec{v}_1 = (1,3)^T, \vec{v}_2 = (-3, 1)^T$.
> 
> Our eigenvectors are orthogonal, but not orthonormal! Thus, we need to rescale them to get unit eigenvectors.
> $$
> \vec{v}_1 = \left(\frac{1}{\sqrt{10}}, \frac{3}{\sqrt{10}}\right)^T \qquad
> \vec{v}_2 = \left(\frac{-3}{\sqrt{10}}, \frac{1}{\sqrt{10}}\right)^T
> $$
> 
> So, we orthogonally diagonalize $A$ as
> $$
> A = P D P^T = 
> \begin{bmatrix}
> \frac{1}{\sqrt{10}} & \frac{-3}{\sqrt{10}} \\
> \frac{3}{\sqrt{10}} & \frac{1}{\sqrt{10}}
> \end{bmatrix}
> \begin{bmatrix}
> -5 & 0 \\
> 0 & 15
> \end{bmatrix}
> \begin{bmatrix}
> \frac{1}{\sqrt{10}} & \frac{3}{\sqrt{10}} \\
> \frac{-3}{\sqrt{10}} & \frac{1}{\sqrt{10}}
> \end{bmatrix}
> $$

## Singular Value Decompositions (SVDs)
Let $A$ be an $m \times n$ matrix with real entries. A **singular value decomposition (SVD)** for $A$ is a factorization of the form 
$$
A = U \Sigma V^T
$$
Where
- $U$ is an $m \times m$ orthogonal matrix
- $\Sigma$ is $m \times n$ diagonal matrix, with non-negative (real) diagonal entries
  $$
  \Sigma = 
  \begin{bmatrix}
  \sigma_1 & 0 & 0 & \dots & 0 \\
  0 & \sigma_2 & 0 & \dots & 0 \\
  0 & 0 & \sigma_2 & \dots & 0 \\
  \vdots & \vdots & \vdots & \ddots & \vdots \\
  0 & 0 & 0 & \dots & \sigma_n \\
  0 & 0 & 0 & \dots & 0 \\
  \vdots & \vdots & \vdots & & \vdots \\
  0 & 0 & 0 & \dots & 0 
  \end{bmatrix} \qquad \sigma_i \ge 0
  $$
  known as the **singular values** of $A$.
- $V^T$ is an $n \times n$ orthogonal matrix, where the columns $\vec{v}_1, \dots \vec{v}_n$ are known as the **right singular vectors** of $A$.

Singular value decompositions are very general!
> Note that even for a square diagonalizable $A$, its diagonalization need not be its singular value decomposition!

> [!Example] Example
> $$
> A = 
> \begin{bmatrix}
> 1 & 1 \\ 0 & 1 \\ 1 & 0
> \end{bmatrix}
> = 
> \begin{bmatrix}
> 2/\sqrt{6} & 0 & -1/\sqrt{3} \\
> 1/\sqrt{6} & 1/\sqrt{2} & 1/\sqrt{3} \\
> 1/\sqrt{6} & -1/\sqrt{2} & 1/\sqrt{3}
> \end{bmatrix}
> \begin{bmatrix}
> \sqrt{3} & 0 \\0 & 1 \\ 0 & 0
> \end{bmatrix}
> \begin{bmatrix}
> 1/\sqrt{2} & -1/\sqrt{2} \\
> 1/\sqrt{2} & 1/\sqrt{2}
> \end{bmatrix}^T
> $$

How to we find singular value decompositions? First, note that for any $m \times n$ matrix $A$,
- $A^T A$ and $A A^T$ are symmetric matrices of size $n \times n$ and $m \times m$, respectively. Hence, by the spectral theorem, they are orthogonally diagonalizable.
- The eigenvalues of $A^T A$ and $A A^T$ are non-negative real numbers.
- $A^T A$ and $A A^T$ have the same eigenvalues (with the same multiplicities), except for $\lambda = 0$.

Now suppose that $A$ has a singular value decomposition. 
$$
A = U \Sigma V^T
$$
Then,
$$
\begin{align*}
A^T A 
&= (U \Sigma V^T)^T (U \Sigma V^T) \\
&= V \Sigma^T U^T U \Sigma V^T \\
&= V (\Sigma^T \Sigma) V^T
\end{align*}
$$
This is an orthogonal diagonalization of our matrix! Similarly, we can find
$$
A A^T = U (\Sigma \Sigma^T) U^T
$$
So, we can find
- $V$ as an orthonormal basis of eigenvectors for $A^T A$ ($P$ in the orthogonal diagonalization)
- $\Sigma$ as the (positive) square roots of $A^T A$'s eigenvalues
- $U$ as the orthonormal basis of eigenvectors for $A A^T$ ($P$ in the orthogonal diagonalization)

Note that this equation is equivalent to
$$
\begin{align*}
A V &= U \Sigma \\
\begin{bmatrix}
A\vec{v}_1 & \dots & A\vec{v}_n
\end{bmatrix}
&= 
\begin{bmatrix}
\sigma_1 \vec{u}_1 & \dots & \sigma_n \vec{u}_n
\end{bmatrix}
\end{align*}
$$
So, an additional requirement for these systems is that for any $i$, $A \vec{v}_i = \sigma_i \vec{u}_i$, and furthermore, if $\sigma_i \ne 0$, then this implies
$$
\vec{u}_i = \frac{1}{\sigma_i} A \vec{v}_i
$$

> [!Abstract] Theorem: Singular Value Decompositions
> Every $m \times n$ matrix $A$ has a singular value decomposition
> $$
> A = U \Sigma V^T
> $$
> Where
> - The diagonal entries of $\Sigma$ are the square roots of the eigenvalues for $A^T A$
> - The columns of $V$ are an orthonormal basis of eigenvectors for $A^T A$
> - The columns of $U$ are an orthonormal basis of eigenvectors for $A A^T$
> 
> Chosen such that
> $$
> A \vec{v}_i = \sigma_i \vec{u}_i
> $$
> For each $i$.

So, one strategy to find an SVD for $A$ is as follows:
1. Find the eigenvectors and eigenvalues of $A^T A$ to get the $\vec{v}_i$'s and $\sigma_i$'s.
2. Use the fact that $\vec{u}_i = \frac{1}{\sigma_i} A \vec{v}_i$ to get the $\vec{u}_i$'s for when $\sigma_i$ is non-zero.
3. If necessary, get the rest of the $\vec{u}_i$'s (for $\sigma_i = 0$) by finding $\lambda = 0$ eigenvectors for $A A^T$.

By convention, we order the singular values in decreasing order. 
$$
\sigma_1 \ge \sigma_2 \ge \sigma_3 \ge \dots
$$
> This can become very unreasonable to do by hand for many matrices! We can use MATLAB to do a SVD for us, using command `[U, S, V] = svd(A)`.

> [!Example]- Example: Singular Value Decompositions
> Find the SVD of
> $$
> A = 
> \begin{bmatrix}
> 1 & 0 \\ 0 & 1 \\ 4 & 4
> \end{bmatrix}
> $$
> 
> We start by finding
> $$
> A^T A = 
> \begin{bmatrix}
> 17 & 16 \\ 16 & 17
> \end{bmatrix}
> $$
> To find eigenvalues $\lambda_1 = 33, \lambda_2 = 1$, and eigenvectors 
> $$
> \vec{v}_1 = (1/\sqrt{2}, 1/\sqrt{2})^T \qquad 
> \vec{v}_2 = (1/\sqrt{2}, -1/\sqrt{2})^T
> $$
> These are our right singular vectors, with singular values $\sigma_1 = \sqrt{33}, \sigma_2 = \sqrt{1} = 1$!
> 
> We now find our $\vec{u}_i$'s.
> $$
> \begin{align*}
> \vec{u}_1 = \frac{1}{\sqrt{33}} A \vec{1} = \left( \frac{1}{\sqrt{66}}, \frac{1}{\sqrt{66}}, \frac{8}{\sqrt{66}} \right)^T \\
> \vec{u}_2 = A \vec{v}_2 = \left( \frac{1}{\sqrt{2}}, -\frac{1}{\sqrt{2}}, 0 \right)^T
> \end{align*}
> $$
> Finally, we need a $\vec{u}_3$, a unit eigenvector for $A A^T$ with eigenvalue $\lambda = 0$. So, we solve $A A^T \vec{x} = 0$.
> $$
> \vec{u}_3 = \left( \frac{4}{\sqrt{33}}, \frac{4}{\sqrt{33}}, -\frac{1}{\sqrt{33}} \right)
> $$
> 
> This gives us final result
> $$
> A = 
> U \Sigma V^T =
> \begin{bmatrix} 
> \frac{1}{\sqrt{66}} & \frac{1}{\sqrt{2}} & \frac{4}{\sqrt{33}} \\
> \frac{1}{\sqrt{66}} & -\frac{1}{\sqrt{2}} & \frac{4}{\sqrt{33}} \\
> \frac{8}{\sqrt{66}} & 0 & -\frac{1}{\sqrt{33}}
> \end{bmatrix}
> \begin{bmatrix} 
> \sqrt{33} & 0 \\ 0 & 1 \\ 0 & 0
> \end{bmatrix}
> \begin{bmatrix}
> \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\
> \frac{1/}{\sqrt{2}} & -\frac{1}{\sqrt{2}}
> \end{bmatrix}^T
> $$

## Inverses and Pseudoinverses
> [!Tip] Motivation
> Using SVDs, we can define the concept of a "pseudoinverse" for non-invertible matrices!

Suppose $A$ is $n \times n$ and invertible with SVD 
$$
A = U \Sigma V^T =
U 
\begin{bmatrix}
\sigma_1 & & & \\
 & \sigma_2 & & \\
 & & \ddots & \\
 & & & \sigma_n
\end{bmatrix}
V^T
$$
Where all $\sigma_i \ne 0$ (otherwise, $A$ would be non-invertible). Then,
$$
A^{-1} = (U \Sigma V^T)^{-1} = V \Sigma^{-1} U^T =
V 
\begin{bmatrix}
1/\sigma_1 & & & \\
 & 1/\sigma_2 & & \\
 & & \ddots & \\
 & & & 1/\sigma_n
\end{bmatrix}
U^T
$$
This is the SVD of $A$'s inverse matrix!
> Note how $U,V$ got swapped, and all $\sigma_i$'s get inverted!

This gives us a notion to find inverse matrices, even for matrices that don't have a inverse! This defines a "pseudoinverse".

Now, consider a general $m \times n$ matrix $A$ with SVD 
$$
A = U \Sigma V^T 
$$
We can define the **Moore-Penrose Pseudoinverse** of $A$ to be
$$
A^+ = V \Sigma^+ U^T
$$
Where $\Sigma^+$ is the transpose of the matrix $\Sigma$, where all non-negative singular values are inverted ($1/\sigma_i, \sigma_i \ne 0$).

Some properties of the pseudo-inverse are as follows:
- If $A$ is $n \times n$ and invertible, then $A^+ = A^{-1}$.
- If $A$ is $m \times n$ with linearly independent columns, then $A^+ = (A^T A)^{-1} A^T$.

> [!Example]- Example: Pseudo-Inverses
> $$
> A = 
> \begin{bmatrix}
> 1 & 0 \\ 0 & 1 \\ 4 & 4
> \end{bmatrix}
> $$
> 
> A has SVD
> $$
> A = 
> U \Sigma V^T =
> \begin{bmatrix} 
> \frac{1}{\sqrt{66}} & \frac{1}{\sqrt{2}} & \frac{4}{\sqrt{33}} \\
> \frac{1}{\sqrt{66}} & -\frac{1}{\sqrt{2}} & \frac{4}{\sqrt{33}} \\
> \frac{8}{\sqrt{66}} & 0 & -\frac{1}{\sqrt{33}}
> \end{bmatrix}
> \begin{bmatrix} 
> \sqrt{33} & 0 \\ 0 & 1 \\ 0 & 0
> \end{bmatrix}
> \begin{bmatrix}
> \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\
> \frac{1/}{\sqrt{2}} & -\frac{1}{\sqrt{2}}
> \end{bmatrix}
> $$
>
> So, we can find its pseudo-inverse as
> $$
> A^+ = 
> V \Sigma U^T =
> \begin{bmatrix}
> \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\
> \frac{1/}{\sqrt{2}} & -\frac{1}{\sqrt{2}}
> \end{bmatrix}
> \begin{bmatrix} 
> \frac{1}{\sqrt{33}} & 0 & 0 \\ 0 & 1 & 0
> \end{bmatrix}
> \begin{bmatrix} 
> \frac{1}{\sqrt{66}} & \frac{1}{\sqrt{2}} & \frac{4}{\sqrt{33}} \\
> \frac{1}{\sqrt{66}} & -\frac{1}{\sqrt{2}} & \frac{4}{\sqrt{33}} \\
> \frac{8}{\sqrt{66}} & 0 & -\frac{1}{\sqrt{33}}
> \end{bmatrix}^T
> $$

Now consider a linear system $A \vec{x} = \vec{b}$. 
- If $A$ is $n \times n$ and invertible, then
  $$
  \vec{x} = A^+ \vec{b} A^{-1} \vec{b} 
  $$
- If $A$ is $n \times m$ with linearly independent columns, then
  $$
  \vec{x} = A^+ \vec{b} = (A^T A)^{-1} A^T \vec{b}
  $$
  The unique least-squares solution to the system!

What if $A \vec{x} = \vec{b}$ has infinitely many solutions? Or what if $A \vec{x} = \vec{b}$ is inconsistent but has infinitely many least-squares solutions? What does $\vec{x} = A^+ \vec{b}$ mean in these cases?

> [!Abstract] Theorem
> The vector $\vec{x} = A^+ \vec{b}$ is the least-squares solution of the system $A \vec{x} = \vec{b}$, with the smallest possible norm $|| \vec{x} ||$. 

# Image Compression
## Matrix Approximations
Consider the matrix $A$, with SVD $A = U \Sigma V^T$. 
$$
A = U 
\begin{bmatrix}
\sigma_1 & & & \\
 & \sigma_2 & & \\
 & & \ddots & \\
 & & & \sigma_r \\
 & & & & 0 \\
 & & & & & 0
\end{bmatrix}
V^T
\qquad
\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_r > 0
$$
We ask, how could we approximate $A$ with a lower rank matrix?
> $A$ has rank equal to the number of non-zero singular values!

Well, for a rank $1 \le k \le r$, one way we could approximate $A$ is by dropping all singular values between $k + 1$ to $r$!
$$
A_k = U 
\begin{bmatrix}
\sigma_1 & & & \\
 & \ddots & \\
 & & \sigma_k \\
 & & & 0 \\
 & & & & 0
\end{bmatrix}
V^T
$$
We can find that this is actually the best approximation to $A$ possible.

> [!Abstract] Theorem: Eckart-Young Theorem
> $A_k$ is the best $k$ approximation to $A$, with error given by the magnitude of the singular values we dropped.
> $$
> || A - A_k ||_F = \sqrt{\sigma_{k+1}^2 + \dots + \sigma_r^2}
> $$
> > This is known as the Frobenius norm, and we can also find it by taking the sum of the squares of the entries in the matrix (then square rooting).

> [!Example] Example
> Find the best rank 1 approximation to
> $$
> A = 
> \begin{bmatrix}
> 1 & 7 \\ 2 & 15
> \end{bmatrix}
> $$
> 
> We can find SVD
> $$
> A =
> \begin{bmatrix}
> -0.4233 & -0.9060 \\ -0.9060 & 0.4233
> \end{bmatrix}
> \begin{bmatrix}
> 16.7032 & 0 \\ 0 & 0.0599
> \end{bmatrix}
> \begin{bmatrix}
> -0.1338 & -0.9910 \\ -0.9910 & 0.1338
> \end{bmatrix}^T
> $$
> 
> With this, we can find rank 1 approximation by dropping the smallest singular value.
> $$
> A_1 =
> \begin{bmatrix}
> -0.4233 & -0.9060 \\ -0.9060 & 0.4233
> \end{bmatrix}
> \begin{bmatrix}
> 16.7032 & 0 \\ 0 & 0
> \end{bmatrix}
> \begin{bmatrix}
> -0.1338 & -0.9910 \\ -0.9910 & 0.1338
> \end{bmatrix}^T = 
> \begin{bmatrix}
> 0.9462 & 7.0073 \\ 2.0251 & 14.9966
> \end{bmatrix}
> $$
> 
> And furthermore, according to the theorem above, we can find error
> $$
> || A - A_1 ||_F = \sqrt{0.0599^2} = 0.0599
> $$
> 
> Now say we do a rank 1 approximation on 
> $$
> B = 
> \begin{bmatrix}
> 3 & 4 \\ -5 & 3
> \end{bmatrix}
> $$
> 
> We find $\sigma_1 \approx 5.9, \sigma_2 \approx 4.9$! Because $\sigma_2$ is much larger than our previous example, we find a higher error, so we should expect our approximation to be a lot worse.

## Image Compression
But why do we want to be able to approximate matrices like this?

Well, if we write
$$
\begin{align*}
U &= [ \vec{u}_1, \vec{u}_2 \dots \vec{u}_m ]  \\
V &= [ \vec{v}_1, \vec{v}_2 \dots \vec{v}_n ] \\
A &= U \Sigma V^T \\ 
&= [ \vec{u}_1, \vec{u}_2 \dots \vec{u}_m ]
\begin{bmatrix}
\sigma_1 & & & \\
 & \sigma_2 & & \\
 & & \ddots & \\
 & & & \sigma_r \\
 & & & & 0 \\
 & & & & & 0
\end{bmatrix}
\begin{bmatrix}
\vec{v}_1^T \\ \vec{v}_2^T \\ \vdots \\ \vec{v}_n^T
\end{bmatrix} \\
&= 
\sigma_1 \vec{u}_1 \vec{v}_1^T + 
\sigma_2 \vec{u}_2 \vec{v}_2^T + \dots + 
\sigma_r \vec{u}_r \vec{v}_r^T
\end{align*}
$$
> Each of these terms yields a $m \times n$ matrix!

> [!Abstract] Theorem
> If $A$ has rank $r$, then
> $$
> A = \sigma_1 \vec{u}_1 \vec{v}_1^T + 
> \sigma_2 \vec{u}_2 \vec{v}_2^T + \dots + 
> \sigma_r \vec{u}_r \vec{v}_r^T
> $$

Consequently, the lower rank approximations to $A$ are:
$$
\begin{align*}
A_1 &= \sigma_1 \vec{u}_1 \vec{v}_1^T \\
A_2 &= \sigma_1 \vec{u}_1 \vec{v}_1^T + 
\sigma_2 \vec{u}_2 \vec{v}_2^T \\
&\vdots \\
A_k &= \sigma_1 \vec{u}_1 \vec{v}_1^T + 
\sigma_2 \vec{u}_2 \vec{v}_2^T 
+ \dots + \sigma_k \vec{u}_k \vec{v}_k^T \\
\end{align*}
$$
> We can find the lower rank approximations by dropping the smallest $\sigma_i$ terms!

This gives us a way to store lower rank approximations! For example, instead of explicitly storing $A_1$, we only need to store $\sigma_1, \vec{u}_1, \vec{v}_1$, and the computer can reconstruct the original matrix for us! 

This is a lot cheaper than storing $A_1$. If $A_1$ is $1000 \times 1000$, for example, then instead of storing the entire matrix (1 million entries), we only need to store $1 + 1000 + 1000 = 2001$ entries! If we store these entries in a file, then the computer can take these entries and regenerate the original image!

Generalizing, we can compute $n \times n$ matrix $A_k$ provided we know and store the collection
$$
\begin{cases}
\sigma_1 \quad \dots \quad \sigma_k \\
\vec{u}_1 \quad \dots \quad \vec{u}_k \\
\vec{v}_1 \quad \dots \quad \vec{v}_k
\end{cases}
$$
Which would take $k + kn + kn = (2n + 1) k$ entries, opposed to the original $n^2$ entries of the matrix! In fact we can actually have our approximation take $2nk$ entries, if we multiply the $\sigma_i$'s into one of the vectors!

This will be useful if
$$
2kn < n^2 \Longrightarrow k < \frac{n}{2}
$$
