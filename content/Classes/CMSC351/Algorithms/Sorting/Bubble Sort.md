---
title: Bubble Sort
tags:
- cmsc351
---

# Algorithm
Take a list $A$ of length $n$.

$$
A = [5,2,-3,1]
$$

We can iterate through adjacent pairs in the loop, and swap those out of order. Performing this $k$ times, we can guarantee that the final $k$ values are correct (and sorted) - the below example illustrates why.
1. For the first iteration,
   $$
   [5,2,-3,1] \to [2,-3,1,5]
   $$

2. For the second iteration,
   $$
   [2,-3,1,5] \to [-3,1,2,5]
   $$

3. For the third iteration,
   $$
   [-3,1,2,5] \to [-3,1,2,5]
   $$

We are done! Notice how in every iteration $i$ (starting from 1) of the loop, we guarantee the $n - i$ index of the loop correctly contains the $i^{th}$ largest element. Thus, performing this $n - 1$ times, we can guarantee a sorted array (if all $n - 1$ elements are sorted, the first element must be the smallest element).

# Pseudocode
Pseudocode for Bubble Sort is given below.

```python
def bubble_sort(array):
    # i only needs to iterate n - 1 times
    for i in range(0, len(array) - 1):
        # we don't need to check / sort the ith last
        # elements of the array, as they're already sorted
        for j in range(0, n - i - 1):
            # swap the elements if not sorted
            if array[j] > array[j + 1]:
               temp = array[j]
               array[j] = array[j + 1]
               array[j + 1] = temp
```

We find the time complexity of Bubble Sort to be $\Theta(n^2)$, and the **auxilliary memory** to be $\Theta(1)$ (no extra memory). This implementation of Bubble Sort is stable and in-place.
> It's worth noting that regardless if the list is sorted, Bubble Sort **always** takes the same amount of time.

> [!Warning] Bubble Sort Stability
> While this implementation of Bubble sort is stable, that does not mean all implementations necessarily are. If we replaced the $>$ in line 8 with $\ge$, we would make our algorithm unstable!
