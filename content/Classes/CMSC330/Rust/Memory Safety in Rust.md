---
title: Memory Safety in Rust
tags:
- cmsc330
- wip
---

In lower-level langauges such as C, the low level accesses to memory that we can do can provide a lot of versatility and flexibility. However, at the same time, this allows for lots of unsafe code! In particular, there are a variety of **unsafe memory operations** that we can do, and these operations can cause undefined behavior!

Two common unsafe memory operations we can accidentally do are given as follows:
- **Type Unsafe Operations**: The accessing and use of memory whose type differs from the expected type.
- **Temporally Unsafe Operations**: The accessing and use of memory not allocated, or already freed by the program.

The Rust compiler avoids these issues by adding a constraint to the compiler to ensure memory safe programs. To do this, Rust adheres to two key concepts: **ownership** and **lifetimes**, described below.
> However, as a result of this convenience, there are a subset of safe programs that Rust will not be able to compile!


# Ownership
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
> Intuitively, we can think of this as if the value of a "pointer type" gets copied on the stack, then the ownership will transfer.

Transfer of ownership can be avoided through use of deep copies (through the `.clone()` method, see #needs_link), which will duplicate memory allocated on the heap! Instead of transferring ownership of a value on the heap, we can instead assign an owner to a newly allocated value instead.

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

# References
## Rules of References
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
1. A **mutable reference**, obtained by prepending a (mutable) variable with `&mut`, which can be used to read from and write to a variable's value.
2. An **immutable reference**, obtained by prepending a variable with `&`, which can only be used to read from a variable's value.

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

When we define a reference, Rust will attempt to fit the program to match the above rules. It will treat the owner of the value differently, depending on the references that exist.
- If there exists an immutable reference, the owner is also treated as an immutable reference.
- If there exists a mutable reference, the owner is temporarily treated as invalid.

> Only when one of the rules cannot be matched, will the Rust compiler throw an error.

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

## Lifetimes of References
Validity of references is determined by a concept known as **lifetimes**. A reference's lifetime is an implicit parameter, that tracks the "timeframe" from which **it is first defined**, to the **time it can be last used**.
> Intuitively, lifetimes are the block in which references are used for - the concept of lifetimes tells us that **references will only be valid for as long as they need to be**.

> [!Info] Note: Lifetime vs. Scope
> As a reference may not necessarily be used for the entire scope for which it is defined, a reference's lifetime may not be the same as it's scope. Think about them as two distinct concepts. 

Recall our rules of references. To check that these rules are met, the Rust compiler refers to the references' lifetimes. Below list the checks the compiler perfroms for each rule (in order of how we defined the rules).

| Rule | Lifetime Check |
| - | - |
| Every reference must be valid. | A variable's lifetime must encapsulate the lifetime of all references created from it. |
| At a single time, there can only be many immutable references, or only one mutable reference. | The lifetime of a mutable reference cannot overlap with the lifetime of another reference. | 

Consider the following example.

> [!Example]+ Example: Lifetimes of References
> Consider the following code block. Despite there being two mutable references in the same scope, the code is still valid, as the lifetimes of the references do not overlap.
> 
> ```rust
> fn main() {
>    let mut a = String::from("hello");         // a's lifetime begins
>    {
>         // Mutable reference c, a is temporarily invalid
>         let b = &mut a;                       // b's lifetime begins
>         println!("b is {b}");                 // b's lifetime ends
>
>         let c = &mut a;                       // c's lifetime begins
>         println!("c is {c}");                 // c's lifetime ends
>    };
>    println!("a is {}", a);                    // a's lifetime ends
> }
> ```

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

While Rust is typically pretty good at inferring the correct lifetimes during compilation, in some cases we need to tell it what we're expecting. To do this, we use **lifetime annotations**, which follow the format

```rust
&'[name] x
```
> Typically, we use lowercase characters (`a`, `b`, `...`) to denote lifetimes.

Annotations do not change any lifetimes - rather, they tell the rust compiler what we are expecting!

This becomes particularly important in some particular use-cases for references:
1. Returning references from functions
2. Creating structs with references

As the former is much more common, we focus on using references in functions below.

### References in Functions
When writing functions, Rust will automatically attempt to infer the lifetimes of references, using rules known as **lifetime elisions**. This is mainly done for convenience, and in these cases, we don't need to specify any explicit lifetimes. These rules are given as follows.

1. If the output does not contain a reference, then for every input reference (to a function), Rust will assume that the references could have different lifetimes. 
   ```rust
   // rust assumes the following:
   fn example<'a,'b>(x:&'a str, y:&'b i32) -> i32 {
      // ...
   }
   ```
2. If the output contains a reference, and there is only 1 input reference, then the lifetime of the return value is the same as the input.
   ```rust
   // rust assumes the following:
   fn example<'a>(x:&'a str) -> &'a str {
      // ...
   }
   ```
3. If the output contains a reference, and there is more than 1 input reference, but one of them is `&self` (or `&mut self`), then the return value has the same lifetime as `self`.
   ```rust
   // rust assumes the following:
   fn example<'a,'b,'c>(&'a self, x:'b i32, y:&'c str) -> &'a str {
      // ...
   }
   ```



In the case that none of the 3 rules match, however, we'll have to explicitly provide the lifetime annotations ourselves, to tell Rust about the lifetime of the output reference.

> [!Info] Note: Criteria for Explicit Lifetime Annotation
> Note that by these elision rules, it's only necessary to add explicit lifetimes for functions that meet the following:
> - The function returns a reference type (fails to match rule 1)
> - The function has multiple input references (fails to match rule 2)
> - The function is not an object method (fails to match rule 3)
>
> If any of these 3 cases are not met, then explicit annotation of lifetimes is unnecessary!

These annotations tell the compiler how long we expect the reference output should be able to live, relative to its input parameters. This way, we avoid any future cases of invalid reference usage.

To annotate lifetimes, we'll also need to include the `< >` notation after the function name, to tell it the various distinct lifetimes that exist in the function. Consider the following examples.

> [!Example]+ Example: Explicit Lifetime Annotations
> ```rust
> // The output should live at least as long as x exists
> fn function<'a, 'b>(x: &'a str, y: &'b str) -> &'a str {}
> 
> // The output should live at least as long as both x and y exist
> fn function<'a>(x: &'a str, y: 'a str) -> &'a str {}
> ```