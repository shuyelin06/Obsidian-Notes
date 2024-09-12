---
title: MATH401
tags:
- math401
---

This course, Applications in Linear Algebra, describes various ways we can


- Leontief Input-Output Model
- Applications to Computer Graphics
- Least Squares and Curve Fitting
- Team Ranking
- Linear Discrete Dynamical systems
- Markov Chains
- Google Pagerank Algorithm
- Heat Diffusion and Systems of Linear Differential Equations
- Matrix Exponentials and Rotations
- ..
- ..

---

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

# Leontief Input-Output Model
Suppose we have an economy, divided into sectors $A,B,C$, and each sector produces a product. For a sector to produce its product, it could consume some of its own product as well as some of the products produced by the other sectors. 

For example, let $A, B, C$ be our products. Suppose that
- To produce 1 unit of product $A$, we need 0.2 units of $A$, 0.15 units of $B$, and 0.1 units of product $C$.
- To produce 1 unit of product $B$, we need 0.25 units of $A$, and 0.05 units of $B$.
- To produce 1 unit of product $C$, we need 0.2 units of $B$, and 0.1 units of $C$.

> Assume that all units are on the same scale, presented in monetary value (making the unit standardized across all products).

For each product, we can create a **consumption vector**, representing what it takes to produce that product.
$$
A : \begin{bmatrix}
0.2 \\ 0.15 \\ 0.1
\end{bmatrix}
\quad
B : \begin{bmatrix}
0.25 \\ 0.05 \\ 0
\end{bmatrix}
\quad
C : \begin{bmatrix}
0 \\ 0.2 \\ 0.1
\end{bmatrix}
$$
We can use these vectors to determine the cost of producing each product! For example, if we wanted to produce $p_A, p_B, p_C$ units of $A,B,C$ (respectively), we can find our cost as
$$
p_A \begin{bmatrix}
0.2 \\ 0.15 \\ 0.1
\end{bmatrix}
+ p_B \begin{bmatrix}
0.25 \\ 0.05 \\ 0
\end{bmatrix}
+ p_C \begin{bmatrix}
0 \\ 0.2 \\ 0.1
\end{bmatrix}
= 
\begin{bmatrix}
0.2 & 0.25 & 0 \\
0.15 & 0.05 & 0.2 \\
0.1 & 0 & 0.1 
\end{bmatrix} 
\begin{bmatrix}
p_A \\ p_B \\ p_C
\end{bmatrix}
= M \vec{p}
$$

This gives us a matrix vector product, where $\vec{p}$ contains the amounts produced, $M$ is called the **consumption matrix**, and $M \vec{p}$ is called the **internal demand** (amounts of products that are consumed).

Now say we have some demand outside of our economy for these products, say $d_A = 50$ units of $A$, $d_B = 80$ units of $B$, and $d_C = 100$ units of $C$. How much of each product do we need to produce?

Because each product uses the other products, we can't just supply exactly $d_A, d_B, d_C$. We need to supply more to be used internally as input elsewhere in the economy! This motivates the **Leontief Input-Output Model**, stating that for any product, it's amount produced is equal to the sum of its **internal** and **external demand**.
$$
\text{Amount Produced} = \text{Internal Demand} + \text{External Demand}
$$
In mathematical terms,
$$
\vec{p} = M \vec{p} + \vec{d}
$$
So given our consumption matrix $M$ and external demand $\vec{d}$, we ask: what must we set $\vec{p}$ to so that we can satisfy the external demand?

We can solve this equation for $\vec{p}$ as so.
$$
\begin{align*}
\vec{p} &= M \vec{p} + \vec{d} \\
\vec{p} - M \vec{p} &= \vec{d} \\
(I - M) \vec{p} &= \vec{d}
\end{align*}
$$

This gives us a linear system that we can solve!

