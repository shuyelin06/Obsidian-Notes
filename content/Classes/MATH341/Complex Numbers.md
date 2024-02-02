---
title: Complex Numbers
tags:
- math341
---

Complex numbers are defined in the form
$$
\mathbb{C} = \{ a + bi \; | \; a,b \in \mathbb{R} \}
$$
Where $i^2 = -1$. This form is known as the **standard form**.
> We define $\mathbb{C}$ to denote all complex numbers. 

We say $a$ and $b$ are the real and imaginary parts of the complex number, respectively.
$$
Re(z) = a \qquad Im(z) = b
$$

# Properties of Complex Numbers
## Sums and Products
Let $z = a + bi$, $w = c + di$, $z,w \in \mathbb{C}$. Then,
- The **sum** of $z$ and $w$ is
  $$
  z + w = (a + c) + (b + d) i
  $$

- The **product** of $z$ and $w$ is
  $$
  z \cdot w = (ac - bd) + i (ad + bc)
  $$

## Complex Conjugates and Norm
Let $z = a + bi$ be a complex number.

We define it's **complex conjugate**, $\bar{z} = z - bi$, which is the complex number whose product with $z$ yields a non-negative real number.
$$
z \cdot \bar{z} = a^2 + b^2
$$

Complex conjugates have the following two properties:
- **Sum of Conjugates**: $\overline{z + w} = \bar{z} + \bar{w}$
- **Product of Conjugates**: $\overline{z \cdot w} = \bar{z} \cdot \bar{w}$

The **norm** of complex number $z$ is defined as
$$
|z| = \sqrt{a^2 + b^2} = \sqrt{z \cdot \bar{z} }
$$

# Geometry of Complex Numbers
Complex numbers can be plotted on a plane known as the **complex plane**. This is a plane where the horizontal axis consists of all real numbers ($1,2,\dots$) and the vertical axis consists of all complex numbers ($i, 2i, \dots$).

### Geometric Representation
Let $z = a + bi$ be a complex number on the plane. Then, if $\theta$ is the angle between $z$ and the horizontal axis,
$$
z = a + bi = |z| \cos(\theta) + |z| i \sin(\theta) = |z| (\cos(\theta) + i \sin(\theta))
$$

>[!Abstract] Theorem: Complex Exponential 
> For every $\theta \in \mathbb{R}$, we have
> $$
> e^{i \theta} = \cos(\theta) + i \sin(\theta)
> $$
> > We can use this to find $\sin(\theta)$ and $\cos(\theta)$ as
> > $$
> > \sin(\theta) = \frac{e^{i\theta} - e^{-i\theta}}{2i} \qquad \cos(\theta) = \frac{e^{i\theta} + e^{-i\theta}}{2}
> > $$

Using this theorem, we can represent all complex numbers in the polar form
$$
z = r \cdot e^{i \theta} \qquad 0 \le \theta \le 2 \pi \qquad r \in \mathbb{R}
$$

>[!Abstract] Theorem: Properties of Complex Geometries
> Let $x$ and $y$ be two real numbers and $n$ be an integer. Then,
> 1. $e^{ix} e^{xy} = e^{i (x + y ) }$
> 2. **De Moivre's Formula**: $(e^{ix})^n = e^{inx}$

> [!Example]- Example: Applying Complex Geometric Properties
> Evaluate
> $$
> \int e^x \cos(x) \; dx
> $$
> We observe that $\cos(x)$ is equivalent to the real part of the equation $e^{ix}$, so we can rewrite the answer as the **real part** of the equation
> $$
> \int e^x \cdot e^{ix} \; dx = \int e^{(1 + i)x} \; dx = \frac{1}{1 + i} e^{(1 + i)x}
> $$
> 
> We can then convert and solve for the real part of the equation.