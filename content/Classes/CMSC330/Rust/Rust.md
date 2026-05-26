---
title: The Rust Programming Language
tags:
- cmsc330
---

This article serves as brief documentation for the **Rust Programming Language**. It is by no means comprehensive; for full documentation, refer to the official documentation [here](https://doc.rust-lang.org/book/title-page.html).

# Introduction to Rust
## My First Rust Program
To create a Rust program, we will create a file with the `.rs` extension. Then, we need to add a main function using syntax `fn main() {}`, from which our program will run.

Below, we create our first program, the "Hello World" program!

```rust
// hello.rs
fn main() {
   println!("Hello World!");
}
```

Rust provides fine grained control of memory, while managing the allocation and freeing of memory for us. Using specific rules of memory management (see [[Memory Safety in Rust]]), Rust guarantees memory safe programs!

## Compiling Rust Programs
Like many others, Rust is a **compiled language**. This means that to run the program, we need to **compile** our file into something we can execute and run. To do this, we use the Rust compiler, `rustc`. 

By default, `rustc` will create an executable output will be the filename itself, without the `.rs` extension.

```bash
# creates hello.x
rustc hello.rs
```

Note that the `rustc` compiler does not (by default) generate and leave intermediate files like object files and interface files! It only produces a single executable.

# Basic Rust Concepts
## Rust Types
Below, we discuss some basic data types in Rust. Note that on top of these types, we can also define our own (refer to [[User-Defined Types in Rust]]) using combinations of these base types!

Rust is a **statically typed language**, meaning that all types must be known at compile time. The compiler can generally infer what our types are, apart from some special cases.

Types in Rust are split between two subsets:
- **Scalar types**, which represent any single value.
- **Compound types**, which represent multiple values at once.

We begin with the scalar types, and then discuss the compound types.

### Scalar Types
Rust has 4 primary scalar types: integers, floating-point numbers, booleans, and characters. Below, we briefly describe each.

For numeric types such as integers and floats, Rust includes a variety of types to specify the number of bits that are to be allocated for that number. A table of such integer and float types are given below. 

| Length | Integer | Float |
| :-: | :-: | :-: |
| 8-bit | `i8` | |
| 16-bit | `i16` | |
| 32-bit | `i32` | `f32` |
| 64-bit | `i64` | `f64` |
| 128-bit | `i128` | |
| arch | `isize` | |
> The `arch` length depends on the architecture of the system the program is running on - in other words, if the machine is 64-bit or 32-bit.

Note that we can also create unsigned integer types, by replacing the `i` with `u` in any of the integer types.

Additionally, Rust has boolean and character types.
- The boolean type is called `bool`, and can only take on values `true` or `false`.
- The character type is called `char`, and can only take on alphabetic letters (or emojis!)

### Compound Types
In addition to scalar types, Rust also has compound types, which can group multiple values into one type. Rust supports 2 primitive compound types.

The first is a **tuple**, which groups a number of values with (possibly) heterogeneous types into a single type. Tuples are created with a comma delimited list of values between `( )`, and cannot be changed after creation. Note that like other languages, we can use pattern matching with tuples to extract their values.

```rust
let tuple = (2,3,2.1);
let (x,y,z) = tuple; // x = 2, y = 3, z = 2.1
```

Other than tuples, Rust also supports **arrays**, which group a number of values with homogeneous types into a single type. Arrays are created with a comma delimited list of values between `[ ]`, and have a fixed length after creation. However, unlike tuples, individual elements in arrays can be accessed and modified using the indexing operator `[i]`.

```rust
let arr = [1,2,3,4,5];
let x = arr[2]; // x =
```



## Variables and Mutability
To define a **variable** in Rust, use a `let` binding.

```rust
// x stores 5
let x = 5;

// y stores a String "hello"
let y = String::from("hello");
```

Note that when creating a variable, we don't need to specify its type. In fact, the type of the variable will automatically be inferred by the Rust compiler, as Rust is a **statically explicitly typed language**.
> We'll need to explicitly define types for function signatures and structures, however.

Unlike other languages, however, every variable in Rust has an additional concept, known as **mutability**.
- An **immutable** variable is one whose value is set at definition, and can no longer be changed.
- A **mutable** variable is one whose value can be changed anywhere in the scope it's defined.

By default, variables in Rust are immutable. To make a variable mutable, include the `mut` keyword after the `let`.

```rust
// Invalid - immutable type
let a = 5;
a = 3;

// Valid
let mut x = 5;
let x = 3;
```

This is one way Rust ensures memory safe programs!

## Functions
To create a **function** in Rust, use the `fn` keyword. To define a function, we need to explicitly define the types of its parameters and return value.

```rust
// fn [Function] ( [Var1]:[Type1], ... ) -> [Return Type] {}
fn example(x: i32) -> f32 {
   return (x as f32) * 3.0;
}
```

The code blocks comprising function bodies make up a series of statements, and optionally end in an expression. Recall that:
- **Expressions** refer to code that evaluates to and return a value. 
- **Statements** refer to code that do not evaluate to anything, and instead create side effects.

To denote a statement, use `;` at the end of the line. Lines without a `;` are automatically taken as expressions.

The expression at the end of the function will determine what it returns! If no expression is given, however, then the function will return the `unit` type. Alternatively, we can end a function with a `return .. ;` statement to specify its return value.
> Note that these rules are the same for any code block `{ }`, but are more commonly used for functions.


```rust
// These functions are equivalent
fn func_1(x: i32) -> i32 {
   x
}

fn func_2(x: i32) -> i32 {
   return x;
}
```

Note that an expression in Rust must always return the same type, or else the program won't compile. This is especially important to consider for conditional statements.

```rust
// Valid - Returns an integer in all cases
if true { 2 } else { 1 }

// Invalid - Returns an integer and float in different cases
if true { 5 } else { 3.4 }

// Invalid - Returns an integer and unit in different cases
if true { 5 }
```