---
title: Graph Traversal
tags:
- cmsc351
---

For any algorithm utilizing (or manipulating) a graph to determine a solution, we need to be able to traverse through all vertices of the graph to do some process. We will define this process as the act of **visiting** a vertex, and ask for the various ways we can visit all vertices in a graph once.

In this article, we briefly describe the two most common ways of graph traversal, namely, **breadth first traverse (search)** and **depth first traverse (search)**.

# Breadth First Traverse
Suppose we have a graph $G$ and a starting vertex $s$. To traverse this graph using a **breadth first traverse (search)**, we first visit all vertices connected to $s$, then all vertices connected to those, and so on and so forth.
> Intuitively, we can think of this as covering (visiting) the entire graph through layers of increasing distance from $s$.

To peform a breadth first traverse, we do the following.

First, we set up:
- A queue $Q$ with initial value $s$
- A boolean list tracking whether a vertex has been visited or not, with $s$ marked as being visited.
- A list containing the order in which we visit vertices.

Then, we repeat the following. Until the queue is empty,
1. First, we dequeue the first element from our queue, say $x$.
2. Then, we find all vertices adjacent to $x$ that haven't been visited, place them in $Q$, and update our visited and visit order arrays.

Consider the following example. Note that when finding adjacent vertices, we will visit them in increasing order to remove ambiguity.

> [!Example] Example: Breadth First Traverse
> ```mermaid
> graph LR
>    0 -.- 1 & 4 & 5;
>    1 -.- 2 & 3;
>    3 -.- 5 & 6 & 7;
>    5 -.- 6;
> ```
>
> Performing a Breadth First Search starting at 0, we obtain final order
> $$
> [0,1,4,5,2,3,6,7]
> $$

Pseudocode for our algorithm is given below.

```python
def bft(graph, start):
    queue = [s]
    visited = list of False of length V
    visited[s] = True
    vorder = [s]

    while len(queue) > 0:
       x = queue.dequeue()
       for all y adjacent to x:
           if not visited[y]:
              queue.enqueue(y)
              visited[y] = True
              vorder.append(y)

    return vorder
```

Analyzing the time complexity of breadth first traverse, we find that:
- We dequeue and enqueue every vertex exactly once, for a total of $V$ times.
- We check all edges in the graph to find its neighbors, and as the graph is undirected, this is $2E$.

This gives us time complexity of $\Theta(V + 2E)$.


# Depth First Traverse
Suppose we have a graph $G$ and a starting vertex $s$. To traverse this graph using a **depth first traverse (search)**, we first move along one path as far as possible, before backtracking and trying another path. 

> [!Example] Depth First Traverse
> ```mermaid
> graph LR
>    0 -.- 1 & 4 & 5;
>    1 -.- 2 & 3;
>    3 -.- 5 & 6 & 7;
>    5 -.- 6;
> ```
>
> Performing a Breadth First Search starting at 0, we obtain final order
> $$
> [0,1,2,3,5,6,7,4]
> $$

Depth first traverse can be done both iteratively and recursively. We discuss both implementations below.

## Recursive Implementation
To implement depth first traverse recursively, we take advantage of the fact that recursion naturally allows us to backtrack nodes.

```python
vorder = []
visited = []

def dft(graph, node):
    vorder.append(node)
    visited[node] = True
    for all adjacent nodes y:
        if not visited[y]:
           dft(graph, y)
```

Analyzing the time complexity of this code, we see that we will process a total of $V$ nodes, and iterate over a total of $2E$ edges. This, like breadth first search, will give us $\Theta(V + E)$.

## Iterative Implementation
To implement depth first traverse iteratively, we will have to use our own data structure to allow for backtracking. Commonly, this is done using a stack.

```python
def dft(graph, start):
    vorder = []
    visited = []
    stack = [start]
    
    while len(stack) > 0:
       node = stack.pop()
       
       if not visited[x]:
          visited[x] = True
          vorder.append(x)
          
       for all nodes y adjacent to x:
          if not visited[y]:
             stack.append(y)

    return vorder
```

This, like the recursive definition will also yield a time complexity of $\Theta(V + E)$.

This can lead us to assume that the iterative and recursive solutions are the same, but this is misleading! Consider a graph with $V$ vertices, where every vertex is connected to every other vertex. Then, discluding the addition of our starting vertex to the stack, for every additional vertex we visit, we will add
$$
(V - 1) + (V - 2) + \dots + 2 + 1 + 0 = \frac{V(V-1)}{2}
$$
vertices total to our stack, meaning that our `while` loop will actually run $\Theta(V^2)$ times! Thus, in this case, we will actually have a time complexity of $\Theta(V^2 + E)$.
> We can avoid this problem with other iterative implementations, and while that's not discussed here, it's important to understand this slight nuance.