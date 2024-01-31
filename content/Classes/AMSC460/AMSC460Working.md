---
title: AMSC460Working
tags:
- amsc460
- wip
---

(Machine Numbers)

While performing any calculations, our computers will represent any real number $x \in \mathbb{R}$ using a **finite number of binary digits**. This yields a limited amount of possible numbers, which are commonly referred to as **machine numbers**.

Here, we discuss different representations of numbers, and the consequences of these representations with regard to error.

# Binary Machine Numbers
While we see numbers in (commonly) decimal form, this is not how machines see them! Below, we discuss how the most common representation of numbers in machines, and potential sources of error they can create. 

## IEEE Standard 754
The most common representation of numbers in machines is the **IEEE Standard 754**, the floating point representation of numbers.

Under this standard, a real number $x \in \mathbb{R}$ will be represented in the following format:

$$
x = (-1)^s 2^{e - \text{B}} (1.m) 
$$

- $s$ denotes the **sign** of the number, which determines whether $x$ is positive or negative.
- $m$ denotes the **mantissa**, which takes on some value between $0 \le m < 1$.
- $e$ denotes the **exponent (characteristic)**, which takes on some positive integer value.
- $B$ denotes the **bias**, which offsets the exponent value to allow for an (approximately) equivalent number of positive and negative powers of 2.

> Note that this standard essentially represents $x$ in the base-2 equivalent of the scientific notation we're used to.

In our machine, the number of bits allocated to represent each part of a number depends on the number of bits allocated for the number (bias is predetermined based off this allocation).

For our purposes, we will assume a 64 bit number, otherwise known as a `double`. Using this standard, a number $x$ would be represented as follows (let $s_i, b_i, d_i$ represent bits taking on 0 or 1):

| Sign ($s$) | Exponent ($e$) | Mantissa ($m$) |
| :-: | :-: | :-: |
| $s_0$ | $b_{10} b_9 \dots b_2 b_1 b_0$ | $d_1 d_2 d_3 \dots d_{51} d_{52}$ |
> Note we read the binary for the exponent from the right to left, but read the mantissa left to right.

Where the following bit counts (and corresponding values) would be assigned:

| Symbol | # Bits | Value |
| :-: | :-: | - |
| $B$ | None | $1023$ |
| $s$ | 1 Bit | $0$ or $1$ |
| $e$ | 11 Bits | $\sum_{i=0}^{10} b_i 2^i$ |
| $m$ | 52 Bits | $\sum_{i=1}^{52} d_i 2^{-i}$ |
> Note that $B = 1023$ offsets the exponent $e$ to allow an approximately equal number of positive and negative powers of 2. 

> [!Warning] Error
> Note that it's simply not possible to represent all real numbers with this representation. To this degree, there are "gaps" in the real numbers representable, and the computer will round to the closest real number during floating point arithmetic. This is fine in most use-cases, but creates **error**, which is discussed later.

## Special Numbers
By virtue of the limited number of bits we can use to represent a real number, it's simply not possible to represent all numbers.

To address this, the machine reserves the exponent values $e = 0$ and $e = 2048$ for special numbers, which represent numbers outside of the representable number range.
- $e = 0$ represents the special number $\pm 0$ (depending on sign), which is treated as a very small number.
- $e = 2048$ represents the special number $\pm \infty$ (depending on sign), which is treated as a very large number.

Note that the smallest possible positive number we can represent is on $s = 0, e = 1, f = 0 \Longrightarrow 2^{-1022}$, so any real number smaller than this is simply given the special number $+0$, known as an **underflow**.

Similarly, the largest possible positive number we can represent is on $s = 0, c = 2047, f \approx 1 \Longrightarrow \approx 0.1799 \times 10^{309}$, so any real number smaller than this is simply given the special number $+\infty$, known as an **overflow**.
> There are equivalent underflows and overflows for negative numbers.

Artithmetic with these special number is defined, and follows logical reasoning if we think of these special numbers as very small or very large values.
> Don't think of $0$ as $0$, instead think of it as a very small number.

For some calculations that we can't be sure about, like $0 \times \infty$, the machine assigns the special number NaN (not a number).

Some examples are given below.

