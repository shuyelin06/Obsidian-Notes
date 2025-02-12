---
title: CMSC427
tags:
- cmsc427
---

This is Introduction to Computer Graphics! This course discusses how we can synthesize artificial images from scratch.

- Modeling
- Rendering
- Interaction

# 2D Geometries
## Curves / Lines
Say we want to draw a line on the screen between points $P_0 = (x_0, y_0), P_1 = (x_1, y_1)$. Say the only function we have available to us is a function `putPixel(x,y)`, which draws a pixel at screen coordinates $(x,y)$.

How do we draw this line on the screen?

> [!Warning]
> One way we could do this is by modeling a line as the equation $y = mx + b$, but this fails on certain edge cases! 
> 
> ```python
> for x0 to x1
>    y = m * x + b
>    putPixel(x,y)
> ```
> 
> For example, what if the line is vertical ($m = \infty$)?

Instead, let's model the line using an extra free variable, so that $x$ and $y$ are not dependent on each other.

$$
\begin{align*}
x &= t * (x_1 - x_0) + x_0 \\
y &= t * (y_1 - y_0) + y_0 \\
&0 \le t \le 1
\end{align*}
$$

This is known as the **parametric equation** for the line!

```python
for t = 0 to 1
    x = t * (x1 - x0) + x0 
    y = t * (y1 - y0) + y0
    putPixel(x,y)
```

> [!Info] Parametric Curves
> This not only avoids the previous issues, but also gives us a convenient way to extend this definition!
> - With our current definition from $t \in [0,1]$, we have a line segment.
> - If we extend this to $t \in [0, \infty)$, we'll get a ray starting at $P_0$!
> - If we extend this to $t \in (-\infty, \infty)$, we'll get a line!
> 
> Furthermore, we can modify how $t$ varies in its domain to change where we're sampling the line.
> > If the line definition uses $t^2$, then we'll have more samples closer to $0$!

In fact one curve has multiple different forms that we may use throughout the program.
- Implicit Equation: $f(x,y) = 0$
- Parametric Equation: $x = f_x (t), y = f_y (t)$
- Functional Equation: $y = f(x)$

These are different equations that may be used to model a curve. 
> The parametric equation is commonly used for rendering.

> [!Example] Example: Equation for a Circle
> Note the implicit equation for a circle.
> $$
> x^2 + y^2 = R^2
> $$
> 
> The following parametric equation gives us a circle.
> $$
> x = R \cos(t) \qquad y = R \sin(t) \qquad 0 \le t \le 2 \pi
> $$
>
> Modifying simple equations like these can give us a lot of different shapes! For example:
> - Having unequal $R$ between x and y can create an ellipse
> - Modifying the equations can give you what's known as a "super-ellipse" 


## Points, Polylines, Polygons
In theory, all of our curves are smooth! However, in practice, we need to represent them as piece-wise discrete approximations. 

We define the following: 
- A **point** is a vertex in space.
- A **polyline** is a continuous sequence of line segments
- A **polygon** is a closed sequence of line segments. 

For polygons, we have the following definitions.
- **Simple polygons** have no self-intersections and duplicate points. If this is not true, the polygon is **non-simple**. 
- **Convex polygons** are polygons where any two points in the polygon can be connected by an inside line. Otherwise, they are **concave**.

How do we know if a point is inside of a polygon?
1. We could do a **half-face test**, where for a convex polygon, we take a cross product to see if the point is on the same side of every edge.
2. We could do a **line intersection test**, where we radially cast a line outwards, and check the number of times we intersect the edge. If the number of intersections is even, we are outside of the polygon.

> This is one of many problems you can have with polygons. Some examples include polygon triangulation, polygon collision, and rasterization.

In graphics, we commonly use **triangles**.
- Triangles are the easiest polygon to rasterize
- Triangles are guaranteed to be planar

> [!Info] Polygon Triangulation: Ear Cutting
> To triangulate a polygon, we can use the **ear cutting algorithm**. This is based off the idea of "ears", which are vertices which are locally convex.
>
> For each ear, cut it off as a triangle. Repeat this algorithm until the polygon has fully been triangulated.

So far, we know how to take a parametric curve and generate a polyline approximation of it. But what about the converse? How do we take a polyline and generate a parametric curve from it?
> We can use this to generate smooth surfaces for more realism.

### Rendering Polylines
...


---


> [!Example] 
> We have implicit equation
> $$
> \left( \frac{x}{a} \right)^2 - \left( \frac{y}{b} \right)^2 = 1
> $$
> 
> And parametric equation
> $$
> x(t) = a \sec{t} \qquad y(t) = b \tan{t}
> $$
> 
> Verify that these equations satisfy the implicit equation.
> 
> We can do this by plugging in $x,y$ into our implicit equation and seeing if the expression holds!
> $$
> \left( \frac{a \sec{t}}{a} \right)^2 - \left( \frac{b \tan{t}}{b} \right)^2 = \sec^2 (t) - \tan^2 (t) = 1
> $$
> > Here, we can use trig identities to see if the expression is true!


---

# WebGL
Many of the principles in WebGL can be applied to other Graphics APIs!

## Primitives
To draw in WebGL, we do not have functions like `drawVertex()` that would draw vertex by vertex-- that would be too inefficient!

Instead, WebGL has **primitive types**, where we can submit batches of vertices together that form primitives. 
- `gl_POINTS`: A set of points in space
- `gl_LINES`: A set of lines, where every two vertices form their own line
- `gl_LINE_STRIP`: A set of lines, where every vertex is connected to the one before and after it.
- `gl_LINE_LOOP`: A line strip, but with the very first and last vertex also connected.
- `gl_TRIANGLES`: A set of triangles, where every 3 vertices form a triangle.
- `gl_TRIANGLE_STRIP`: A set of triangles, where every vertex forms a triangle with the last 2.
  > Every other triangle, the triangle is read in the opposite winding direction to keep everything consistent. 
- `gl_TRIANGLE_FAN`: A set of triangles, where every two vertices after the first form a triangle with the first.

For triangles, **the order of the points define a winding direction**. Depending on how you see the triangle in 3D space, it either has a clockwise or counter-clockwise order!
> By default, OpenGL defines counter-clockwise winding as the front of the triangle.

## (Basic) Drawing Loop
THe drawing loop in OpenGL is as follows:
1. Load points into a buffer, which are sent to the GPU
   - Consists of creating a buffer, loading points into it, and binding it to the rendering pipeline.
2. Submit a command to the GPU to draw the shape, using what we've bound to the pipeline
3. 

---

# Geometry
A **point** is a position in space, denoted $(x,y)$. A **vector** is a displacement in space, denoted $\langle x,y \rangle$.
