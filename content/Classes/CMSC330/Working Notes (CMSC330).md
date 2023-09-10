A**Key Questions**: 
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
