---
title: Karatsuba's Algorithm
tag:
- cmsc351
---

**Problem**: Given two integer numbers $N_1$ and $N_2$, how can we multiply these numbers together while minimizing the number of single-digit multiplications?

# Intuition
## Product of Two Double-Digit Numbers
Suppose we're multiplying two base 10 numbers $a_1 a_0 \cdot b_1 b_0$ where $a_i$ and $b_i$ are digits. Then we have the following product:
$$
\begin{align*}
        (10 a_1 + a_0) (10 b_1 + b_0) \\
        100 a_1 b_1 + 10 (a_0 b_1 + a_1 b_0) + a_0 b_0
\end{align*}
$$

By the typical method of multiplication, we have 4 single digit multiplications!
$$
a_1 b_1 \qquad a_0 b_1 \qquad a_1 b_0 \qquad a_0 b_0
$$

However, using the term $(a_1 + a_0)$ and through smart manipulation, we can actually reduce the number of single digit multiplications down to 3!
$$
\begin{align*}
(a_1 + a_0) (b_1 + b_0) = a_1 b_1 + a_0 b_1 + a_1 b_0 + a_0 b_0 \\
\to a_0 b_1 + a_1 b_0 = (a_1 + a_0) (b_1 + b_0) - a_1 b_1 - a_0 b_0
\end{align*}
$$

Plugging this back into our original equation, we find
$$
\begin{align*}
(10 a_1 + a_0) (10 b_1 + b_0) = 10^2 a_1 b_1 + 10 [ (a_1 + a_0) (b_1 + b_0) - a_1 b_1 - a_0 b_0 ] + a_0 b_0 \\
\end{align*}
$$
Which now has 2 single digit multiplications, and one multiplication $(a_1 + a_0) (b_1 + b_0)$ which may or may not be a single digit multiplication. Regardless, this product should be significantly easier than a standard 2 digit multiplication!

Thus, to calculate $(a_1 a_0) (b_1 b_0)$, we will be performing:
- 3 single digit multiplications (approximately)
- 6 additions or subtractions with up to 2 digits per operation
- 3 decimal shifts (multiplication by 100 and 10)

> Note that when we multiply by 10, we're really performing a left shift (similar to bitwise shifts).

## Generalization
Now, let's try to generalize this to numbers with more digits. Suppose we're calculating the product of two 4-digit numbers, $(A_1 A_0) \cdot (B_1 B_0)$.

By the same process, while accounting for the change in base, we obtain product
$$
(100 A_1 + A_0) (100 B_1 + B_0) = 100^2 A_1 B_1 + 100 [ (A_1 + A_0) (B_1 + B_0) - A_1 B_1 - A_0 B_0 ] + A_0 B_0
$$

We now have
- 3 double digit multiplications
- 6 additions and subtractions on 4 digits
- 6 decimal shifts total

There's a pattern here!

Suppose we have two numbers $A_1 A_0$ and $B_1 B_0$, where both have $n$-digits, $n$ is even. By the same process as before, we find that $A_1 A_0 \cdot B_1 B_0$ is
$$
(10^{n/2} A_1 + A_0) (10^{n/2} B_1 B_0) = 10^{n} A_1 B_1 + 10^{n/2} [ (A_1 + A_0) (B_1 + B_0) - A_1 B_1 - A_0 B_0 ] + A_0 B_0
$$

Where we have:
- 3 multiplications on $\frac{n}{2}$ digits
- 6 additions or subtractions with up to $2n$ digits
- $n + n/2$ decimal shifts total

We can recursively apply this formula until we reach our base case of single digit multiplications!

This is the idea behind Karatsuba's algorithm - by smartly defining our product, we can minimize the number of single digit multiplications, and thus our time complexity for the overall multiplication!

