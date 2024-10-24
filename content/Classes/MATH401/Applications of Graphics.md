---
title: Applications of Graphics
tags:
- math401
---

# Applications of Computer Graphics
Here, we're going to work with points in $2D$/$3D$, and focus on how we can move these points in space. For example, how can we rotate points in space? Translate them? 
> Hint: This can be accomplished through matrix multiplication!

We'll start by treating points in $2D$/$3D$ as either $2 \times 1$ / $3 \times 1$ vectors $\vec{p}$. We can represent collections of them, called **pictures**, as a $n \times k$ matrix
$$fffff
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
x' = \frac{x}{1 - z/d} \qquad y' = \frac{y}{1 - z/d} \qquad z' = 0
$$
Now, how do we express this in matrix form?

The problem is, this is a nonlinear transformation!

However, interestingly enough, we can find the the linear transformation
$$
(x,y,z,1) \to (x,y,0,1 - \frac{z}{d})
$$
After which, if we divide by the $w$ coordinate, we'll obtain our perspective projection!

So, our perspective projection matrix is
$$
P = \begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 0 \\
0 & 0 & -\frac{1}{d} & 1
\end{bmatrix}
$$
Where for any $(x,y,z)$ point, we convert it to homogeneous coordinates $\vec{v} = (x,y,z,1)$, and after multiplying $P \vec{v}$, we divide all entries by the $w$ coordinate (sometimes called **post-processing**).
> Note that this matrix assumes that our view is at $(0,0,d)$ and is looking at the origin! If our view has a different orientation, we can shift it to the $z$-axis, and then change everything back!

> [!Example]+ Example: Perspective Projection
> Consider the cube with vertices $(\pm 3, \pm 3, \pm 3)$. Consider perspective projection from $(0,0,9)$.
> 
> Let's apply perspective projection on $(3,3,3)$.
> $$
> \begin{bmatrix}
> 1 & 0 & 0 & 0 \\
> 0 & 1 & 0 & 0 \\
> 0 & 0 & 0 & 0 \\
> 0 & 0 & -\frac{1}{9} & 1
> \end{bmatrix}
> \begin{bmatrix}
> 3 \\ 3 \\ 3 \\ 1
> \end{bmatrix} =
> \begin{bmatrix}
> 3 \\ 3 \\ 0 \\ \frac{2}{3}
> \end{bmatrix}
> \Longrightarrow
> \begin{bmatrix}
> 9/2 \\ 9/2 \\ 0 \\ 1
> \end{bmatrix}
> $$
> Our transformation was $(3,3,3) \to (\frac{9}{2}, \frac{9}{2}, 0)$!

