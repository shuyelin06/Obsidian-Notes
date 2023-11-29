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
### Ownership in Rust
To implement proper memory management, higher level languages will typically utilize some form of garbage collection in order to manage memory. However, this creates overhead, and can significantly slow down a program!

To work around this, Rust adheres to an idea called **ownership**. Ownership in Rust follows 3 rules:
1. Every value has an "owner".
2. Only one owner is allowed at any given time, though ownership can be transferred with a `let` binding.
2. When a value's owner goes out of scope, the value will automatically be dropped (freed).

These rules apply to variables referring to memory stored on the heap ("pointer" type variables). Variables storing values that do not refer to the heap simply just have these values copied on another `let` binding. 

```rust
let x = String::from("hello"); // Refers to memory on heap
let a = x; // Ownership of "hello" transferred from x -> a

let y = 5; // Just a value on the stack
let b = y; // No ownership transfer, b just gets value 5
```

Transfer of ownership can be avoided through use of deep copies (through the `.clone()` method), which will duplicate memory allocated on the heap! Instead of transferring ownership of a value on the heap, we can instead assign an owner to a newly allocated value instead.

```rust
let x = String::from("hello");
let y = x.clone(); // No ownership transfer, y is the owner of a new "hello"
```

By guaranteeing that a value will always only have one owner, ownership ensures that that invalid frees and undefined memory accesses never occur, as ownership allows these properties to be checked for during compile time!

See the below example of ownership.

> [!Example]+ Example: Ownership in Rust
> Because only one owner is allowed at a time, only one variable may be used to refer to variables on the heap at any given time. Consider the following example, where we bind `x` to a string allocated from the heap.
> 
> ```rust
> let x = String::from("hello"); // Allocate space on the heap for a string
> ```
> 
> After this binding, we say that `x` has ownership of the memory allocated by the string `hello`. However, if we follow this with another `let` binding
> 
> ```rust
> let y = x; // Move ownership of the string to y
> ```
> 
> Rust will perform a shallow copy on `x` (by default), and **move the ownership of `x`** to `y`, meaning we can no longer use `x` to refer to the string `hello`, as it no longer "owns" the memory!
> > If we instead perform a deep copy via `.clone()`, we won't have this issue, as `y` will point to a completely new copy of `hello`, and ownership of the original `hello` will not transfer!
> 
> Note that we have to perform a `let` binding to transfer ownership.
> 
> ```rust
> println!("{}", x); // ERROR, x no longer has ownership of "hello"
> println!("{}", y); // OKAY, y has ownership of "hello"
> ```

### References
While ownership can ensure safe programs, this constraint also severely limits the variety of safe programs we can write, and can cause unexpected behavior, like in the below example.

> [!Example]+ Example: Ownership in Rust - Unexpected Behavior
> Consider the following code.
> 
> ```rust
> fn main() {
>    let x = String::from("hello");
>    {
>       let c = x; // transfer ownership of "hello" to c
>    }
>    println!("x is {}", x); // ERROR - "hello" already freed
> }
> ```
>
> Because we move ownership of `hello` from `x` to `c` in the code block, yet do not transfer this ownership back to any other variable, `hello` is freed inside the code block! Thus, the print statement on `x` (line $L_6$) is invalid, as the memory of `hello` was already freed.

To prevent unexpected behavior like the one above, Rust provides a convenience called **references**, which allow for temporary transfers of ownership. There are two different types of references in Rust:
1. A **mutable** reference, obtained by prepending a (mutable) variable with `&mut`, which can be used to read from and write to a variable's value.
2. An **immutable** reference, obtained by prepending a variable with `&`, which can only be used to read from a variable's value.

```rust
let mut x = String::from("hello");
let b = &mut x;         // mutable reference
let c = &x;             // immutable reference
```

References for any variable must follow the below rules:
1. Every reference must be valid.
2. One of the following, but not both must be true at a single time:
   - There can be infinitely many immutable references to a value.
   - There can be only one mutable reference to a value.

Consider the following examples.

> [!Example]+ Example: References in Rust
> ```rust
> fn main() {
>    let a = String::from("hello");
>    {
>         let c = &a;
>         println!("c is {}", c);
>    }
>    println!("a is {}", a);
> }
> ```
> 
> Note that before, this example would be invalid as we never pass ownership back to `a`. However, with references, this is okay as ownership will automatically be transferred back!
>
> This would have equivalent output to the code
> ```rust
> fn main() {
>    let a = String::from("hello");
>    let b = {
>         let c = &a;
>         println!("c is {}", c);
>         c
>    }
>    println!("b is {}", b);
> }
> ```
> As in this code, we explicitly transfer ownership back out of the code block! References let us do this in a much cleaner way.