# Karatsuba's Algorithm
## Pseudocode
Given the product of two numbers $A_1 A_0 \cdot B_1 B_0$, where both have $n$ digits ($n$ is even), we can minimize the number of single digit multiplications by calculating the product
$$
(10^{n/2} A_1 + A_0) (10^{n/2} B_1 B_0) = 10^{n} A_1 B_1 + 10^{n/2} [ (A_1 + A_0) (B_1 + B_0) - A_1 B_1 - A_0 B_0 ] + A_0 B_0
$$

And recursively applying it on the 3 smaller products 
$$
A_1 B_1 \qquad (A_1 + A_0)(B_1 + B_0) \qquad A_0 B_0 
$$

Until we reach our base case of single digit multiplications!

Pseudocode for the algorithm is given below.

```python
def karatsuba(A,B):
    if single_digit(A) || single_digit(B):
       return A * B:
    else:
        digits_half = min(num_digits(A),num_digits(B)) / 2
        A1, A0 = split(A, digits_half)
        B1, B0 = split(B, digits_half)

        k1 = karatsuba(A1, B1)
        k2 = karatsuba(A1 + A0, B1 + B0)
        k2 = karatsuba(A0, B0)

        return (10^(2 * digits_half)) * k1 + (10^(digits_half)) * (k2 - k3 - k1) + k3
```

See the below example for Karatsuba's Algorithm.

> [!Example]- Example: Karatsuba's Algorithm
> Using Karatsuba's algorithm, multiply the following 2 numbers together.
> $$
> (8254)(13491)
> $$
>
> Let's draw a tree diagram to show the products we're performing. Karatsuba's algorithm will perform the following multiplications:
>
> ```mermaid
> graph LR
>       1[8254 * 13491] -.->
>            2[82 * 134] & 3[136 * 125] & 4[54 * 91];
>       2 -.->
>         5[8 * 13] & 6[10 * 17] & 7[2 * 4];
>       3 -.->
>         8[13 * 22] & 9[19 * 27] & 10[5 * 6];
>       4 -.->
>         11[5 * 9] & 12[9 * 10] & 13[4 * 1];
> 
>       5 -.-> 14[Return 104];
>       6 -.->
>         15[1 * 1] & 16[1 * 8] & 17[0 * 7];
>       7 -.-> 18[Return 8];
> 
>       8 -.->
>         19[1 * 2] & 20[4 * 4] & 21[3 * 2];
>       9 -.->
>         22[1 * 2] & 23[10 * 9] & 24[9 * 7];
>       10 -.-> 25[Return 30];
> 
>       11 -.-> 26[Return 45];
>       12 -.-> 27[Return 90]
>       13 -.-> 28[Return 4];
> 
>       15 -.-> 29[Return 1];
>       16 -.-> 30[Return 8];
>       17 -.-> 31[Return 0];
> 
>       19 -.-> 32[Return 2];
>       20 -.-> 33[Return 16];
>       21 -.-> 34[Return 6];
>       22 -.-> 35[Return 2];
>       23 -.-> 36[Return 90];
>       24 -.-> 37[Return 35];
> ```
>
> This will yield 18 single digit multiplications (recall that multiplications like $10 * 9$ would take 2 single digit multiplications), compared to the schoolbook multiplication which would need 20 single digit multiplications.

## Time Complexity
Let's find the time complexity of Karatsuba's Algorithm.

If we apply Karatsuba's algorithm on the product of 2 $n$ digit numbers, we perform 3 multipliations on $n / 2$ digits, and perform a fixed number of additions and decimal shifts.

This gives us recurrence relation
$$
T(n) = 3 T(n/2) + \Theta(n)
$$

Which, after applying the master theorem, gives us
$$
T(n) = \Theta(n^{\lg_2(3)}) \approx \Theta(n^{1.5849625})
$$

> Note that the schoolbook method of multiplying 2 n-digit numbers requires $n^2$ single digit multiplications, giving us $\Theta(n^2)$. Thus, implementing this new algorithm gives us a better time complexity!