So, in our example, we can solve to find our production amounts
$$
\vec{p} = \left(
I - \begin{bmatrix}
0.2 & 0.25 & 0 \\
0.15 & 0.05 & 0.2 \\
0.1 & 0 & 0.1 
\end{bmatrix} 
\right)^{-1}
\begin{bmatrix}
50 \\ 80 \\ 100
\end{bmatrix} \approx
\begin{bmatrix}
101.89 \\ 126.07 \\ 122.43
\end{bmatrix}
$$
101.89 of $A$, 126.07 of $B$, and 122.43 of $C$.
> Note that our solution requires that $(I - M)$ is invertible. While it may not always be, "reasonable" conditions in economies typically imply that $I - M$ would be invertible.

> [!Info] Conceptually Interpreting $(I - M)^{-1}$
> Note that each column of $(I - M)^{-1}$ gives us the **increase** tells us the amount of extra production needed for each product! For example, if we wanted to produce $(1,0,0)$ of products, we can find it as $\vec{p} = (I - M)^{-1} (1,0,0)^T$, which is just the first column!
>
> In more mathematical terms, the $j^{th}$ colum of $(I - M)^{-1}$ contains the additional production required to satisfy an additional unit of external demand for product $j$.

Given this interpretation, it should make sense that:
- The diagonal entries of $(I - M)^{-1}$ are $\ge 1$. 
- The entries of $(I - M)^{-1}$ should be non-negative.

But is there a mathematical explanation for this? Under certain conditions of $M$, it is true that
$$
(I - M)^{-1} = I + M + M^2 + M^3 + \dots
$$
First, we observe that all terms on the right-hand side should have non-negative entries (as $M$ has all non-negative entries- we cannot consume negative products)! Furthermore, as $I$ has 1's down the diagonal, this means that our inverse must have values $\ge 1$, as we are only adding positive numbers to 1!

These conditions are $M$ are as follows. We define a **column sum** of a matrix to be the sum of the entires in any given column of the matrix. Any matrix $M$ with column sums $<1$ satisfy the above condition, and in fact, any "reasonable" economy is one where each column sum is $<1$.
> Otherwise, it would take more than one unit to produce a unit of a product, which is not economically feasible!

> [!Abstract] Theorem: Economically Feasible Consumption Matrices
> Suppose that $M$ is $n \times n$ with non-negative entries and suppose every column sum of $M$ is less than 1.
>
> Then,
> - $(I - M)^{-1} = 1 + M + M^2 + M^3 + \dots$
> - In particular, $(I - M)^{-1}$ exists and has non-negative entries.
> - Given an external demand $\vec{d}$ with non-negative entries, then we have a unique solution $\vec{p} = (I - M)^{-1} \vec{d}$ and furthermore, $\vec{p}$ has non-negative entries too.

> [!Example]- Example: A Nonsensical Economy
> Suppose we have consumption matrix
> $$
> M = 
> \begin{bmatrix}
> 0.6 & 0.7 \\ 
> 0.5 & 0.5 \\
> \end{bmatrix}
> $$
> 
> and we want to satisfy some external demand $\vec{d}$. In this example,
> $$
> (I - M)^{-1} = 
> \begin{bmatrix}
> -3.33 & -4.66 \\
> -3.33 & -2.66
> \end{bmatrix}
> $$
> 
> It's not feasible to satisfy $\vec{d}$, and this is because of the column sums!


# Applications of Computer Graphics
Here, we're going to work with points in $2D$/$3D$, and focus on how we can move these points in space. For example, how can we rotate points in space? Translate them? 
> Hint: This can be accomplished through matrix multiplication!

We'll start by treating points in $2D$/$3D$ as either $2 \times 1$ / $3 \times 1$ vectors $\vec{p}$. We can represent collections of them, called **pictures**, as a $n \times k$ matrix
$$
[ \vec{p}_1, \vec{p}_2, \vec{p}_3, \dots \vec{p}_k ]
$$
We'll also treat "movements" in space as a matrix $M$, such that we can transform points by taking $M \vec{p}$. We can also apply this movement to an entire picture by multiplying
$$
M [ \vec{p}_1, \vec{p}_2, \vec{p}_3, \dots \vec{p}_k ]
$$

