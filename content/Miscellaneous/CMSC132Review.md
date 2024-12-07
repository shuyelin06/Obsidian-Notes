---
title: CMSC132Review
---

Message me if you have any questions!

# Conceptual Review Questions
## OOP / Java Concepts
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

## Linked Lists
### 8. How does storing a list in an array compare with using a linked list (i.e., what are the advantages and drawbacks of each)?

### 9. How does a singly–linked list compare with a doubly–linked list (advantages and disadvantages of both)?

## Equals
### 10. What are two differences between using instanceof and getClass()in an equals() method?

###  11. What is the reason that the parameter of an equals() method should be of type Object?

## Binary Search Trees
###  12. Describe what amortized cost is.

### 13. In the average case, what is the complexity of inserting a value into a binary search tree?

### 14. In the average case, what is the complexity of searching for an element in a binary search tree?

### 15. What is the worst–case complexity of searching for an element in a binary search tree?

### 16. What causes the worst–case behavior of searching for an element in a binary search tree?

### 17. What is the average case complexity of deleting an element from a binary search tree?

### 18. Why did we not have to do anything to prevent a tree traversal from processing the same elements more than once?

## Heaps
### 19. Explain how the heap getSmallest() operation works.

### 20. Give the formula for finding the parent of the element at position of a heap that is stored in an array.

### 21. Give the formula for finding the left child of the element at position of a heap that is stored in an array.

### 22. Give an operation that is usually efficient for a binary search tree that is not efficient for a heap

### 23. On average, what is the complexity of inserting an element in a heap?

### 24. How do external files compare with storing data in data structures in memory?

## Input / Output
### 25. What is buffering, and why is it used?

## Hashing
### 26. Explain how insertion in linear probing works. (Just ignore here the possibility of a hash table filling up.)

### 27. Explain how lookup in linear probing works.

### 28. Explain how deletion in linear probing works.

### 29. Explain how double hashing works compared to linear probing.

### 30. Explain what a compression function is, and why it’s needed.

### 31. Explain why Math.abs()was used with the result of a compression function in the lecture slides. Is there any case where this would be unnecessary?

### 32. What does Java’s hash code contract say?

### 33. How could a class violate Java’s hash code contract?

### 34. What can happen if a class violates Java’s hash code contract?

### 35. What has to happens when a hash table that uses open addressing (the open addressing hashing methods we discussed were probing and double hashing, as opposed to chained hashing) is full (or close to full), if we want to increase its size so more data can be stored?

### 36. What property (or properties) would make a hash function be good?

### 37. What property (or properties) would make a hash function be invalid (it could not be used at all for hashing)? (We are talking about hashing in general, not specifically Java’s library classes that use hashing, so Java’s hash code contract is not relevant.)

## Graphs
### 38. Define a path in a graph.

### 39. Define a cycle in a graph.

### 40. Why is graph traversal more difficult than tree traversal?

### 41. Suppose you have to construct a moderately–sized graph (not extremely large) by adding its vertices and edges, then you have to do many traversals of the graph. Which graph representation(s) would be better to use in this situation?

### 42. Now suppose you have to construct a moderately–sized graph (not extremely large) by adding its vertices and edges, and following that, a number of edges have to be removed, and new ones added, in various orders. Finally, when these modifications are done, you want to do one traversal of the resulting graph. Which graph representation(s) would be better to use in this situation?

## Threading
### 43. What is synchronization?

### 44. What are some reasons to use multithreading?

### 45. How do threads differ from processes?

### 46. What’s one reason it could be better to implement the Runnable interface for creating threads, rather than extending the Thread class?

### 47. How do you specify what code a Java thread should execute?

### 48. What do you do to cause a thread to begin running?

### 49. When does a Java thread finish executing?

### 50. When does an entire threaded Java program finish executing?

### 51. What are some possible states for Java threads?

### 52. What can cause a thread to be in the blocked state?

### 53. What can cause a thread to stop being in the blocked state?

### 54. When a thread finishes being blocked what happens to it then?

### 55. What does scheduling refer to?

### 56. What does dispatching a thread mean?

### 57. What is a time slice?

### 58. Suppose a program’s main() method calls start() once (on a thread object). How many threads does the program have running then?

### 59. What is the effect of the Thread class join() method?

### 60. What is a data race?

### 61. What is mutual exclusion?

### 62. What are locks in Java, and what are they used for?

### 63. What does the synchronized keyword do in Java? 

### 64. What happens if a thread tries to execute a synchronizedblock that another thread is already executing? (Suppose that the two synchronizedblocks are synchronizing on the same object.)

### 65. True or false, and explain your answer: when a thread has an object’s lock it means that no other thread can be executing any code concurrently)

### 66. Suppose a thread that has a lock loses its execution time (meaning the scheduler switches to running another thread). What happens with the lock while the thread that has it is not running?

### 67. Can different threads get a lock at the same time? Can different threads get different locks at the same time? And can the same thread get different locks at the same time?

### 68. What is deadlock?

### 69. Under what conditions can we be positive that deadlock will not occur in a concurrent program? (There may be different conditions in which we know that deadlock can’t happen.)

### 70. Why weren’t all of the Java library data structures (collections) written to be thread–safe?

## Sorting
### 71. What does it means to say that a sorting algorithm is in–place?

### 72. What does it means to say that a sorting algorithm is stable?

### 73. What does it means to say that a sorting algorithm is a comparison sort?

### 74. Suppose Elon Musk told you that due to his incredibly massive brain (equaled only by his incredibly massive ego) he just invented a sorting algorithm called TwitSort that would sort any data in O(log(n)) time. What would you say about Mr. Musk’s claim? (And what would you say about Mr. Musk’s ego?)
