---
title: Radix Sort
tags:
- cmsc351
---

# Intuition
Consider a list $A$ with elements all given in a specific base. For example, consider the list with integers in base $10$, with at most 3 digits.

$$
A = [125, 231, 236, 234, 573, 491]
$$

Because all of the elements are in the same base, we could theoretically sort $A$ by sorting them by their digits, in order of least-significant to most-significant digit!

If we were to use a stable sorting algorithm to do this, we can ensure that the relative order of elements with some identical digits will be preserved!

We can do this with $A$. Starting from the least significant (rightmost) digit, and working our way to the most significant (leftmost) digit, we sort our array as follows:

$$
\begin{align*}
        &[125, 231, 236, 234, 573, 491] &\text{Original Array} \\
        &[231, 491, 573, 234, 125, 236] &\text{1st Sort} \\
        &[125, 231, 234, 236, 573, 491] &\text{2nd Sort} \\
        &[125, 231, 234, 236, 491, 573] &\text{3rd Sort} \\
\end{align*}
$$

# Radix Sort
## Algorithm
In **Radix Sort**, and given an array $A$ with elements in the same base with at most $d$ digits, we can sort it by applying a stable sorting algorithm to sort elements by each individual digit, in order of least (rightmost) to most (leftmost) significant digit.

Typically, Radix Sort uses Counting Sort as the stable sorting algorithm, because we have a predefined base we can sort on!

## Time Complexity 
Applying Counting Sort as the stable sorting algorithm, we see that for each sort with regards to a digit, we get time $\Theta(n + (b-1))$, where $b$ is our base (as the digits can only range from $0 \to (b - 1)$).

Applying this for every digit up to $d$ digits, we get final time complexity
$$
\Theta( d (n + (b - 1)) ) 
$$

Now, assuming $b$ is fixed, and $d$ doesn't depend on $n$, we have time complexity $\Theta(n)$! However, this assumes independence of $b$ and $d$, and may not hold in all cases. Consider the following example.

> [!Example]+ Example: Time Complexity of Radix Sort
> Let's sort a list of $n$ nonzero ints between 0 and $2^n - 1$, each represented in binary. What's the time complexity?
>
> It takes $n$ binary digits to represent our elements in the list, giving us time complexity $\Theta(n \cdot n) = \Theta(n^2)$.

Furthermore, we have auxiliary space $\Theta(n + (b-1))$, as we will take this much space at any time due to Counting Sort.