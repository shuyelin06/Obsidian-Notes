---
title: User-Defined Types in Rust
tags:
- cmsc330
---

While Rust has numerous base types, we can create types of our own for our programs!

This article describes how we can create types of our own in Rust, focusing on Rust's **structures** and **enumerators**. 

# Structures in Rust
In Rust, we can create **structures**, which group multiple datatypes together under one type. To create a structure, we use the `struct` keyword. For example, below we define a structure `Shape`.

```rust
struct Shape {
       length: i32,
       width: i32,
}
```

After defining a structure, we can create instances of the structure by using its constructor, through syntax `[Name] { ... }`. For convenience, we can also use the `..` operator to shallow copy fields from another structure instance.

When we have an instance of a structure, we can use the dot operator (`.`) to access specific fields of the structure.

```rust
let shape1 = Shape { length: 6, width: 4 };
let x = shape1.length; // x = 6

// Shallow copy remaining fields from shape1 (width)
let shape2 = Shape { length: 3, ..shape1 };
let y = shape2.width; // y = 4
```

If we want to avoid using named fields, we can also declare **anonymous structures**, which are structures with anonymous (non-named) fields. To do this, we use `( )`. See the below example.

```rust
// struct [Structure] ( [type1], [type2], ... );
struct Anonymous (i32, i32);
```

> [!Note] Note: Generic Types
> In addition to the normal structure definition, we can also use the `< >` brackets to specify generic types.
>
> ```rust
> struct Example_Structure<T> {
>        field: T,
> }
> ```

# Enumerators in Rust
We can also create **enumerators** in Rust, which specify the various values some type can take on. Enumerators can create types that wrap other types under one name, and to create an enumerator, we use the `enum` keyword.
> It is often the case that we find anonymous structures (discussed earlier) useful in enumerators.

```rust
// enum [Enumerator] { [Value], [Value], ... }
enum Shape {
     Box(i32),
     Circle(i32)
}
```

To define a specific type from an enumerator, we can use the `::` operator.

```rust
let shape = Shape::Box(2); // Define Box
let shape2 = Shape::Circle(3); // Define Circle
```

Enumerators are often useful in **pattern matching operations** using the `match` keyword, where we can specify behaviors depending on the type wrapped by an enumerator. We can use pattern matching operations to conveniently extract the fields from an anonymous structure, following syntax `Type(Field1, Field2, ...)`.

```rust
// match [Variable] { [Type] => [Behavior], [Type] => [Behavior], ... }
match shape {
      Shape::Box(x) => x,       // If Shape::Box type
      Shape::Circle(x) => x * 3 // If Shape::Circle type
}
```

# Implementations for Types
## Implementations
Rust types are similar to classes like in other languages, as they can also implement methods which use the instance of some type, or are based on the type itself.

> [!Warning]
> These qualities of Rust types does not mean that Rust is an object orientated programming language! Rust types lack any concept of inheritance and polymorphism.

To add methods to a type, we use keyword `impl` to define implementations (functions) for the type.

To create a method of an instance, the corresponding function should begin with `&self` or `&mut self` as the first parameter, which can be used to refer to the instance itself. Without a reference to `self` as the first parameter, the function is treated as a method of the structure type itself.

For example, consider our `Shape` structure from before. We can define methods as follows:

```rust
// impl [Structure] { [Function Definitions] } 
impl Shape {
     // Structure method
     fn new(x: i32, y: i32) {
        return Shape { width: x, length: y };
     }
     
     // Instance method
     fn area(&self) -> i32 {
        // Use . to access fields of the instance
        return self.width * self.length; 
     }
}
```
> Note that we can also implement methods for specific variations of a generic structure (if we specify what the generic type is), in the exact same way.

## Traits
While `impl` can define implementations for different types, it can also be used to define higher level abstractions!

In particular, we can use `impl` to implement interfaces of functions, known as **traits**, for a type. These let us define groups of behaviors, that a type must have if they are implementing the trait.
> This is analogous to interfaces in other languages, like Java.

To define a trait, we use the `trait` keyword. For example, consider the below code, where we create a `Printable` trait.

```rust
// trait [Trait Name] { [Function Signatures] } 
trait Printable {
      fn print(&self) -> (); 
}
```

Then, we can use the `for` keyword with `impl` to define the functions for a particular trait.

```rust
// impl [Trait] for [Structure] { [Function Definitions] }
impl Printable for Shape {
     fn print(&self) -> () {
        println!("Shape - width: {self.width}, length: {self.length}");
     }
}

let s = Shape { length: 5, width: 3 };
s.print(); // Shape - width: 3, length: 5
```

Using the `impl .. for` combination, we can give structures different known attributes! This lets us guarantee properties for certain types based on their traits, which can be used to view types from a higher level abstraction!

> [!Info] Note
> Use of traits also allows compatability of our types with standard library functions. For example, some functions may expect a structure to be cloneable with the `.clone()` method, or in other words, implement the `Clone` trait!
