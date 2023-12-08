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

---

```rust
let v = "hello"
v -> [];
```

slices are segments of memory that are known at compile time.

## Lifetime
--- WIP

If Rust CANNOT guarantee that a program is safe, it simply will not compile that program.

note that when Rust does a copy, it will always try to do a shallow copy as deep copies are expensive. To force a deep copy,  use the `.clone()` method.

---

Given a `String`, we can get portions of it with type `&str` known as **slices**. These refer to a location in a string, and store the length they can refer to in the string.
> Essentially, they represent a pointer to the string's characters!

`.push_str` really just links one string to another, in a sort of linked list.

```rust
let mut a = String::from("hello");
push(&mut a);

fn push(x: &mut str) {
   x.push_str("world");
}
```

Calling `.push_str` will allocate new space on the heap for `"world"`, and then modify the `"hello"` string to point to the `"world"` string to create a sort of a linked list storing the entire word `"helloworld"`.

```mermaid
graph LR
      1["hello"] -. push_str .-> 2["world"];
```

---

Cellula Automata

Conway's Game of Life

Going to create a grid with cells, which can either be **live** or **dead**.
1. Any live cell with 2 or 3 live neighbors live, all others die.
2. Any dead cell with exactly 3 live neighbors are revived.

Esoteric Programming Languages: Languages that defy expectations

---
Rust
- Memory Safe Programs in Rust
- Structures in Rust
- Smart Pointers in Rust

Final Topics:
- Regex / Regular Languages
- Automata Theory (Finite State Machines)
- Lambdas / closures
- Functional programming and higher order functions
- Grammars (context free grammars)
- Operational Semantics
- lexing, parsing, interpreting
- Lambda calculus
- Language stuff
  - Python
  - Ocaml
  - Rust
- Typing


# Smart Pointers (?)

In addition to references, Rust has **smart pointers**. These are pointers that point to not only memory on the heap, but also extra data associated with that memory.

A common example of this is when we create a `String`.

```rust
let x = String::from("Hello");
```

While `x` will point to memory allocated for a string `"Hello"`, it also has additional data we can reference (ex. string length). This extra data is typically dropped when the memory it's associated to goes is dropped.

Smart pointers are extremely important in creating recursive data structures! Consider the following example.

```rust
enum LinkedList {
     Cons(i32, LinkedList),
     Nil
}
```

Because data structures that we define must have a size known at compile time, this won't compile, as one `LinkedList` needs to allocate enough space to store another `LinkedList` inside itself.

We can work around this using the `Box<T>` type, a special type of smart pointer that will store types we give it into the heap. This is a type whose size is known (and can be treated like a "primitive type" which by default is allocated on the stack), and we can use this to fix our `LinkedList` structure.

```rust
enum LinkedList {
     Cons(i32, Box<LinkedList>),
     Nil
}
```

---

Examples of other smart pointers are given as follows:
- `Vectors`
- `Strings`
- `Slices` of vec, string/str, arrays

Smart pointers will automatically check for memory issues for us. It's not needed to check that an index is within the bounds of an array, for example, as rust will automatically check this for us.