> [!Example]+ Example: Arithmetic with Special Numbers
> $$
> \begin{align*}
>       5 + \infty = \infty \\
>       \infty * \infty = \infty \\
>       1 / \infty = 0 \\
>       \infty / \infty = \text{NaN} \\
>       0 / 0 = \text{NaN}
> \end{align*}
> $$


# Decimal Machine Numbers
While computers represent numbers in binary, us humans (more often than not) work with numbers in decimal. This too, however, can create error, which is described below.

## Scientific Notation
Any $x \in \mathbb{R}$ can be represented as

$$
x = \pm 0.d_1 d_2 d_3 \dots d_{k} d_{k+1} \times 10^n
$$
Where $0 \le d_i \le 9$. This is often known as **scientific notation**. We call **normalizing** the operation of converting a number into its equivalent scientific notation.

> [!Example]+ Example: Scientific Notation
> We can normalize the following numbers as so:
> $$
> \begin{align*}
>       2 = 0.2 \times 10^1 \\
>       0.001 = 0.1 \times 10^{-2}
> \end{align*}
> $$

## $K$-Digit Normalized Form
Note that it's often not possible to represent all digits of a number. So, for these numbers, we often approximate them using their **$k$-digit normalized floating point decimal form**, which limits the number of a number's digits in the decimal form.

To obtain this form, we either perform:
- **Chopping**, where we remove $d_{k+1} d_{k+2} \dots$
- **Rounding**, where we add 1 to $d_k$ if $d_{k+1} \ge 5$, and chop.

> [!Example]+ Example: Chopping vs Rounding
> Suppose we have $x = \pi$, which is approximately $3.14159265\dots$, and let $k = 5$. Then,
> - With chopping, we would represent $x$ as $x = 0.31415 \times 10^1$.
> - With rounding, we would represent $x$ as $x = 0.31416 \times 10^1$.

By virtue of removing digits, this chopping / rounding process creates error.


# Error
## Error Definitions
Due to the infinite number of real numbers possible, error is inevitable. Whether through rounding, or imprecision in instruments, we will (in many cases) obtain numbers that only approximate the actual value.

Below, we discuss the various types of error and their implications. Let $x \in \mathbb{R}$ be approximated by $\tilde{x}$. Then, the **error**, **absolute error**, and **relative error** are defined as follows:

$$
\begin{align*}
        &x - x^* &\text{Error} \\
        &|x-x^*| &\text{Absolute Error} \\
        &\frac{|x-x^*|}{|x|}, x \ne 0 &\text{Relative Error}
\end{align*}
$$

We will use the notation $\epsilon_x$ to denote the relative error of $x$.
> Note that the relative error acts as a sort of normalization on the error value, which can be used to compare errors with one another.

Let $t$ be an integer. If we can bound our relative error at or under the value $5 \times 10^{-t}$,
$$
\frac{|x-x^*|}{|x|} \le 5 \times 10^{-t}
$$
We say that **$x^*$ approximates $x$ to $t$ significant digits**.

Error can be really handy in analyzing algorithms / operations! See the below example.

> [!Example]+ Example: Error in Chopping and Rounding 
> Recall the chopping operation from decimal machine numbers. 
>
> If we chop for $k$-digits on the normalized number $0.d_1 d_2 \dots d_k d_{k+1} \dots$, we will obtain the result $0.d_1 d_2 \dots d_k$. Let's find the relative error of this operation. 
> 
> $$
> \begin{align*}
>         \frac{|x - \tilde{x}|}{|x|}
>         &= \frac{|0.d_1 d_2 \dots d_k d_{k+1} \dots \times 10^n - 0.d_1 d_2 \dots d_k \times 10^n|}{|0.d_1 d_2 \dots d_k d_{k+1} \dots \times 10^n|} \\
>         &= \frac{|0.000 \dots d_{k+1} d_{k+2}|}{|0.d_1 d_2 \dots d_k d_{k+1} \dots|} \\
>         &= \frac{|0.d_{k+1} d_{k+2} \dots \times 10^{-k}|}{|0.d_1 d_2 \dots d_k d_{k+1} \dots|} \\
> \end{align*}
> $$
>
> We know that as the number was normalized, $0.d_1 d_2 \dots d_k d_{k+1} \dots \ge 0.1$, and $0.d_{k+1} d_{k+2} \dots \le 1$. So, our relative error with chopping is
> $$
> \frac{|0.d_{k+1} d_{k+2} \dots \times 10^{-k}|}{|0.d_1 d_2 \dots d_k d_{k+1} \dots|} \le \frac{1}{0.1} \times 10^{-k} = 10^{-k + 1}
> $$
> Thus, if we chop on any normalized number, our relative error will be at most $10^{1-k}$.
>
> Similarly, we can show that with rounding, we find a relative error less than $0.5 \times 10^{-k + 1}$. 

