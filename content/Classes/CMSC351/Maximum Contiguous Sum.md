---
title: Maximum Contiguous Sum
---

# Maximum Contiguous Sum
> Hi Anna! :>

Given a list $A$, find the maximum contiguous sum. A **contiguous sum** is a sum of contiguous elements in the array, otherwise known as a subarray.
> The beauty of this problem comes with the number of different, distinct ways we can solve it! 

> [!Example] Example: Maximum Contiguous Sum
> $$
> A = [5, -100, 6, -1, 10, -5, 2]
> $$
>
> We find the maximum contiguous sum of 15, given by the subarray $[6, -1, 10]$.

## Solution 1: Brute Force
Possibly the most intuitive way to solve this problem is to check **every possible sum**, and simply take the max. We do this by performing a nested for loop through our array.

```python
def max_cont_sum(array):
    max_sum = array[0]
    
    for i in range(0, len(array)):
        sum = 0
        
        for j in range(i, len(array)):
            sum += array[j]
            max_sum = max(sum, max_sum)
    
    return max_sum
```

However, this algorithm has a time complexity of $\Theta(n^2)$, which is highly inefficient! Can we do better than this?

## Solution 2: Divide and Conquer
Another potential (more effecient) way of solving this problem is using the **divide and conquer** approach. In this approach, we take the problem, and divides it into subproblems, which can be solved and combined to form an answer.
> Dynamic programming algorithms are often implemented recursively.

How might this work?

We could divide our list in half, and find the maximums for each half! However, this comes with a problem - we may split our array where the maximum sum occurs! Thus, we'll need to check for 3 cases when combining 2 arrays:
1. **Case 1**: The left divided array has a greater sum
2. **Case 2**: The right divided array has a greater sum
3. **Case 3**: The maximum sums of the two arrays can be combined

```python
'''
[5, -100, 6, -1, 10, -5, 2]

Through divide and conquer, we split this in half
[5, -100, 6] | [-1, 10, -5, 2]
However, our maximum sum is cut down the middle!
'''

def max_contiguous_sum(array, left, right):
    # base case: if list of length 1, there is only one possible sum
    if left == right:
       return array[left]
    else:
        center = (left + right) // 2 # find the center using integer division

        # find the biggest sum we can find going left
        left_max = max_contiguous_sum(array, left, center)
        # find the biggest sum we can find going right
        right_max = max_contiguous_sum(array, center + 1, right)
        
        # calculate the straddle max
        left_half_max = array[center]
        left_half_sum = 0
        for i in range(center, left - 1, -1):
            left_half_sum = left_half_sum + array[i]
            if left_half_sum > left_half_max:
               left_half_max = left_half_sum
        
        right_half_max = array[center + 1]
	right_half_sum = 0
	for i in range(center + 1, right + 1):
	    right_half_sum = right_half_sum + array[i]
	    if right_half_sum > right_half_max:
	       right_half_max = right_half_sum

        straddle_max = left_half_max + right_half_max

        return max(left_max, right_max, straddle_max)
```

While this code looks unnecessarily complex, we actually find it is more efficient than brute force! We can do a time analysis to see why.
- In our `if` block, we are only returning an array value, which takes constant time, which we'll denote $t_{\text{if}}$.
- In our `else` block, the only code block that has a significant contribution to the time are the for loops at line 24 and 31. These for loops run for
  $$
  \begin{align*}
	(C - (L - 1)) = C - L - 1 \\
	(R + 1 - (C + 1)) = R - C
  \end{align*}
  $$
  times, giving us a total runtime of $L + R - 1$, or in other words, the length of the list (or sublist). Thus, we have time $t_{\text{loop}} (L + R - 1)$, where $t_{\text{loop}}$ is the time it takes for one loop iteration to run.

This is the runtime complexity of each function call! How many function calls are we making?
- At the initial call, we have an array length of $n$, giving us a time of $t \cdot n$.
- At level 1, we have length $n / 2$ but with 2 lists, giving us a time of $2 \cdot \frac{1}{2} t \cdot n = t \cdot n$.
- At level 2, we have length $n / 4$ but with 4 lists, giving us a time of $4 \cdot \frac{1}{5} t \cdot n = t \cdot n$.
- ...

Repeating this, we see that every recursive call, we use $t \cdot n$ time. Note that at recursive level $k$, our array length is $\frac{n}{2^k}$. Thus, our recursion stops at

$$
\frac{n}{2^k} = 1 \to 2^k = n \to k = \lg(n)
$$

$\lg(n)$ levels, giving us a total runtime complexity of

$$
\Theta( n \lg(n))
$$

which is actually better than brute force!

## Solution 3: Dynamic Programing (Kadane's Algorithm)