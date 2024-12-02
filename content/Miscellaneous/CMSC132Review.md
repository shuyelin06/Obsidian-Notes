---
title: CMSC132Review
---

# Conceptual Review Questions
## December 2, 2024 Discussion
### 1. What types of methods can static fields be accessed in?
Any methods in the class

### 2. What types of methods can nonstatic fields be accessed in?
Any non-static methods. 

### 3. Describe the three levels of copying objects.
1. **Reference Copy**: Reassigning references, same object. For example:
2. **Shallow Copy**: We make a new object, but all fields are reference copied (or copied if primitive).
3. **Deep Copy**: We make a new object, but new objects are made for each field as well (if they're references). 

### 4. How does an abstract class compare to an interface?
- **Similarities**: 
  - Both abstract classes and interfaces cannot have instances. In other words, we cannot call `new Interface()` or `new Abstract Class()`.
    > This is NOT the same as having **references** to interfaces / abstract classes. `Interface a = ...` is okay.
- **Differences**:
  - Interfaces cannot have instance fields. They can only have methods.
  - You `extend` an abstract class, and `implements` an interface. 

### 5. What is the difference between a checked and an unchecked exception in Java?
You MUST catch or throw a checked exception, but you do not have to do this for an unchecked exception.

### 6. In what ways can a generic type variable be used inside a class, and how can it not be used?
- **What We CAN Do**:
  - Can use it as a parameter, return value, field, etc.
  - We can always call Object methods on a generic type, or if the generic type is bounded, 
    ```java
    class Example<T extends AnotherClass>
    ````
    can use methods of that class (or any superclass of that class).
- **What We CANNOT Do**: 
  - Can't call a constructor for a generic type (`new T()`)

### 7. What is the advantage of using generics in Java, as opposed to code that just uses Object references to refer to different types of things?
- Any mistakes will be caught at compile time
- No need to explicitly cast types (which is ugly and inconvenient)
- Promotes code reuse


