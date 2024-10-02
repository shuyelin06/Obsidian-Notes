---
title: Least Squares
tags:
- math401
---

# Least Squares / Curve Fitting 
Given a set of data in space, we ask: how do we find a "best fit line"?
> Finding such a line would let us make generalizations and inferences from our data!

## Least Squares Solutions
Suppose we have an inconsistent linear system $A \vec{x} = \vec{b}$. As it is inconsistent, we simply cannot find an $\vec{x}$ satisfying the system. 

This makes sense for our purposes! It's often impossible to find an exact solution for a line passing through all points (points may not be co-linear). However, it is possible to find an exact solution for a line **minimizing** its distance to all points! This is the idea behind least squares.

A **least squares solution** of $A \vec{x} = \vec{b}$ is a vector $\hat{x}$ that minimizes the distance from $A \hat{x}$ to $\vec{b}$, known as the **least squares error**.
$$
|| A \hat{x} - \vec{b} ||
$$
> For some $\hat{x}$, this yields us the sum of the squares of the vertical distances between our line and the true collection of points.

Note that with this minimizer, for any other $\vec{x}$,
$$
|| A \vec{x} - \vec{b} || \ge || A \hat{x} - \vec{b} ||
$$

We first build up some context below.

## Finding the Least Squares Solution
> [!Info] Dot Products
> Given $\vec{v}, \vec{w}$ in $\mathbb{R}^n$, their **dot product** is
> $$
> \vec{v} \cdot \vec{w} = \vec{v}^T \vec{w} = v_1 w_1 + v_2 w_2 + \dots
> $$
>
> The dot product relates to a handful of geometric quantities like lengths and angles.
>
> The **length** (**norm**) of a vector $\vec{v}$ is given as
> $$
> || \vec{v} || = \sqrt{\vec{v} \cdot \vec{v}} = \sqrt{v_1^2 + v_2^2 + \dots}
> $$
>
> And for any $\vec{v}, \vec{w}$ in $\mathbb{R}^n$, we have
> $$
> \vec{v} \cdot \vec{w} = || \vec{v} || || \vec{w} || \cos\theta
> $$
> where $\theta$ is the angle between $\vec{v}$ and $\vec{w}$. 
>
> We say $\vec{v}, \vec{w}$ are **orthogonal** if $\vec{v} \cdot \vec{w} = 0$.
> > Note that this means that $\vec{0}$ is uniquely orthogonal to every vector $\vec{w}$ in $\mathbb{R}^n$.

> [!Info] Orthogonal Projections
> Let $W$ be a subspace of $\mathbb{R}^n$ ($W$ is some span of a collection of vectors, a line through the origin, a plane through the origin, etc).
> 
> The **orthogonal projection** of $\vec{v}$ onto a subspace $W$, denoted $\text{proj}_w \vec{v}$, is the closest vector in $W$ to $\vec{v}$. It satisfies
> $$
> || \vec{v} - \text{proj}_W \vec{v} || \le || \vec{v} - \vec{w} ||
> $$
> 
> $\vec{v} - \text{proj}_W \vec{v}$ is orthogonal to every possible $\vec{w}$ in $W$.

The **column space** of an $m \times n$ matrix $A$ is the span of its columns (the set of all linear combinations of its columns). Note that $\text{Col}A$ is a subspace of $\mathbb{R}^m$.

Every linear combination of the columns of $A$ has the form $A \vec{x}$ for some $\vec{x}$ in $\mathbb{R}^n$. So
$$
\text{Col}A = \{ A \vec{x} : \vec{x} \in \mathbb{R}^n \}
$$
Here, $\vec{b} \in \text{Col}A$ if and only if there is some $\vec{x} \in \mathbb{R}^n$ such that $A \vec{x} = \vec{b}$ if and only if $A \vec{x} = \vec{b}$ is a consistent linear system.

Now suppose $A \vec{x} = \vec{b}$ is inconsistent. So, by above, if there is no solution then $\vec{b} \not\in \text{Col}A$. Let $\hat{b} = \text{Proj}_{\text{Col} A} \vec{b}$. Then, because $\hat{b} \in \text{Col}A$, we found the existence of an $\hat{x}$ such that
$$
A \hat{x} = \hat{b}
$$
Such an $\hat{x}$ is a least squares solution, because $\hat{b}$ is the closest vector in $A$'s column space to $\vec{b}$!