> [!Info] Machine Epsilon
> The **machine epsilon**, denoted $\epsilon_M$, is the smallest machine number which, when added to 1, does not give 1.
> 
> Formally, its the smallest machine number $\epsilon_M$ such that
> $$
> 1 + \epsilon_M \ne 1
> $$
> > For our 64-bit representation, we can find our machine epsilon as $2^{-52}$.
>
> An interesting property of the machine epsilon is that for any $x \ne 0$, the relative error produced by its representation is less than the machine epsilon. Thus, the machine epsilon essentially serves as a "measure" of how close we can represent numbers.

## Error Propagation
### Condition Numbers
Consider a map $f: x \to y$ where $x,y \in \mathbb{R}$, which could represent some sort of operation on $x$.

If $x$ has an error, and is approximated by $\tilde{x}$ such that its relative error is $\epsilon_y$, then what is the relative error in the result $y$ (denoted $\epsilon_y$)?

We find this relative error. Assume $\tilde{x}$ is a close approximation of $x$. Then,
$$
\begin{align*}
        \epsilon_y
        &= \frac{|y - \tilde{y}|}{|y|} \\
        &= \frac{|f(x) - f(\tilde{x})|}{|f(x)|} \\
        &= \frac{1}{|f(x)|} \cdot \frac{|f(x) - f(\tilde{x})|}{|x - \tilde{x}|} \cdot \frac{|x - \tilde{x}|}{|x|} \cdot |x| \\
        &\approx \frac{1}{|f(x)|} \cdot |f'(x)| \cdot \epsilon_x \cdot |x| \\
        &\approx \frac{|f'(x)| \cdot |x|}{|f(x)|} \cdot \epsilon_x 
\end{align*}
$$

As shown above, the resultant relative error in $y$ can be found in terms of the relative error in $x$, where the coefficient is called the **condition number of $f$ at $x$**, $C_f (x)$.
$$
C_f (x) = \frac{|f'(x)| \cdot |x|}{|f(x)|}
$$
The condition number tells us the degree in which $x$'s relative error increased / decreased as a result of the function, and thus provides a good measure in which an error will propagate as a result of a function. 
- If $C_f(x) \approx 1$, the function doesn't create a major change in $x$'s relative error, and we say the function is **well conditioned**.
- If $C_f(x) \gg 1$, the function greatly increases $x$'s relative error in $y$, and we say that the funciton is **ill-conditioned**.

See the below examples, where we use the condition number for analysis.

> [!Example]+ Example: Well Conditioned Function
> Suppose $f(x) = \frac{1}{x}$. We find its condition number for $x \ne 0$ as
> $$
> \begin{align*}
>         C_f(x)
>         &= \frac{|f'(x)| \cdot |x|}{|f(x)|} \\
>         &= \frac{|-1/x^2| \cdot |x|}{|1/x|} = 1
> \end{align*}
> $$
> Because the condition number is 1 for all $x \ne 0$, we say that $f(x)$ is well conditioned for all $x \ne 0$, as for all $x \ne 0$ the relative error in the output $y$ is approximately equal to the relative error in the input $x$. 

> [!Example]- Example: Ill-Conditioned Function
> Suppose $f(x) = \log(x)$. We find its condition number on $x > 0$ as
> $$
> C_f(x) = \frac{|1/x| \cdot |x|}{|\log{x}|} = \frac{1}{|\log{x}|}
> $$
> Notice that as we approach $0$ or $\infty$, $C_f (x) \to 0$, meaning that along these limits our function is well conditioned. However, as we approach 1, $C_f (x) \to \infty$, telling us that around 1, our relative error will greatly increase in magnitude - so our function is ill-conditioned around 1!

WIP
-

### Propagation in Multiplication / Division
Let's now consider error propagation with regard to the standard arithmetic operations: $\times$ and $/$.

In the case of the product ($\times$) $z = x \times y$, where $x$ and $y$ are approximated by $\tilde{x}$ and $\tilde{y}$ (respectively), we find our error $\epsilon_z$ to be:
$$
\begin{align*}
        \epsilon_z
        &= \frac{|z - \tilde{z}|}{|z|} \\
        &= \frac{|x y - \tilde{x} \tilde{y}|}{|xy|} \\
        &= \frac{|xy - x \tilde{y} + (x \tilde{y} - \tilde{x} \tilde{y})|}{|xy|} \\
        &= \frac{|x(y - \tilde{y}) + \tilde{y} (x - \tilde{x})|}{|xy|}
\end{align*}
$$
Here, we apply the triangle inequality ($|a + b| \le |a| + |b|$) and property of multiplicavity ($|ab| = |a| \cdot |b|$) to obtain
$$
\begin{align*}
        \epsilon_z
        &= \frac{|x(y - \tilde{y}) + \tilde{y} (x - \tilde{x})|}{|xy|} \\
        &\le \frac{|x| \cdot |y - \tilde{y}|}{|x| \cdot |y|} + \frac{|\tilde{y}| \cdot |x - \tilde{x}|}{|x| \cdot |y|} \\
        &\le (1) \epsilon_y + \frac{|\tilde{y}|}{|y|} \epsilon_x \\
        &\le \epsilon_y + \frac{|\tilde{y} + (y - y)|}{|y|} \epsilon_x \\
        &\le \epsilon_y + \left( \frac{|\tilde{y} - y|}{|y|} + \frac{|y|}{|y|} \right) \epsilon_x  \\
        &\le \epsilon_y + (\epsilon_y + 1) \epsilon_x \\
        &\le \epsilon_y + \epsilon_x + \epsilon_x \epsilon_y
\end{align*}
$$

Our error is bounded by $\epsilon_z \le \epsilon_y + \epsilon_x + \epsilon_x \epsilon_y$. With this, we make the following observations:
- In the case that $\epsilon_x$ and $\epsilon_y$ are small, our error is approximately bounded by $\epsilon_x + \epsilon_y$.
- In the case that $\epsilon_x$ and $\epsilon_y$ are large, our error is approximately bounded by $\epsilon_x \epsilon_y$. 

In the case of division, we can similarly show that the relative error of $z$ is
$$
\epsilon_z \approx \epsilon_x + \epsilon_{\frac{1}{y}}
$$
Referring to one of the above examples, the function $1/x$ is well conditioned, so $\epsilon_{\frac{1}{y}} \approx \epsilon_y$.
$$
\epsilon_z \approx \epsilon_x + \epsilon_y
$$

Generally, these condition numbers are okay! So, multiplication and division are fine.

### Propagation in Addition 
---

In the case of addition,

$$
\begin{align*}
        \epsilon_z
        &= \frac{|x + y - (\tilde{x} + \tilde{y})|}{|x + y|} \\
        &\le \frac{|x|}{|x|} \frac{|x - \tilde{x}|}{|x + y|} + \frac{|y|}{|y|} \frac{|y - \tilde{y}|}{|x + y|} \\
        &= \frac{|x|}{|x+y|} \epsilon_x + \frac{|y|}{|x+y|} \epsilon_y 
\end{align*}
$$

We see that our error depends on our choice of $x$ and $y$!

Consider the case where $x$ and $y$ have the same sign. We can see that as
$$
\frac{|x|}{|x+y|} + \frac{|y|}{|x+y|} = 1
$$
We have a convex combination of $\epsilon_x$ and $\epsilon_y$! So, our error is bound under the maximum of either $\epsilon_x$ or $\epsilon_y$.

Consider the case where $x$ and $y$ have opposite signs, but have different magnitudes. In this case, our coefficients are not too far from 1, so we have a similar case as the above.

Consider the case where they have different signs and very similar magnitudes. This means that $x + y \approx 0$, which would cause our errors to skyrocket as our coefficients tend towards infinity! So, when $x$ and $y$ have different signs but similar magnitudes, things get unstable.
> This is known as subtractive (catastrophic) cancellation, when 2 numbers cancel each other out - and this typically increases relative error substantially.
>
> **This is often one of the main sources of errors in algorithms.**