## 2D Graphics
A **linear transformation** is a function $f : \mathbb{R}^n \to \mathbb{R}^m$ such that
1. $\forall \vec{u}, \vec{v} \in \mathbb{R}^n$, $f(\vec{u} + \vec{v}) = f(\vec{u}) + f(\vec{v})$
2. For $\vec{u} \in \mathbb{R}^n, c \in \mathbb{R}$, $f(c \vec{u}) = c f(\vec{u})$

If $A$ is any $m \times n$ matrix, then we can use it to define a linear transformation function $f(\vec{x}) = A \vec{x}$. And in fact, every linear transformation $f: \mathbb{R}^n \to \mathbb{R}^m$ has a corresponding matrix form.

> [!Abstract] Theorem: Matrices of Linear Transformations
> If $f : \mathbb{R}^n \to \mathbb{R}^m$ is a linear transformation, then there is a $m \times n$ matrix $A$ such that $f(\vec{x}) = A \vec{x}$ for all $\vec{x}$.
>
> To find it, we can find $A$ column by column as so:
> $$
> A = 
> \begin{bmatrix}
> f(\vec{e}_1) & f(\vec{e}_2) & \dots &f(\vec{e}_n)
> \end{bmatrix} 
> $$
> Where $\vec{e}_i$ is the standard basis vector for $i$, the vector with 1 in the $i^{th}$ component and 0's everywhere else.

> [!Example]+ Example: Matrices of Linear Transformations (1)
> Counterclockwise rotation about the origin by $\pi / 2$ degrees in $\mathbb{R}^2$ is a linear transformation $f : \mathbb{R}^2 \to \mathbb{R}^2$.
> 
> We can find its standard matrix column by column:
> $$
> \begin{align*}
> e_1 = (1,0) &\to (0,1) \\
> e_2 = (0,1) &\to (-1,0)
> \end{align*}
> $$
> This gives us matrix
> $$
> \begin{bmatrix}
> 0 & -1 \\
> 1 & 0
> \end{bmatrix}
> $$

Note that we can also combine common linear transformations to build more complex transformations! Consider the following example. 
> Note that what combining matrices by multiplying them, we should multiply right to left in order of the operation we want to perform first!

> [!Example] Example: Compositions of Linear Transformations
> Find the matrix for reflection through the $x$-axis.
> $$
> A = 
> \begin{bmatrix}
>     f(\vec{e}_1) & f(\vec{e}_2) 
> \end{bmatrix}
> = 
> \begin{bmatrix}
>     1 & 0 \\
>     0 & -1
> \end{bmatrix}
> $$
>
> What about reflection through the line $L_\theta$ that makes an angle of $\theta$ with the positive $x$-axis? 
> 
> Instead of doing heavy math, we can actually just combine linear transformations! Let's first rotate to the origin, then reflect, then rotate back!
> 1. Rotate by $-\theta$ radians
> 2. Reflect across the $x$-axis
> 3. Rotate by $\theta$ radians
> 
> Finding and multiplying the matrices for these steps will give us our final transformation!


Below, we can find some common linear transformations in $\mathbb{R}^2$.
- Say we wanted to perform a CCW rotation about the origin by $\theta$ radians. Our transformation matrix is
  $$
  \begin{bmatrix}
  \cos \theta & -\sin(\theta) \\
  \sin \theta & \cos(\theta)
  \end{bmatrix}
  $$
- Say we wanted to reflect a line across the $x$-axis. Then, we have transformation matrix
  $$
  \begin{bmatrix}
  1 & 0 \\
  0 & -1
  \end{bmatrix}
  $$
- Say we wanted to translate a point, or in other words, shift it by a fixed amount. Such a translation is not possible with a $2 \times 2$ matrix, but it is with a $3 \times 3$ matrix!

  We can represent our vectors in **homogeneous coordinates**, where we add an extra 1 component. So for any 2-dimensional vector, we consider them to be $(x,y,1)$, and can form a translation matrix as follows:
  $$
  \begin{bmatrix}
  1 & 0 & t_x \\
  0 & 1 & t_y \\
  0 & 0 & 1
  \end{bmatrix}
  $$
  