Validity of references is determined by a concept known as **lifetimes**. A reference's lifetime is an implicit parameter, that tracks the "timeframe" from which it is defined, to the **time it can be last used**. Note that a reference's lifetime may not be the same as it's scope.
> Intuitively, lifetimes tell us that **references will only be valid for as long as they need to be**.

Invalid references are determined by an overlap of lifetimes such that there is a mutable lifetime active, and any other lifetime to the same value active at the same time.

Consider the following example.

> [!Example]+ Example: Lifetimes of References
> Consider the following code block.
> 
> ```rust
> fn main() {
>    let mut a = String::from("hello");
>    {
>         let c = &mut a;
>         println!("c is {}", c); // last use of c - c's lifetime ends
>         println!("a is {}", a);
>    };
>    println!("a is {}", a);
> }
> ```
>
> Because `c` only needs to be valid for lines $L_5$ and $L_6$, and `a` only needs to be valid after that, this code is valid as the two mutable references' lifetimes do not overlap!
>
> However, if we swapped the prints on lines $L_5$ and $L_6$, our code would now be invalid, as `c` must stay valid while `a` is valid (their lifetimes overlap), meaning we have two mutable references at the same time!

Because of this concept of lifetimes, note that it is possible to have immutable references to a mutable reference, so long as their lifetimes do not overlap. Consider the following example.

> [!Example]+ Example: Lifetimes of References (2)
> Consider the following program
> ```rust
> fn main() {
>    let mut a = String::from("hello");
>    {
>         let c = &a;
>         let d = &a;
>         println!("{} and {} are the same", c, d);
>    }
>    println!("a is {}", a);
> }
> ```
>
> Even though `c` and `d` are immutable references to mutable reference `a`, the code is valid, as `a` does not need to be valid at the same time `c` and `d` are! Thus, their lifetimes do not overlap.

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

# Structures in Rust
To combine types together into a single type, Rust has a concept of **structures**. These act very similarly to classes in other languages! 

Structures in Rust are defined with the `struct` keyword, and follow the below syntax:

```rust
struct [Structure] {
       [var1]: [type1],
       [var2]:[type2],
       ...
}
```

We can also declare structures with anonymous fields as well, with `()` instead of `{}`.

```rust
struct [Structure] ( [type1], [type2], ... );
struct Anonymous (i32, i32); // Example
```

Below, we define a structure called `Shape`.
```rust
// Example Shape structure with two fields, `length` and `width`.
// Both of these fields are of type 32-bit integers
struct Shape {
       length: i32,
       width: i32,
}
```

After defining a structure type, we can create variables of that type by using its constructor, which follows syntax `[Name] { ... }`. 

```rust
// Allocates memory for a Shape structure, and assigns ownership
// to shape1.
let shape1 = Shape { length: 6, width: 4 };

// Use the .. operator to shallow copy the rest of the fields
// from another structure of the same type. 
let shape2 = Shape { length: 3, ..shape1 }; 
```

To add methods to a structure, we use keyword `impl`. Methods of instances should begin with parameter parameter `&self`, which can be used (with the `.` operator) to refer to the structure instance itself.
> The `impl` keyword can also be used to give traits to a structure, so it can implement different known attributes (like cloning!)

If the `&self` parameter is not given, then the function is treated as a method of the structure type, analogous to a class method in Java.

```rust
impl Shape {
     fn area(&self) -> i32 {
        self.length * self.width
     }

     fn hi() -> i32 {
        5
     }
}

Shape.hi();

shape1 = Shape(length: 2, width: 3);
shape1.area();
```

---

We can also declare **enumerator types**, which wrap multiple types together under one name. Defining an enumerator follows the syntax

```rust
enum [Enumerator] {
     [Type 1]
     [Type 2]
}
```

Enumerator types can also implement methods, and often find use in **pattern matching** operations, using the `match` keyword.

```rust
enum Enumerator {
     Shape(i32, i32),
     Circle(i32),
};

impl Enumerator {
     fn area(&self) -> f32 {
        match self {
              Shape::Rect(a,b) => (a * b) as f32,
              Shape::Circ(r) => r * r * 3.14
        }
     }
}
```