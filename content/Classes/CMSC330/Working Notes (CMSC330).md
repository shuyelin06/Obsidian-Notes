**Key Questions**: 
- What is a programming language?
- Why do so many programming languages exist, when one language could (theoretically) be used to solve every problem?
- How do we design / implement a language?

# -- Notes Below --
Ocaml, Python, Racket, Rust

# Python
## Overview
```python
print("Hello World!")
```

**Python** is a general purpose **interpreted language**, often used in various sectors of Computer Science due to its relative ease of use.
> **Interpreted languages** are compiled/executed line by line instead of the entire program being compiled/executed at once.

Python has the following language properties:
- **Dynamically Typed**: Type checking of variables is performed at run-time.
- **Latently (Implicitly) Typed**: Variable types are inferred by the compiler and do not need to be explicitly declared.

These paradigms increase Python's ease of use!

## Basic Python Program
A basic Python program is given below.

```python
'''
Multiline Comment
'''
# Single Line Comment

# Obtain 

```

##### Control Flow
`while`, `for`, etc

##### Scoping
```python
'''
throws an error - we're defining a local a before 
defining it globally.
'''
a = 5
def f():
	a = 7
	global a
	a = a + 1
	print(a)
```
python does not let us modify global variables in local functions - enter the `global` keyword, which will let us declare a variable as a global variable / let us modify it.

```python
a = 5

'''
throws an error
'''
def f():
	a = a + 1
	print(a)

'''
okay
'''
def g():
	global a
	a = a + 1
	print(a)
```
## OOP in Python
Python supports Object Orientated Programming

```python
class Test:
	# Constructor
	def __init__(self, _a: int):
		self.a = _a
	
	# To String Method
	def __str__():
		...
		
	# Method
	def method(self):
		print("Method Ran!")
```

Objects have methods, 
python has an equivalent to the "null' type (`None`)

Security vs convenience - as security increases, convenience decreases

# Type Checking
**Type checking** refers to the process of determining a variable's type. This lets us perform checks on variables and functions, to ensure that the program is running as intended (and throw errors if it is not).

Typing can occur at various stages of a program.
- **Dynamic Typing**: The performing of type checking at run-time.
- **Static Typing**: The performing of type checking at compile-time.

Additionally, typing can either be done explicitly or implicitly:
- **Manifest (Explicit) Typing** refers to the need to explicitly tell the compiler the type of new variables. 
  In manifest typing, types are associated with variables.
- **Latent (Implicit) Typing** refers to the lack of need to give a type to a variable (the compiler will infer)
  In latent typing, types are associated with values.

# Higher Order Functions
**Properties of Functions**
We can think of functions as mappings from a domain to a codomain.
- Domain: Set of input values to a function
- Codomain: Set of output values to a function

Environment: A mapping of variables to values 
When devleoping a product, we need to ensure that it is portable and can easily be used by future programmers.

--> **higher order programming** - treating functions as data - using functions inside one another.

One such higher order function is the **lambda function**. These are functions which, instead of a standard function definition, appear syntactically similar to a variable.

To define a lambda function, we use keyword `lambda`.

```python
example_lambda = lambda x : x + 1 # adds 1 to the input
example_lambda(3) # returns 4
```

Lambdas can even support multiple inputs.

```python
example_2 = lambda x,y : x + y
```

Lambda functions allow us to pass in functions as data into other functions! They are typically reserved for small, temporary functions we use to pass into functions, or return from other functions.

```python
add = lambda x,y : lambda y : x + y
new_lambda = add(3)
new_lambda(6) # 3 + 6 = 9
```

This idea of creating functions that will be "finalized" later is known as **closure**! We can define functions that return lambdas, whose behaviors are semi-initialized!
> In python, closure is **dynamic**. We can change our environment to change the behavior of functions already defined

```python
x = 5
b = lambda y : x + y

b(4) # 9

x = 2
b(4) # 6, x changes which changes the lambda stored in b.
```

In the above example, when we call `add()`, we are returning a lambda
```
lambda y : 3 + y
```
which has some behavior defined, but can still take in additional inputs!

This can enhance our code!

At the end of the day, all a function is is a **memory address** in code. So, if we can figure out how to treat functions as variables

11:09 AM -> ?


- REPL: Read Eval Print Loop (this is what python does)

Common higher order functions:
- map: Creating a mapping from our domain to our codomain. For example, we have a list of functions that operate on a list, and we can pass in lambdas as mappings to determine what list this function returns.

> Python actually has this! We can create a map() object in python that takes in a lambda and an iterable list, and it will apply the lambda to all values in the list! Any data structure can be mapped through!

Does not modify the original data structure - functional programming conventionally used to assume that all data was immutable.

```python
a = [1,2,3,4]

list(map(lambda x : x + 1, a)) # [2,3,4,5]
```

but there's a short hand for this, known as **list comprehension**!

```python
# equivalent to before, returns [2,3,4,5]
[x + 1 for x in [1,2,3,4]]
```

---

- reduce: taking a list of values, and reducing it to a single value somehow.

> This can be us reducing characters into a string, summing integers, etc.

In python, we can obtain the reduce function by importing it (not in the standard library)

```
from functools import reduce
```

Reduce takes every pair of elements in the list, and returns (and puts back into the list) a single value. It continues to do this until we have a single value.

```python
def concat(lst):
    ret = ""
    for x in lst:
    	ret += x
    return ret

def prod(lst):
    ret = 1
    for x in lst:
    	ret *= x
    return ret


# All of these functions have a common structure
def common(lst, init, f):
    ret = init # init value
    for x in lst:
    	ret = f(ret, x) # updates ret with x
    return ret

# this is what the reduce function essentially does!
# updating function, list to operate on, and init value
reduce(lambda x,y: x + y, [1,2,3,4], 0)
# if init value is not provided, x automatically takes the first element of the array.
```
> THis reflects a common idea - how do we write programs modularly, and abstract parts of programs from one another?

note that reduce is one of the fundamental HOF functions - map and filter (other HOF) can actually just be implemented using reduces!