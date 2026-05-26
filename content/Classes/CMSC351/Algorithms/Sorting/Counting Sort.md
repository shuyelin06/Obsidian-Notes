---
title: Counting Sort
tags:
- cmsc351
---

# Intuition
Consider a list $A$ with non-negative integers within some fixed range $0 \dots k$. For example, consider the list with integers in the range $0 \dots 5$.
$$
A = [3,5,1,2,3,1,2,4,3]
$$

Because we know that all of the integers in our array are within a fixed range, we could theoretically sort $A$ by defining an array to store the counts of every integer in $A$, and then use this array to reconstruct a sorted version of $A$!

Let's define an array $P$ of size 6, where each index stores the count of its respective integer. Creating $P$, we obtain
$$
P = [0,2,2,3,1,1]
$$

We can use this array to reconstruct a sorted version of $A$! Note that because we know the counts of every integer, we can read $A$ left to right, and progressively add any integer whose count is $> 0$ to our new array.

1. We will have no $0$'s in $A$.
2. We will have $1$ at index 0, and $1$ at index 1.
3. We will have $2$ at index 2, and $2$ at index 3.
4. ...

Let's transform our array to make this reconstruction process easier. Redefine every index $i$ in $P$ to store the cumulative count of every integer prior to and up to $i$. 
$$
P = [0,2,4,7,8,9]
$$

This transformed array now tells us the last index in the sorted array (non-inclusive) of the respective integer represented by index $i$! We can use this to easily reconstruct our sorted array.
1. We will have 0's up to and not including index 0 of the array.
2. Then, we will have 1's up to (and not including) index 2 of the array.
3. Then, we will have 2's up to (and not including) index 4 of the array.
4. Then, we will have 3's up to (and not including) index 7 of the array.
5. ...

Knowing these index positions, we can look up the position of elements in $A$, and rearrange them to obtain our sorted list! Iterating through $A$ right to left (to maintain relative order),
1. We see element 3, and because $P[3] = 7$, we know that in our sorted array, this element will be at index $7 - 1 = 6$. We insert, and decrement $P[3]$ by one.
2. We see element 4, and because $P[4] = 8$, we know that in our sorted array, this element will be at index $8 - 1 = 7$. We insert, and decrement $P[4]$ by one.
3. ...

Repeating this process, we obtain the final sorted array.

$$
A = [1,1,2,2,3,3,3,4,5]
$$

> Note that this method of "looking up" element indices lets us generalize counting sort beyond simple integers!

# Counting Sort
## Pseudocode
In **Counting Sort**, and given an array $A$ with integers in the known range $0 \dots k$, we can sort it by:
1. Counting the number of occurrences of each integer in $A$, and storing it into an array $P$, where the index $i$ represents that integer's count.
2. Transforming the indices in $P$ so that every index $i$ stores the cumulative count of every integer prior. This new array $P$ now stores the last index (non-inclusive) that an integer represented by index $i$ will be found at.
3. Then, for every integer in $A$, we can use $P[i]$ to lookup its index, and put it into a new array at this location! Note that to ensure the algorithm is stable, we will have to iterate through $A$ backwards.

The pseudocode for the algorithm is given below.

```python
def counting_sort(array, k):
    # Count Occurrences
    p = [0] * (k + 1)
    for x in array:
        p[x] += 1

    # Transform P
    for i in range(1, len(p)):
        p[i] += p[i - 1]

    # Reconstruct A
    new_array = [0] * len(array)
    for x in array:
        new_index = p[x] - 1 # Offset by 1 to find last index
        new_array[new_index] = x

    for i in range(0, len(array)):
        array[i] = new_array[i]

    return output
```

Note that we could also modify counting sort to work on other inputs!
- For example, we could sort a list of fractions following the form $1/a$ where $a$ is a positive integer, by inverting every fraction before sorting.
- For, we could sort a list of integers between $-10$ and $10$ inclusive, by adding $10$ to all integers before sorting, then reverting this change.

## Time Complexity and Other Properties
Let's analyze Counting Sort for its time complexity. Suppose that our array $A$ has length $n$, and contains integers within the range $0 \dots k$.

Then, note that:
- The first loop on line $L_4$ will take $n$ time
- The second loop on line $L_8$ will take $k$ time
- The third loop on line $L_{13}$ will take $n$ time
- The fourth loop on line $L_{17}$ will take $n$ time

Adding these times together, we find overall time complexity $\Theta(n + k)$!

Now consider the case where $k$ is independent of the list size $n$. Then, this makes $k$ a constant, giving us time complexity $\Theta(n)$!
> However, this does not necessarily mean Counting Sort is always linear time - for example, if $k = n^2$, then we would have complexity $\Theta(n^2)$! So, counting sort depends on the entries in the list.

Furthermore, we see that:
- We have **auxiliary space** $\Theta(n+k)$ as `new_array` has length $n$, and `p` has length $k + 1$.
- This implementation of Counting Sort is stable and not in place.