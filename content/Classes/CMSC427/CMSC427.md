---
title: CMSC427
tags:
- cmsc427
---

This is Introduction to Computer Graphics! This course discusses how we can synthesize artificial images from scratch.

- Modeling
- Rendering
- Interaction

# Modeling
## Modeling Lines
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

```python
for t = 0 to 1
    x = t * (x1 - x0) + x0 
    y = t * (y1 - y0) + y0
    putPixel(x,y)
```

This not only avoids the previous issues, but also gives us a convenient way to extend this definition!
- With our current definition from $t \in [0,1]$, we have a line segment.
- If we extend this to $t \in [0, \infty)$, we'll get a ray starting at $P_0$!
- If we extend this to $t \in (-\infty, \infty)$, we'll get a line!

Furthermore, we can modify how $t$ varies in its domain to change where we're sampling the line.
> If the line definition uses $t^2$, then we'll have more samples closer to $0$!
