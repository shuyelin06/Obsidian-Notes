---
title: Selection Sort
tags:
- cmsc351
---

# Algorithm 
Take a list $A$ of length $n$
$$
        A = [5,2,1,3]
$$

We can iterate through the list, and for every iteration, pick the next smallest element to place at the front of our list. So, for every iteration $i$, we find the $i^{th}$ smallest element and swap it with the element at the $i-1$ index.
1. For the first iteration (swap 1 with 5),
   $$
        [\underline{5},2,\underline{1},3] \to [1,2,5,3]
   $$
2. For the second iteration (swap 2 with itself),
   $$
        [1,\underline{2},5,3] \to [1,2,5,3]
   $$
3. For the third iteration (swap 3 with 5),
   $$
        [1,2,\underline{5},\underline{3}] \to [1,2,3,5]
   $$

We are done!
> Every iteration, we are essentially "picking" the next smallest element to place in the next position!

# Pseudocode
Pseudocode for Selection Sort is given below.

```python
def selection_sort(array):
    # for every iteration, we pick the next smallest
    # element to place at i
    for i in range(0, len(array) - 1):
        # find the ith smallest element
        min_index = i
        
        for j in range(i + 1, len(array)):
            if array[j] < array[min_index]:
               min_index = j

        # place next smallest element at index i
        temp = array[i]
        array[i] = array[min_index]
        array[min_index] = temp
```

Let's find the time complexity of Selection Sort. Let $c$ denote the amount of time it takes for line 9-10 to run. Then, we can find the $\Theta$ of Selection Sort using the number of times $t_{10}$ runs (as it has the most significant contribution to the runtime).
$$
\begin{align*}
        T(n) &= \sum_{i=0}^{n-2} \sum_{i+1}^{n-1} c = \sum_{i=0}^{n-2} c \left( (n-1) - (i+1) + 1 \right) \\
        &= c \sum_{i=0}^{n-2} n-i-1 = c \left(\sum_{i=0}^{n-2} (n-1) - \sum_{i=0}^{n-2} i \right) \\
        &= c \left( \ (n-1) \left((n-2) - 0 + 1\right) - \frac{(n-2)(n-1)}{2} \right) \\
        &= \Theta(n^2)
\end{align*}
$$
> Note that Selection Sort will always take the same amount of time!

Additionally we find,
- The auxilliary memory to be $\Theta(1)$.
- The algorithm is not stable, as our selection can swap and change the relative order of equal elements.
- The algorithm to be in-place, as no additional memory is used.

