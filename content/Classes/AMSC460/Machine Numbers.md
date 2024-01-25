---
title: Machine Numbers
tags:
- amsc460
- wip
---

Given any real number $x \in \mathbb{R}$, we know that our computers represent the number using a **finite number of digits**. This yields a finite amount of possible numbers, which are commonly referred to as **machine numbers**.

Here, we discuss how machine numbers are represented in binary, and their consequences.

# Binary Machine Numbers
## IEEE Standard 754
One of the most common representation of numbers in machines is the **IEEE Standard 754**, the floating point representation of numbers.

For a real number $x \in \mathbb{R}$, this standard represents numbers in the following format:

$$
x = (-1)^s 2^{e - \text{B}} (1.m) 
$$

Where
- $s$ denotes the **sign** of the number, which determines whether $x$ is positive or negative.
- $m$ denotes the **mantissa**, which takes on some value between $0 \le m < 1$.
- $e$ denotes the **exponent**, which takes on some positive integer value.
- $B$ denotes the **bias**, which offsets the exponent value to allow for an (approximately) equivalent number of positive and negative powers of 2.

Note that standard essentially represents $x$ in the base-2 equivalent of the scientific notation we're used to. The number of bits allocated to represent the number determines the number of bits available to represent the values of $s,m,e$, and the bias is predetermined based on this size.

For our purposes, we will assume a 64 bit number, otherwise known as a `double`. Using this standard, a number $x$ would be represented as follows (let $s_i, b_i, d_i$ represent bits taking on 0 or 1):

| Sign ($s$) | Exponent ($e$) | Mantissa ($m$) |
| :-: | :-: | :-: |
| $s_0$ | $b_{10} b_9 \dots b_2 b_1 b_0$ | $d_1 d_2 d_3 \dots d_{51} d_{52}$ |
> Note we read the binary for the exponent from the right to left, but read the mantissa left to right.

Where $B$ would take on the predetermined value 1023, and:
- $s$ takes on 1 bit, giving it either the value 0 or 1.
- $e$ takes on 11 bits, giving it the value
  $$
  e = \sum_{i=0}^{10} b_i 2^i
  $$
- $m$ takes on 52 bits, giving it the value
  $$
  m = \sum_{i=1}^{52} d_i 2^{-i}
  $$

Note that $B = 1023$, as $e$ can be a value within the range $[0,2048]$, so setting $B$ as 1023 allows an approximately equal number of positive and negative powers of 2.

> [!Example] Example: Binary Machine Numbers


---

By virtue of this, we see that there are gaps in the numbers we can represent - and in fact, its just not possible to represent all numbers with thsi representation. We are limited by the finite number of bits available.
> Because of this, the **SMALLEST POSITIVE 64-BIT NUMBER WE CAN REPRESENT IS** $s = 0$, $c = 1$, f = 0$, giving us $2^{-1202} \approx 0.2225 * 10^{-307}$.

Anything smaller than this we just set as 0.


> Largest positive number is $s = 0$, $c = 2047$, $f \approx 1$ gives us $0.17997 * 10^{309}$.

Anything larger than this we set as infinity. There's an equivalent negative infinity, which is used to handle overflows.

> Note that $0 < c < 2048$, as we reserve 0 and 2048 for special numbers.

floating point representation of doubles**

---
Special numbers

Inf, -Inf for overflows
- $5 \pm \infty = \pm \infty$
- $\infty * \infty = \infty$
- $1 / \infty = 0$

+0 and -0 for underflows (distinct)
- $+0 == -0$ is true
- Can preserve the sign of 0. For example, if $x = 1e-300$, and $y = -x * x = 0$, then $1 / y = -\infty$.

Indeterminate forms gives NaN, otherwise known as not a number.
- $\infty / \infty$
- $0 / 0$
- $0 / \infty$

---


As not all numbers can be represented finitely, computers will **round**, where a real number $x \in \mathbb{R}$ will be represented as another close number.

Note that any $x \in \mathbb{R}$, $x \ne 0$ can be uniquely represented in the form
$$
x = (-1)^s 2^{c-1203} (1 + f)
$$
where $s$ is either 0 or 1, $c$ is any integer value, and $0 \le f < 1$.

$c$ is typically known as the **exponent** or **characteristic**, where $f$ is referred to as the mantissa.
> This is the IEEE Standard 754 for Doubles (1 bit for the sign 11 for exponent, and 52 bites for the mantissa).

Assume $x > 0$.
1. Then, if $x \ge 2$, then there exists $n \ge 1$ such that
$$
1 \le x / 2^n < 2
$$
Where in this case, $x / 2^n$ will become our $1 + f$ term, and $c = 1203 + n$

2. Similarly, if $1 \le x < 2$, then $x = 1 + f$, and $c = 1203$.

3. If $0 < x < 1$, then there exists an $n \ge 1$ such that
$$
1 \le 2^n x < 2
$$
Where $2^n x  = 1 + f$, and $c = 1203 - n$.

Computers represent numbers this way. However, on a computer, to represent c and f, there are only a limited number of representations of c and f, which limits the numbers we can represent.

On a computer, we need to represent $s

---

## Decimal Machine Numbers
Any $x \in \mathbb{R}$ can be represented as

$$
x = \pm 0.d_1 d_2 d_3 \dots d_{k} d_{k+1} \times 10^n
$$
Where $0 \le d_i \le 9$. This is often known as **scientific notation**.

> [!Example] Example: Scientific Notation
> $$
> \begin{align*}
>       2 = 0.2 \times 10^1 \\
>       0.001 = 0.1 \times 10^{-2}
> \end{align*}
> $$

However, on a machine, it's not possible to represent all the digits. So, we use a concept of **k-digit normalized floating point decimal form**, which limit the number of digits in the decimal form. In such a form, we either perform:
- **Chopping**, where we remove $d_{k+1} d_{k+2} \dots$
- **Rounding**, where we add 1 to $d_k$ if $d_{k+1} \ge 5$, and chop.

> [!Example] Example: Chopping Example
> Suppose we have $x = \pi$, which is approximately $3.14159265\dots$, and let $k = 5$. Then,
> - With chopping, we would represent $x$ as $x = 0.31415 \times 10^1$.
> - With rounding, we would represent $x$ as $x = 0.31416 \times 10^1$.

This leads to errors (continued...)