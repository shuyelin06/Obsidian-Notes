---
title: Smart Pointers in Rust
tags:
- cmsc330
- wip
---

Recall that in [[Memory Safety in Rust]], we can create what are essentially "pointer types" in Rust using references (`&`).

# Smart Pointers (WIP)

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