> [!Info] Compositions of Transformations with Translation
> Note that to combine translations with other transformations in $\mathbb{R}^2$, we need to convert our $2 \times 2$ transformations to a corresponding $3 \times 3$ matrix in homogeneous coordinates! We can do this by adding a 1 in the bottom-right diagonal, all others 0. 
>
> So for example, a rotation compatible with translations is
> $$
> \begin{bmatrix}
> \cos \theta & -\sin(\theta) \\
> \sin \theta & \cos(\theta)
> \end{bmatrix} \Longrightarrow
> \begin{bmatrix}
> \cos \theta & -\sin(\theta) & 0 \\
> \sin \theta & \cos(\theta) & 0  \\
> 0 & 0 & 1
> \end{bmatrix}
> $$

> [!Example]+ Example: Compositions of Linear Transformations (2)
> Suppose we want to do a CCW rotation about the point $(5,7)$ by some angle $\pi / 3$. Find a matrix for this operation.
>
> We can find the matrix as follows:
> 1. Translate by $(-5,-7)$
> 2. Rotate about the origin by $\theta$
> 3. Translate by $(5,7)$
> 
> We find this as
> $$
> \begin{bmatrix}
>   1 & 0 & 5 \\
>   0 & 1 & 7 \\
>   0 & 0 & 1
>   \end{bmatrix}
> \begin{bmatrix}
>   \cos \frac{\pi}{3} & -\sin \frac{\pi}{3} & 0 \\
>   \sin \frac{\pi}{3} & \cos \frac{\pi}{3} & 0  \\
>   0 & 0 & 1
>   \end{bmatrix}
> \begin{bmatrix}
>   1 & 0 & -5 \\
>   0 & 1 & -7 \\
>   0 & 0 & 1
>   \end{bmatrix}
> $$
> If we wanted to apply this to a point $(x,y)$, we would convert this to homogenoeus coordinates $(x,y,1)$, then take the product! 

## 3D Graphics
Like in the 2D case, we will represent the 3D point $(x,y,z)$ in homogeneous coordinates $(x,y,z,1)$.

---

**Translations** can be done by multiplying the $4 \times 4$ matrix
$$
\begin{bmatrix}
1 & 0 & 0 & t_x \\
0 & 1 & 0 & t_y \\
0 & 0 & 1 & t_z \\ 
0 & 0 & 0 & 1
\end{bmatrix}
$$

---

**Rotations** in 3D are considerably more complex than that of the 2D case. Rotations in 3D have an **axis (line)** and an **angle**. All points are rotated around this axis such that the orthogonal vector from the line to the point, and the orthogonal vector from the line to the new point, form the angle given.

If the axis goes through the origin, then the rotation is a linear transformation $f : \mathbb{R}^3 \to \mathbb{R}^3$ and can be given by a $3 \times 3$ matrix.

> [!Example]- Example: Z-Axis Rotation in 3D
> Consider the rotation around the $z$-axis by $\theta$ radians.
> 
> We can find the standard matrix by transformating the standard basis vectors.
> > It's important to realize that our rotation is actually a rotation in the $xy$ plane! The z-coordinate does not change.
> $$
> f\left( \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} \right) 
> = \begin{bmatrix} \cos(\theta) \\ \sin{\theta} \\ 0 \end{bmatrix}
> \quad
> f\left( \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix} \right) 
> = \begin{bmatrix} -\sin(\theta) \\ \cos{\theta} \\ 0 \end{bmatrix}
> \quad
> f\left( \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix} \right) 
> = \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}
> $$
> 
> This gives us standard matrix
> $$
> A = 
> \begin{bmatrix}
> \cos(\theta) & -\sin(\theta) & 0 \\
> \sin(\theta) & \cos(\theta) & 0 \\
> 0 & 0 & 1
> \end{bmatrix}
> $$
> 
> For homogeneous coordinates, we have
> $$
> A = 
> \begin{bmatrix}
> \cos(\theta) & -\sin(\theta) & 0 & 0 \\
> \sin(\theta) & \cos(\theta) & 0 & 0 \\
> 0 & 0 & 1 & 0 \\
> 0 & 0 & 0 & 1
> \end{bmatrix}
> $$