We know that the vector $\vec{b} - \hat{b}$ is orthogonal to every vector $\vec{w} \in A$. In other words, it is orthogonal to every $A \vec{y}$ for any $\vec{y}$. So,
$$
\begin{align*}
(A \vec{y}) \cdot (\vec{b} - A \hat{x}) = 0 \\
(A \vec{y})^T (\vec{b} - A \vec{x}) = 0 \\
\vec{y}^T A^T (b - A \hat{x} 0 = 0 \\
\vec{y}^T (A^T \vec{b} - A^T A \vec{x}) = 0 \\
\vec{y} \cdot (A^T \vec{b} - A^T A \hat{x}) = 0
\end{align*}
$$
For every $\vec{y}$. This means that $A^T \vec{b} - A^T A \hat{x}$ **must** be the 0 vector, so
$$
A^T \vec{b} - A^T A \hat{x} = 0 \Longrightarrow A^T A \hat{x} = A^T \vec{b}
$$
This is the equation that least squares must satisfy! So, to find $\hat{x}$, we solve the linear system
$$
A^T A \hat{x} = A^T \vec{b}
$$
Note the following:
1. $A^T A \hat{x} = A^T \vec{b}$ is always consistent (has a solution)
2. $A^T A \hat{x} = A^T \vec{b}$ has a unique solution if and only if $A^T A$ is invertible, if and only if $A$ has linearly independent columns.

> [!Example]+ Example: Least Squares
> Find the least squares solutions to
> $$
> \begin{cases}
> x_1 + x_2 = 6  \\
> -x_1 + x_2 = 3 \\
> 2x_1 + 3x_2 = 9
> \end{cases}
> $$
> 
> We can represent this as the system
> $$
> A \hat{x} = \vec{b} \Longrightarrow
> \begin{bmatrix}
> 1 & 1 \\
> -1 & 1 \\
> 2 & 3
> \end{bmatrix}
> \begin{bmatrix}
> x_1 \\ x_2
> \end{bmatrix}
> = 
> \begin{bmatrix}
> 6 \\ 3 \\ 9
> \end{bmatrix}
> $$
> We now solve $A^T A \hat{x} = A^T \vec{b}$.
> $$
> \begin{bmatrix}
> 6 & 6 \\ 6 & 11
> \end{bmatrix}
> \hat{x} = 
> \begin{bmatrix}
> 21 \\ 36
> \end{bmatrix}
> $$

> [!Example]- Example: Least Squares (2) 
> | X | Y |
> | :-: | :-: |
> | 1 | 1 |
> | 2 | 2.4 | 
> | 3 | 3.6 |
> | 4 | 4 |
>
> Find a line best fitting the data.
>
> What we can do is assume we have a line $y = B_0 + B_1 x$, and then sub in the points. This will yield us vectors that we can solve with least squares! 

We can use least squares to solve a multitude of problems! As long as we can find a corresponding system of equations, we can solve the system with least squares.

> [!Example]+ Example: Best-Fit Parabola
> | x | y | 
> | :-: | :-: |
> | 1 | -0.15 | 
> | 2 | 0.68 | 
> | 3 | 1.21 |
> | 4 | 0.86 | 
> | 5 | -0.08 |
> 
> Find a best fit parabola taking on the form
> $$
> y = \beta_0 + \beta_1 x + \beta_2 x^2
> $$
> 
> We can form a linear system by plugging in our x and y values.
> $$
> \begin{align*}
> -0.15 = \beta_0 + \beta_1 (1) + \beta_2 (1)^2 \\
> 0.68 = \beta_0 + \beta_1 (2) + \beta_2 (2)^2 \\
> 1.21 = \beta_0 + \beta_1 (3) + \beta_2 (3)^2 \\
> 0.86 = \beta_0 + \beta_1 (4) + \beta_2 (4)^2 \\
> -0.08 = \beta_0 + \beta_1 (5) + \beta_2 (5)^2
> \end{align*}
> $$
> 
> This is a linear system! We can write $A, x$, and $b$ as follows
> $$
> A = 
> \begin{bmatrix}
> 1 & 1 & 1 \\
> 1 & 2 & 4 \\
> 1 & 3 & 9 \\
> 1 & 4 & 16 \\
> 1 & 5 & 25
> \end{bmatrix}
> \qquad
> x =
> \begin{bmatrix}
> \beta_0 \\ \beta_1 \\ \beta_2
> \end{bmatrix}
> \qquad
> b = 
> \begin{bmatrix}
> -0.15 \\ 0.68 \\ 1.21 \\ 0.86 \\ -0.08
> \end{bmatrix}
> $$
> We can use least squares to solve this!

But not all models will work with least squares! Least squares requires that we have a linear system, so anything that cannot form a linear system after subbing in x,y will not work.

> [!Example] Example: Applying Least-Squares to Non-Linear Systems
> Suppose we have a non-linear model
> $$
> y = \beta_0 + \beta_1 e^{\beta_2 x}
> $$
> 
> For non-linear systems, one work around is to make an educated guess for the non-linear variables, and solving the subsequent linear system! So, we make a guess for $\beta_2$, and then solve $\beta_0$ and and $\beta_1$!
> 
> We can then compare the least squares errors to find which combination of variables works best!


# Team Ranking
Suppose there is a league of sports teams who play each other. We want to be able to rank them from best to worst.

Rather than looking at their win/loss records, we would like to instead base our rankings on margins of victory, as this will give us less ambiguous results.
> The general idea we will use was developed by Kenneth Massey, in his undergraduate thesis.

> [!Example]+ Example: Looking at Margins of Victory
> Consider 3 teams T1, T2, T3
> 1. T1 beats T2
> 2. T2 beats T3
> 3. T3 beats T1
> 
> In this case, we can't really say which team is best, as the situation is completely symmetric! But if we instead had
> 1. T1 beats T2 by 10 points
> 2. T2 beats T3 by 2 points
> 3. T3 beats T1 by 1 point
> 
> Then we have more information, and we can say as T1 completely crushed T2 and barely lost to T3, T1 seems to be the best!

The idea is to somehow assign each team a value, say $r_i$ (for team $i$), such that **if team $i$ plays team $j$, then the expected margin of victory (or defeat) for team $i$ is given by the difference $r_i - r_j$.**

> [!Example]+ Example: From Massey's Thesis
> Suppose we have 4 teams:
> 1. (T1) The Beast Squares
> 2. (T2) The Gaussian Eliminators
> 3. (T3) The Likelihood Loggers
> 4. (T4) The Linear Regressors
> 
> Now suppose that T1 beats T2 by 4, T1 beats T4 by 2, T2 beats T3 by 1, T2 loses to T4 by 7, and T3 ties with T4. The idea is that we want to find each team a $r_i$ value where
> $$
> \begin{align*}
> &r_1 - r_2 = 4 &r_1 - r_4 = 2 \\
> &r_2 - r_3 = 1 &r_2 - r_4 = -7 \\
> &r_3 - r_4 = 0
> \end{align*}
> $$
> 
> This gives us a linear system, where we can solve for $r_1, r_2, r_3, r_4$! Generally these systems are inconsistent, but we can still find the best $r_i$'s using **least squares**!
> $$
> \begin{bmatrix}
> 1 & -1 & 0 & 0 \\
> 0 & 1 & -1 & 0 \\
> 0 & 0 & 1 & -1 \\
> 1 & 0 & 0 & -1 \\
> 0 & 1 & 0 & -1
> \end{bmatrix}
> \begin{bmatrix}
> r_1 \\ r_2 \\ r_3 \\ r_4
> \end{bmatrix}
> =
> \begin{bmatrix}
> 4 \\ 2 \\ 1 \\ -7 \\ 0
> \end{bmatrix}
> $$
> 
> One issue that happens is when we take $A^T A$, we don't get an invertible matrix (as there are infinite solutions)! So, we can't simply find $r = (A^T A)^{-1} A^T b$. 
>
> Instead, let's just row reduce and find all solutions $r$ can possibly take on! Here, we find our solution as
> $$
> \begin{bmatrix} 
> 1.125 \\ -3.75 \\ -2.375 \\ 0
> \end{bmatrix} 
> + r_4
> \begin{bmatrix} 
> 1 \\ 1 \\ 1 \\ 1
> \end{bmatrix} 
> $$
> We find that $r_1 > r_4 > r_3 > r_2$, no matter what $r_4$ we choose! This is our team order. 
> > Note that we can also use this to predict matches, even if they didn't occur! For example, $r_1 - r_3 = 3.5$, so we can predict that team 1 would beat team 3 by 3.5 points!

To remove the (infinite) choices of free variables that we have as solutions, we can impose the constraint that $r_1 + r_2 + r_3 + r_4 = 0$ (force the average to be 0) and add that as an additional requirement to our initial linear system. 

One can prove that with this new requirement, we get a unique least squares solution, and moreover, this solution satisfies this "normalization condition".
