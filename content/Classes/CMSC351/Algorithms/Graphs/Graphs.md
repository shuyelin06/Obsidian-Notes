---
title: Graphs
tags:
- cmsc351
- wip
---

# Introduction to Graphs
A **graph** is defined as a set of **vertices (nodes)** $N$, and a set of edges  $E$ which join vertices together.

Two vertices are **adjacent** if they are joined by an edge.

The **degree** of a vertex refers to the number of edge connections it has.

A **loop** is an edge joining a vertex to itself. Note that in non-directional graphs, loops will add a degree of 2 to the vertex.

**Multiple edges** refers to 2 or more edges joining the same 2 vertices.

A graph is **simple** if it has no loops or multiple edges.

A graph is **weighted** if each edge has a positive value assigned to it.

A graph is **directed** if each edge has an associated direction.

A **walk** is a route from a starting vertex to ending vertex, following edges. In a walk, we can repeat edges or vertices.

A **trail** is a walk with no repeated edges (but repeated vertices are allowed)

A **path** is a walk with no repeated vertices.

A **cycle** is a trail with no repeated vertices except the starting vertex = the ending vertex.

A graph is **connected** if, for any 2 vertices, there exists a path between them.

A **tree** is a simple connected graph with no cycles.

## Storing Graphs
There are a couple of simple ways to store graphs.

Assume the graph is simple and unweighted.

**Adjacency Matrix**: Store a matrix of vertices such that
$$
A[i][j] = \begin{cases}
                1 & \exists \text{edge between } i,j \\
                0 & \text{otherwise}
        \end{cases}
$$
> Note that in a undirected graph, these matrices are symmetric.

**Adjacency List (of Lists)**: Create a list of lists, with $V$ entriessuch that
$$
A[i] = \text{list of vertices that i is adjacent to}
$$
> Note that here, if we're at a vertex, we have immediate access to adjacent vertices.

Consider the code
```
for x in vertices:
    for all_edges:
        ...
```

If we have an adjacency matrix, we'll take $n$ to find adjacencies as we must scan through every 0 and 1. In an adjacency list, however, we have "immediate" access to vertices, which gives us $1$ in the best case, and $n$ in the worst case.. However, if we be sneaky, we can see that the inner loop will take $2E$ time, giving us time $\Theta(V + 2E)$.

# Shortest Path Algorithm
WIP

Gives us
$$
\Theta(V + E)
$$

Take the shortest path algorithm. Notice that if we remove the return, and return pred, we still get $\Theta(V + E)$, and pred will contain ALL predecessors necessary to construct shortest paths!

# Breadth First Search
Given a graph and a starting vertex $S$, we wish to visit ALL vertices, but visit those closest to $S$ first.

We need to make the changes:
- Remove the distance list, and replace it with a visited list of ooleans whic store if we've visited a vertex or not.
- Remove the predecessor list.
- Introduce a list order which stores the order in which we visit / traverse the nodes.

# Depth First Search
Given a graph and a starting vertex $S$, we want to visit ALL vertices, by going as far as possible, then backing up to a junction where we can go deep again if we cannot go any further.

Some sources say the time complexity of depth first search is $\Theta(V + E)$. They're wrong! Consider the following example:

Consider a graph with $V$ vertices, where every vertex is connected to one another (a complete graph). For every vertex we visit, notice that we push $n-1, n-2, n-3, \dots$ vertices onto our stack. Thus, we will have to inevitably pop $\Theta(v^2)$ from our stack. This gives us $\Theta(V^2 + E)$

The problem with this is that we're allowing more than one thing on the stack. Thus, we need a hashset or something!

We want to get around this - so, let's say we're about to put something on the stack. If it is, then we remove earlier occurrences! How do we do this in $\Theta(1)$ time?

We can modify the stack to also be a doubly-linked list, so we can delete from the stack in $\Theta(1)$ time. Then, we create a list of pointers indexed by vertex, such that the pointers will point to the FIRST occurrence of the vertex. They're initially NULL, but after their respective vertex, they point to this vertex.
> This way, we can easily check if some vertex is on the stack, and delete it if we have a duplicate.

> Note that while we could do a hashmap, this is better as hashmaps have a worst case of $\Theta(n)$ on conflict! (Also the hashing can take time)

This will give us our desired $\Theta(V + E)$ time, as now our outer look will iterate exactly $V$ times, and the inner loop will iterate $2E$ times.

