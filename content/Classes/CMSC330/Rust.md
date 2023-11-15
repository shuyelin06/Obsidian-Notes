---
title: Rust Programming Language
tags:
- cmsc330
---

This article serves as brief documentation for the **Rust Programming Language**.

# Introduction to Rust
## My First Rust Program
To create a Rust program, we first need to create a file with the `.rs` extension. Below, we create a hello world program, which prints `Hello World!`.
```rust
// hello.rs
fn main() {
   println!("Hello World!");
}
```

Like many others, Rust is a **compiled language**. This means that to run the program, we need to first **compile** our file into something we can execute and run. To do this, we use the commmand `rustc`. By default, the executable output will be the filename itself, without the `.rs` extension.
```bash
rustc hello.rs
```
> Note that the `rustc` compiler does not (by default) generate and leave intermediate files like object files and interface files! It only produces a single executable.

## Basic Syntax in Rust

```rust
// variable declaration
let x = 37;

// tuple declaration
let (a,b,c) = ("I'm", 1, '8'); // tuples are heterogeneous

// for loop
for y in 0..10 {
    println!("{}", y); // implicit format specifiers
}

// if statement
let a = if true {false} else {true};

// variable scoping
let a = 3
{
        let a = a + 2; // variable shadowing
}

// function declaration
fn other() {
   println!("unit -> unit");
}

// function declaration with parameters
fn other2(x: u32) -> u32{ // we define types as the number of bits they take up
   let res = x + 1;
   println!("u32 ({}) -> u32({})", x, res);
   res // no semicolon to return from a code block
}

```
> Note that we can actually specify the size of types in rust! this seems to imply the existence of a u64, u128, telling us that Rust lets us have greater control to memory, while avoiding common issues that we see in C!

Rust provides fine grained control of memory, while managing the allocation and freeing of memory for us! It aims to be a memory secure language!

Rust prefers static and explicit typing. While you don't have to be explicit with variables, you'll need to explicitly define types for more complex things (ex. functions).

Rust makes a distinction between expressions and statements. Recall that **expressions** refer to code that can evaluate to a value that can be manipulated, whereas **statements** refer to code that do not, and instead create side effects. In rust, we end statements with `;`, and do not include a `;` to denote an expression.
> Having an expression at the end of a code block will make it "evaluate to" this expression and return this value for anything accepting it!
>
> Expressions in rust MUST always have the same return type (consider a if else statement!)

```rust
let x = if false {true} ;
// FAILS IN COMPILATION, because this can evaluate to both type bool and unit,
// which is a type conflict!

// now succeeds, because true; makes both branches of the if block return unit(), so the expression will always return type unit!
let y = if false { true; };
```

In rust, we have code blocks, which is code surrounded by `{}`. In rust, code blocks will have statements, followed by 0 or 1 expressions (which the code block will evaluate to and return). If no expression is provided, rust will return the default return type, `unit`.
> `usize` is the default size for some value on a machine.
>
> functions are just code blocks!

One way Rust ensures safe programs is through the use of **immutable types by default**, where a type can only be mutable if it is explicitly denoted as so with the `mut` keyword.

# Memory Safe Programs
In langauges closer to the hardware such as C, low level access to memory provides lots of versatility and flexibility, yet at the same time allows for unsafe code! Notably, with low level access to memory, there are numerous unsafe memory operations that we can do, which may cause undefined behavior!

Two common unsafe memory operations we can accidentally do are given as follows:
- **Type Unsafe Operations**: The accessing and use of memory whose type differs from the expected type.
- **Temporally Unsafe Operations**: The accessing and use of memory not allocated, or already freed by the program.

To avoid these issues and ensure a secure program, the Rust compiler adds constraints to Rust programs! However, as a result of this convenience, there are a subset of safe programs that Rust will not be able to compile!

To ensure memory secure programs, Rust adheres to two key concepts: **ownership** and **lifetimes**, described below.

## Ownership
In Rust, values have owners, and each value can only have one owner at a time. When the owner goes out of scope, the value will automatically be dropped. This is known as **ownership**.

Only the owner of a value can be used to refer to it! Consider the following example, where we bind `x` to a string allocated from the heap.

```rust
fn main() {
   let x = String::from("hello");
}
```

After this binding, we say that `x` has ownership of the memory allocated by the string `hello`. However, if we follow this with the binding

```rust
let y = x;
```

Then, we say that the ownership of `x` has **moved** to `y`, meaning that we can no longer use `x` to refer to the string `hello`, as it no longer "owns" the memory!

```rust
println!("{}", x); // ERROR, x no longer has ownership of "hello"
println!("{}", y); // OKAY, y has ownership of "hello"
```

To do this, the Rust compiler will track the ownership of all values in the program at any given time. This can quickly become quite complex, and the ownership of a variable can be passed between multiple owners.

However, by guaranteeing that a value will always only have one owner, we ensure that only one free can occur, and undefined memory accesses are not possible!

## Lifetime
--- WIP

