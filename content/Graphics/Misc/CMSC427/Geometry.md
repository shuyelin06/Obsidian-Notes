---
title: Geometry
tags:
- cmsc427
---

# Parametric Curves
## Definition
A **parametric curve** is a vector-valued function of one variable $t$. Given $t$, we compute a 3D point $(x(t), y(t), z(t))$, and as we vary $t$, we "move" the point along the curve.
> The **tangent** of the curve is $(x'(t), y'(t), z'(t))$, and corresponds to the "speed" at a given point.

Parametric curves find a lot of applications, including:
- Animation: Curves provide a "track" for objects to move along
- Surfaces: Curves can be used to create surfaces, through a variety of techniques (extrusion, sweeping, etc)

It's infeasible to create these curves by specifying every point along the curve. This requires too much data, and is too hard to work with.

Instead, what we will do is specify curves using a small number of **control points**. These will influence how the curve will look.

## Hermite Curves
### Hermite Basis Matrix
A **Hermite Curve** is a cubic curve in the form
$$
\begin{align*}
x(t) = at^3 + bt^2 + ct + d \\
y(t) = et^3 + ft^2 + gt + h \\
z(t) = it^3 + jt^2 + kt + l
\end{align*}
$$
Which interpolates between the end points $P0, P1$, while matching the tangents at endpoints $T0, T1$. 

For any given dimension, we solve for the curve's parameter by taking system of equations $MA = G$, where 
- $M$ is the equation matrix
- $A$ is the parameter vector
- $G$ is the geometry vector
$$
\begin{bmatrix}
0 & 0 & 0 & 1 \\
1 & 1 & 1 & 1 \\
0 & 0 & 1 & 0 \\
3 & 2 & 1 & 0
\end{bmatrix}
\begin{bmatrix}
a \\ b \\ c \\ d
\end{bmatrix}
M A = G = 
\begin{bmatrix}
x_0 \\ x_1 \\ dx_0 \\ dx_1
\end{bmatrix}
$$
We can then take the inverse of $M$ to get the **Hermite basis matrix**, letting us find our parameters. 
$$
A = \begin{bmatrix}
a \\ b \\ c \\ d
\end{bmatrix} =
\begin{bmatrix}
2 & -2 & 1 & 1 \\
-3 & 3 & -2 & -1 \\
0 & 0 & 1 & 0 \\
1 & 0 & 0 & 0
\end{bmatrix}
\begin{bmatrix}
x_0 \\ x_1 \\ dx_0 \\ dx_1
\end{bmatrix} = M^{-1} G
$$

Consider an alternative definition of the Hermite equations, by interpreting them as blending functions that weigh between our geometry data. Taking our original Hermite equation,
$$
x(t) = (2x_0 - 2x_1 + dx_0 + dx_1) t^3 + (-3x_0 + 3x_1 - 2dx_0 - dx_1)t^2 + (dx_0)t + x_0
$$
We can group our data terms to get
$$
x(t) = (2t^3 - 3t^2 + 1)x_0 + (-2t^3 + 3t^2)x_1 + (t^3 - 2t^2 + t)dx_0 + (t^3 - t^2)dx_1
$$
Giving us blending functions
$$
\begin{align*}
h_{00} (t) = 2t^3 - 3t^2 + 1 \\
h_{01} (t) = -2t^3 + 3t^2 \\
h_{10} (t) = t^3 - 2t^2 + t \\
h_{11} (t) = t^3 - t^2
\end{align*}
$$
Which are 4 functions that blend between our data points, and sum to 1 for all $t$. At any $t$, each curve tells us how much that data point "contributes" to the final result.

The Hermite curve is the basis for most of the interpolating curves we work with, with some small modification

### Computing the Tangents
Oftentimes, we won't have the tangent data $T0, T1$. Instead, we'll have other points $x_{-1}, x_2$ we'll want to infer the tangents from. If $dx_0 = x_0 - x_{-1}, dx_1 = x_2 - x_1$, then can find that
$$
G = 
\begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
1 & 0 & -1 & 0 \\
0 & -1 & 0 & 1
\end{bmatrix} 
\begin{bmatrix}
x_0 \\ x_1 \\ x_{-1} \\ x_2
\end{bmatrix} 
$$

We can insert this into our original equation to find the Hermite curve given 4 points (where 2 are used to define the tangents)
$$
A = 
\begin{bmatrix}
2 & -2 & 1 & 1 \\
-3 & 3 & -2 & -1 \\
0 & 0 & 1 & 0 \\
1 & 0 & 0 & 0
\end{bmatrix}
\begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
1 & 0 & -1 & 0 \\
0 & -1 & 0 & 1
\end{bmatrix} 
$$

### Catmull-Rom Splines
If we build a Hermite curve from a polyline, we can get a problem from mismatched derivatives, as for any given point, the tangents on either side will not match. 

**Catmull-Rom Splines** fix this issue by defining the tangent at any point as the difference between the adjacent points. To compute tangents, Catmull-Rom uses matrix
$$
G = 
\begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 1/2 & -1/2 & 0 \\
-1/2 & 0 & 0 & 1/2
\end{bmatrix} 
\begin{bmatrix}
x_0 \\ x_1 \\ x_{-1} \\ x_2
\end{bmatrix} 
$$
We then use this $G$ with our Hermite Basis matrix like before.

> The 1/2 is a weight that Catmull-Rom has traditionally used. Typically in general development, we'll replace 1/2 with $\alpha$, a tuning factor.

### Bezier Curves
**Bezier Curves** are another type of curve that are typically more flexible and intuitive, particularly for polylines. They also use Hermite curves, but define the points and normals differently.

For points $P0, P1, P2, P3$, Bezier Curves use the middle two points to define the tangents, and interpolate between the end points. In fact, the specific translation is:
$$
\begin{align*}
P0 = P0 \\
P1 = P3 \\
T0 = 3 * (P1 - P0) \\
T1 = 3 * (P3 - P2)
\end{align*}
$$

Intuitively, Bezier Curves are the result of a recursive series of linear interpolations. Given our control points $P0, P1, P2, P3$, we can find our interpolated point point as
$$
\begin{align*}
A = Lerp(P0,P1,t) \\
B = Lerp(P1,P2,t) \\
C = Lerp(P2,P3,t) \\
X = Lerp(A,B,t) \\
Y = Lerp(B,C,t) \\
P = Lerp(X,Y)
\end{align*}
$$

Known as **de Casteljau's Algorithm**, this recursive linear interpolation yields the same curve as our Bezier Curve. 

In fact, for $n$ points, if you substitute the linear interpolations in, you'll end with the **Bernstein Polynomials**.
$$
B_i^n (t) = \binom{n}{i} (1 - t)^{n-i} (t)^i
$$
> $n$ is the number of data points, and $i$ is the term of the polynomial.

We can convert the Bernstein Polynomials to an $n$ order Bezier Curve, by multiplying each polynomial by a corresponding data point.
$$
x(t) = \sum_{i=0}^n B_i^n (t) p_i
$$
> Often, we will regroup our terms into the groups of $t^i$, so we can write our computation in a matrix form. This makes things substantially faster.

Bezier Curves have a handful unique properties:
1. The Bezier Curve is a convex combination of the control points, meaning the curve is always inside the convex hull of control points.
   - This makes the curve predictable, and usable in fast intersection / culling tests.
2. If the curve is in a plane, no straight line intersects a Bezier curve more times than it intersects the curve's control polyline. In other words, the "curve is not more wiggly" than the control polyline.
3. Transforming the control points, or transforming the points on the curve yield the same transformed point.
4. Any Bezier curve can be subdivided into smaller Bezier Curves.

> [!Info] Drawing Bezier Curves
> Due to the nature of the curves, uniformly sampling and drawing from the curve can yield poor approximations of our curve.
>
> Instead, we will only use as many line segments as needed, using **adaptive sampling**. 
> 1. Use the De Casteljau construction to split the Bezier Segment in the middle
> 2. For each half, if it is "flat enough", draw the line segment. Otherwise, repeat (1).
>
> > We say the curve is "flat" enough if the hull is flat enough.

> To support Bezier curves with more points, we can use piecewise curves.

# Fractals
**Fractals** are a class of shapes that are characterized by some recursive structure. They are self-similar, meaning that different parts are similar to each other and the whole.

## Fractal Dimensionality
What makes fractals unique is their dimensionality. When we typically consider parametric surfaces, we can describe them with a finite number of variables.
- A curve can be described by 1 variable
- A surface can be described by 2 variables

However, we can't do this with fractals! Consider the **Koch Curve** below.
![[Graphics/CMSC427/Resources/FractalsE1.png]]

We can't just use one parameter $t$ to describe the curve, as it would take an infinite amount of length to get to any position. However, we also can't describe the curve with two variables $u,v$, as this includes points outside of the curve!

In fact, the dimension of the Koch Curve is $1.26186$ - somewhere between 1 and 2 dimensions. 

We can measure a fractal's dimension by measuring the dimension of the generator, with the following formula:
$$
D = \frac{\log N}{\log 1/s}
$$
- $N$ is the number of parts in the generator
- $S$ is the scale factor for one part (the length of one part divided by the total length of the generator).

> [!Example] Example: Measuring Fractal Dimensionality
> Consider the following fractal generator:
> 
> ![[Graphics/CMSC427/Resources/FractalsE2.png]]
>
> Let's measure the dimension of the resultant fractal. 
> - The fractal has $N = 6$ parts
> - The length of one part is $\sqrt{2}$, and the total length of the fractal is 4. So, our scale factor is $\frac{\sqrt{2}}{4}$.
>
> This gives us dimension
> $$
> D = \frac{\log 6}{\log 4 / \sqrt{2}} \approx 1.723
> $$

## Creating Fractals
### Iterated Function Systems
**Iterated Function Systems** create fractals by defining a finite set of mappings (transforms). To generate a fractal with these transforms, we:
1. Start with an arbitrary point
2. Repeatedly iterate and apply randomly selected transforms to find where the point will end up

By convention, we define a single IFS transform in row numbers of the form $a,b,c,d,e,f,p$, defining transform
$$
\lambda (x,y) = (ax + by + e, cx + dy + f)
$$
Using a combination of these transforms, we can create arbitrarily complex fractal shapes.
> $p$ represents the percentage of the fractal's area generated by the transform. It isn't required, but could let the fractal be drawn more efficiently if selected well.

> [!Example] Example: Koch Curve
> The IFS transform system for the Koch Curve is as follows:
> $$
> \begin{matrix}
> 0.3333 &  0.0000 &  0.0000 &  0.3333 &  0.0000 & 0.0000 &  0.25 \\
> 0.1667 & -0.2887 &  0.2887 &  0.1667 &  0.3333 & 0.0000 &  0.25 \\
> 0.1667 &  0.2887 & -0.2887 &  0.1667 &  0.5000 & 0.2887 &  0.25 \\
> 0.3333 &  0.0000 &  0.0000 &  0.3333 &  0.6667 & 0.0000 &  0.25
> \end{matrix}
> $$


### L-Systems
**L-Systems** create fractals by modeling shapes as a string of symbols. They have two parts:
1. A grammar for generating strings, where symbols have different meanings in drawing the shape
2. A rendering algorithm for interpreting strings as shapes

Typically, this grammar is defined by a set of symbols with meaning, and a set of replacement rules for different symbols.
> By defining a "grammar" and a set of rules for shapes, we can create an arbitrary number of shapes that look similar!

> [!Example] Example: L-System, Koch Curve
> The following is an L-system for a Koch Curve. Let $F$ be the initiator. Then, our replacement rule is:
> $$
> F \to F+F--F+F
> $$
> Where $+$ is a 60 degree CCW rotation, $-$ is a 60 degree CW rotation. Now, we replace $F$ as many times as we want in the rule to get our curve!

**Stochastic L-Systems** are systems where each rule is given a probability of occurring. This is often used for generating more natural shapes.

For example, we could have various replacements for symbol $F$, each with its own probability:
$$
\begin{align*}
F \to 0.33 \to F [+F] F [-F] F \\
F \to 0.33 \to F [+F] F \\
F \to 0.34 \to F [-F]
\end{align*}
$$

# Constructive Solid Geometry (CSG)
## Definitions
**Constructive Solid Geometry (CSG)** is an alternative method of generating shapes. One CSG scheme is defined by:
- Primitives: A basic set of primitive shapesa
- Set Operations: Given two shapes, applies an operation generating a new shape. 

> Some examples of set operations include union, intersection, and difference.
