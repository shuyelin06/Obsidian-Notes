---
title: Binary Search
tags:
- cmsc351
---

Suppose $A$ is a sorted list of length $n$ containing distinct elements. Given a specific target element $k$ (which may or may not be in the list), how could we find that element (or fail)?

# Binary Search
Choose some value $v$ at index $i$ in the array. Then, given that the list is sorted, we can make some key insights that drive the idea behind binary search: 
- If $k < v$, we guarantee that if $k$ exists, it is in some index $j$ less than $i$.
- If $k > v$, we guarantee that if $k$ exists, it is in some index $j$ greater than $i$.

We can use this fact to restrict our search interval (by dropping all indices we know $k$ isn't in), until we either find $k$ or don't.

If we do this starting from the middle of the array, we can continuously cut the size of our array in half until we find $k$ or don't. Consider the following example.

> [!Example] Example: Binary Search Algorithm
> $$
> A = [1,3,5,7,10,40,50]
> $$
>
> Suppose we're looking for element 5. Then, starting from the middle of the array,
> 1. Examining index 3 to find 7, we know that because $5 < 7$, if 5 exists, it must be at an index less than 2. Thus, we will examine the subarray to the left of index 3 next.
>    $$
>    A = [\underline{1},\underline{3},\underline{5},7,10,40,50]
>    $$
> 2. Examining the middle of the left subarray, index 1 to find 3, we know that because $5 > 3$, if 5 exists, it must be at an index greater than index 1. Thus, we examine the subarray to the right of index 1 next.
>    $$
>    A = [1,3,\underline{5},7,10,40,50]
>    $$
> 3. We the only element in this right subarray to find 5.

The algorithm is given below (in Python)

```python
def binary_search(array, target):
    left = 0
    right = len(array) - 1

    while left <= right:
          center = (left + right) // 2 # integer division

          if array[center] == target: # element found!
             return center
          else: # element not found. restrict our interval
                if target < array[center]: 
                   right = center - 1
                elif target > array[center]:
                   left = center + 1

    return -1
```
> Note that binary search is often known as a **decrease and conquer** method, as our list search interval is decreasing every iteration.

Let's perform a time complexity analysis on Binary Search.
- In the **best case**, the target is the first element we check in the array. In this case, our while loop only executes once, giving us $\Theta(1)$.
- In the **worst case**, the target does not exist in the array. In this case, the binary search continually divides the array in half, so for iteration $i$, we have list size $n / 2^i$. The algorithm will stop when the list size is 1, so we have a total of $\lg(n)$ iterations.
  $$
  \frac{n}{2^i} = 1 \to i = \lg(n)
  $$
  But when the list size is 1, the while loop will still execute once, giving us $\lg(n) + 1$ total iterations, and time complexity $\Theta(\lg(n))$.

We now analyze the average case for Binary Search. To do this, we find the expected value of choosing any random element (uniformly) from a list of length $n$. To help simplify the calculations, we will focus on lists with length $n = 2^k - 1, k \in \mathbb{Z}^+$.
1. In the $k = 1 \to n = 1$ case, our while loop iterates once.
2. In the $k = 2 \to n = 3$ case, if the element is in the middle, our while loop iterates once. Otherwise, we perform case (1) 2 times, once for the left subarray and once for the right subarray. Thus, we have 1 element with 1 iteration, and 2 elements with 2 iterations.
3. In the $k = 3 \to n = 7$ case, if the element is in the middle, our while loop iterates once. Otherwise, we perform case (2) 2 times, once for the left subarray and once for the right subarray. Recursively continuing this, we will have 1 element with 1 iteration, 2 elements with 2 iterations, and 4 elements with 3 iterations.

We can continue this argument to find that generally, for $i$ iterations, we have $2^{i-1}$ elements in the list. Given that every element has an equal chance of occurring, we find expected value

$$
\sum_{j=0}^{i-1} = \frac{2^i}{n} (c_1 + i c_2)
$$
which comes out to be $\Theta(\lg(n))$.