When we specify an axis of rotation, we'll also specify a direction on that axis indicating how we should rotate about that axis. Then, we will follow the **right hand rule** convention for rotations.

In this convention, we place our thumb in the direction of the axis, and the way our fingers curl defines the orientation of the rotation.

We have the following rotations about the standard axes:
$$
RX(\theta) = 
\begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & \cos(\theta) & -\sin(\theta) & 0 \\
0 & \sin(\theta) & \cos(\theta) & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\qquad
RY(\theta) =
\begin{bmatrix}
\cos(\theta) & 0 & \sin(\theta) & 0 \\
0 & 1 & 0 & 0 \\
-\sin(\theta) & 0 & \cos(\theta) & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
$$
$$
RZ(\theta) =
\begin{bmatrix}
\cos(\theta) & -\sin(\theta) & 0 & 0 \\
\sin(\theta) & \cos(\theta) & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
$$

But what if we want to rotate about an axis that is not one of the standard axes? Well, we could combine rotations to obtain a rotation which is "effectively" a rotation about this axis! 

---

Like in the 2D case, we can combine our transformations to obtain more complex transformations!

> [!Example]+ Example: Compositions of Transformations
> Suppose we want to rotate about the line through $(0,4,3)$ that is parallel to the $x$-axis (with same orientation) by an angle of $\frac{\pi}{6}$.
> 
> We can find our standard matrix by first translating to the origin, rotating about $x$, then translating back to our point!
> $$
> A = 
> \begin{bmatrix}
> 1 & 0 & 0 & 0 \\
> 0 & 1 & 0 & 4 \\
> 0 & 0 & 1 & 3 \\ 
> 0 & 0 & 0 & 1
> \end{bmatrix}
> \begin{bmatrix}
> 1 & 0 & 0 & 0 \\
> 0 & \cos(\pi/6) & -\sin(\pi/6) & 0 \\
> 0 & \sin(\pi/6) & \cos(\pi/6) & 0 \\
> 0 & 0 & 0 & 1
> \end{bmatrix}
> \begin{bmatrix}
> 1 & 0 & 0 & 0 \\
> 0 & 1 & 0 & -4 \\
> 0 & 0 & 1 & -3 \\ 
> 0 & 0 & 0 & 1
> \end{bmatrix}
> $$



## Perspective Projection in 3D
In a 3D scene, how can we render it to a 2D image?

We could simply project these points onto a "viewing" plane, but this will give us a very flat image, which fails to give us a sense of depth!

In fact, this happens because our eyes have depth cues that simple projection doesn't preserve. These include:
- Objects that are further are smaller
- Parallel lines converge at the horizon 

This is where **perspective projection** comes in! Given our view, this projection transforms points so that points further away appear closer in nature!

Consider a view at $(0,0,d)$ which is looking down at the $xy$ plane. Then, for any $(x,y,z)$ point, we want to find its projection on the plane $(x',y',0)$, where the projection is co-linear with our viewing point and input point.

We can find this as the point on the plane intersecting the line $(x,y,z-d)$ starting at $(0,0,d)$
$$
(0,0,d) + t(x,y,z-d) = (tx,ty,d + t(z-d)) \qquad t \in \mathbb{R}
$$
We wish to find the point such that $z = 0$, so we solve such that 
$$
d + t(z-d) = 0 \Longrightarrow t = \frac{d}{d-z} = \frac{1}{1 - z/d}
$$
This gives us the transformed point in perspective projection! 
$$
x' = \frac{x}{1 - z/d} \qquad y' = \frac{y}{1 - z/d}
$$
Now, how do we express this in matrix form?

If we use homogeneous coordinates $(x,y,z,d)$, where $d$ influences our perspective projection, we can express this in the form

--- WIP ---

$$
\begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 0 \\
0 & 0 & -\frac{1}{d} & 1
\end{bmatrix}
$$
After, divide every point by the 4th entry to fix the x and y coordinates.
