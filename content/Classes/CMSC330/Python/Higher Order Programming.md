---
title: Higher Order Programming
---

# Introduction
Oftentimes, we think of functions as these unique entities that take in an input, performs a set of operations, and returns an output. In more formal terms, functions define a mapping between a set of possible inputs (**domain**), and a set of possible outputs (**codomain**).

But in reality, functions are just memory addresses pointing to instructions in memory. So, what if we could treat them as any data value?

That exact idea forms the basis of **higher order programming**. In higher order programming, functions are treated like any other data value! This means we can pass functions as arguments, assign them to variables, and use them the same way as any other primitive datatype! This lets us write very general, reusable code that can be applied in a wide variety of situations.
> This is generally known as the **abstraction principle**, which states to factor out recurring patterns as to not state the same operation more than once.


# Common Higher Order Functions
Below, we describe many commonly used higher order functions. For examples / code, we will be using the Python language for its versatility and ease of use.

## The Lambda Function
To support functional programming, some languages have a concept of a **lambda function**, which are anonymous functions that take in any number of inputs, but only have one expression which is evaluated and returned.

In Python, we can declare a lamdba function using the `lambda` keyword.

```python
x = lambda a, b : a + b # define a lambda that adds two numbers
```

Then, we can use the lambda function just as any other function! This includes making function calls, and using it as arguments to other functions!

We typically reserve lambdas for small, temporary functions that we can return or pass into functions.

```python
x = lambda a, b : a + b # adds a and b
y = lambda c : c(5, 2) # makes a function call

x(3,5) # returns 8
y(x) # evaluates to x(5,2) = 7
```

> [!Info] Closure
> Closure refers to how a function has access to its declaration context's scope. 
>
> In Python, when we define a lambda function, the variables in the scope where it was declared (known as its **context**) can be referred to and used in the lambda function itself!
>
> ```python
> x = 5
> a = lambda y : x + y
>
> a(5) # 5 + 5 = 10
>
> x = 7
> a(5) # 7 + 5 = 10; x changed
> ```
>
> Notice that in the above example, when `x` changes in the scope, it changes in the lambda function as well. This is because Python uses **dynamic closure**, meaning we can change our environment to change the behavior of functions previously defined.

Note that because lambda functions just evaluate and return expressions, we can actually create lambdas that return other lambdas - we can chain lambdas together!

> [!Info] Partial Application (Currying)
> **Partial application** refers to the process in which a select number of arguments in a function are fixed (but not all of them).
>
> In Python, we can see examples of this through lambda chaining!
>
> ```python
> # note how we use 'a' in the first lambda to define the behavior
> # of the second
> add = lambda a : lambda b : a + b
>
> # we "fix" the behavior of the lambda
> add3 = add(3) # returns a lambda which adds 3 to a number
>
> add3(4) # 3 + 4 = 7
> ```


## The Reduce (Fold) Function
Suppose we're iterating through an iterable object (commonly a list), and for every element, we want to do something with it. This something could be finding a summation, creating a new list, etc.

Note that when we implement functions to do these tasks, there seems to be a ton of code repeat.

```python
# find the sum of values in a list
def find_sum(list):
    summation = 0
    for x in list:
    	summation += x
    return summation

# create new list
def new_list(list):
    newlist = []
    for x in list:
    	newlist.append(x)
    return newlist
```

Notice that in each function, we are doing very similar things:
1. Initializing some value, be it an integer, list, etc
2. Iterating through every element in the loop
3. For every element, performing some operation on our initializer with it

Thus, we extract this recurring functionality into a higher order function! We commonly call this function **reduce (fold)**.

To use the `reduce()` function in Python, we need to import it from the `functools` package. 

```python
from functools import reduce
reduce( [function], [iterable], [initial value] )
```
> Note that if an initial value is not provided, `reduce()` will automatically take the first element of the list as an initial value.

Given a starting value (called an **initializer**), `reduce()` will iterate through all elements of a list, and will assign to the initializer the output of the function with the initializer and list element passed in. This function (often a lambda) must take in 2 arguments, where the first will represent the initializer, and the second will represent some arbitrary element of the list. 

```python
# an approximation of what reduce() does
def reduce_approximation(function, iterable, init):
    for x in iterable:
    	init = function(init, x)
    return init
```

Some use-cases for `reduce()` are given below.

> [!Example]+ Summing Elements in a List
> Say we have a list of integers `array`, and we want to sum its elements. We can easily do this with the following `reduce()` call:
>
> ```python
> reduce(lambda x, y : x + y, array, 0)
> ```

> [!Example]+ Filtering Even Numbers from a List
> Say we want to filter all even numbers from a list `array`. We can do this with the following `reduce()` call:
>
> ```python
> reduce(lambda x, y : x.append(y) if y % 2 == 0 else x, array, [])
> ```
>
> Note how we can use a ternary operator to perform operations based on some condition.

Note that `reduce()` is one of the fundamental higher order functions, meaning that most other higher order functions can actually just be implemented using reduces!

## The Map Function
Suppose we have an iterable object, and we want to return a new object after performing some operation on each of its elements.

```python
def add_one(array):
    newlist = []
    for x in array:
    	newlist.append(x + 1)
    return newlist

def mult_two(array):
    newlist = []
    for x in array:
    	newlist.append(x * 2)
    return newlist
```

Notice that all of these functions do the same thing:
1. Iterate through every element in the list
2. For every element, perform an operation and add to a new list

Instead of writing multiple separate functions to do essentially the same task, we could instead extract the core functionality into a higher order function! Introducing the **map** function, which will return a new list where every element has some some provided operation (given as a function) applied to it!

In Python, we can directly call the `map()` function without importing anything! Note that map does not modify the original data structure - in fact, functional programming conventionally assumes that all data was immutable, forcing data structures to be recreated from scratch.

```python
map( [function], [iterable object] )

list(map(lambda x : x + 1, [4,5,6])) # returns [5,6,7]
list(map(lambda x : x * 3, [1,2,3])) # returns [3,6,9]
```
> Note the explicit conversion to a `list()` - in fact, the Python `map()` function actually returns a `Map` object, so we'll need to perform an explicit cast to a list before using the output. 

> [!Info] List Comprehension
> If this wasn't convenient enough, Python also provides a shorthand for performing map functions, known as **list comprehension**! The syntax for list comprehension is given as follows:
>
> ```python
> newlist = [ [expression] for [item] in [iterable] if [condition] ]
> ```
> > Note that the outer brackets (`[ ]`) are necessary - the inner brackets are used to denote fields we can fill in.
>
> This syntax iterates through all `[item]`'s in a list, and given that they fulfill a `[condition]`, will append the output of `[expression]` (likely with the item as an input) to the new list.
>
> Some examples are given below.
> ```python
> list_1 = [ x + 2 for x in [1,2,3] ] # [3,4,5]
> list_2 = [ x * 2 for x in [1,2,3,4,5] if x % 2 == 1 ] # [2,6,10]
> ```