---
title: Graphs
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