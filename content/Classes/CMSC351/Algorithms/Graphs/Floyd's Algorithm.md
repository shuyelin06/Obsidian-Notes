---
title: Floyd's Algorithm
tags:
- cmsc351
---

**Problem**: Given a directed, weighted, simple, and connected graph, how can we find the shortest path between **any two pairs of vertices**?

# Intuition
Consider the following graph.

```mermaid
graph LR
1 -. 20 .-> 2;
3 -. 80 .-> 2;
2 -. 10 .-> 3;
3 -. 40 .-> 1;
```

We can find the shortest path between any two pairs of vertices, by starting from all known edges, and working our way to our shortest path by allowing "intermediate" vertices one by one! See below to see what we mean.

First, we build adjacency matrix $A$ for our graph, defined as
$$
A =
\begin{bmatrix}
        0 & 20 & \infty \\
        \infty & 0 & 10 \\
        40 & 80 & 0 \\
\end{bmatrix}

\qquad

d[i,j] =
\begin{cases}
        x & \text{Weight from} \; i \to j \\
        0 & i = j \\
        \infty & \text{No edge}
\end{cases}
$$

While this matrix stores the edges and their weights in the graph, we can alternatively think of $d[i,j]$ it as storing the weight of the shortest path from $i \to j$, **allowing no intermediate vertices** (i.e. paths of only 1 edge). We can then let each vertex $1,2,3$ be intermediate vertices, and build our matrix to obtain the shortest paths between any two pairs of nodes. 

Now, let's do the following:
1. Let 1 be an intermediate vertex. Then, this changes the shortest path from $3 \to 2$ to 60, because we can traverse through 1. More formally, we update $d[3,2]$ because
   $$
   d[3,1] + d[1,2] < d[3,2]
   $$
   We then update our matrix, giving us a matrix whose $d[i,j]$ yields the shortest paths allowing 1 as an intermediate vertex! We'll call this the **pass by 1 matrix**.
   $$
   \begin{bmatrix}
        0 & 20 & \infty \\
        \infty & 0 & 10 \\
        40 & 60 & 0 \\
   \end{bmatrix}
   $$
2. Let's repeat this process, now allowing 2 to be an intermediate vertex. Now the shortest path from $1 \to 3$ actually appears, as we can take 2 to go to 3. More formally,
   $$
   d[1,2] + d[2,3] < d[1,3]
   $$
   We again update our matrix, giving us a matrix whose $d[i,j]$ yields the shortest paths allowing 1 and 2 as intermediate vertices. We'll call this the **pass by 2 matrix**.
   $$
   \begin{bmatrix}
        0 & 20 & 30 \\
        \infty & 0 & 10 \\
        40 & 60 & 0 \\
   \end{bmatrix}
   $$
3. We repeat this with 3, allowing 3 to be an intermediate vertex. Now, the shortest path from $2 \to 1$ appears, as we cant take 3 to go to 1. More formally,
   $$
   d[2,3] + d[3,1] < d[2,1]
   $$
   Updating our matrix, we get a matrix whose $d[i,j]$ yields the shortest paths allowing 1,2, and 3 all as intermediate vertices. We'll call this the **pass by 3 matrix**.
   $$
   \begin{bmatrix}
        0 & 20 & 30 \\
        30 & 0 & 10 \\
        40 & 60 & 0 \\
   \end{bmatrix}
   $$

Now, because we've allowed all vertices as intermediate vertices, our matrix yields the lengths of all shortest paths! We now define another matrix to find the actual shortest path between vertices.

Define matrix $P$ such that
$$
P =
\begin{bmatrix}
        1 & 1 & \text{NULL} \\
        \text{NULL} & 2 & 2 \\
        3 & 3 & 3 \\
\end{bmatrix}
\qquad 
p[u,v] =
\begin{cases}
        u & \text{For every edge} \; u \to v \\
        v & \text{For every vertex} \; v
\end{cases}
$$

We will use this matrix to tell us the direct predecessor of $j$ in the shortest path from $i \to j$. Currently, it allows no intermediate vertices.

We'll process this graph in a similar way to $A$.
1. Let 1 be an intermediate vertex. Then, we see that the shortest path from $3 \to 2$ changes because instead of taking the path $3 \to 2$, we can instead take $3 \to 1 \to 2$. In other words,
   $$
   d[3,1] + d[1,2] < d[3,2]
   $$
   So $p[3,2] = p[1,2] = 1$, because the direct predecessor in this path is the same as the direct predecessor in the path $1 \to 2$, which is 1. While this process may seem redundant, it paves the way for an algorithm later!
   $$
   P = 
   \begin{bmatrix}
        1 & 1 & \text{NULL} \\
        \text{NULL} & 2 & 2 \\
        3 & 1 & 3 \\
   \end{bmatrix}
   $$
2. Let 2 be an intermediate vertex. Then, we see that the path $1 \to 3$ opens because we can take the path $1 \to 2 \to 3$. In other words, becaus $d[1,3] = \infty$,
   $$
   d[1,2] + d[2,3] < d[1,3]
   $$
   So $p[1,3] = p[2,3] = 2$ as the direct predecessor of $3$ in our new path is intermediate vertex 2.
   $$
   P = 
   \begin{bmatrix}
        1 & 1 & 2 \\
        \text{NULL} & 2 & 2 \\
        3 & 1 & 3 \\
   \end{bmatrix}
   $$
3. Let 3 be an intermediate vertex. THen, we see that the shortest path from $2 \to 1$ changes as instead of taking the path $2 \to 1$, we can instead take path $2 \to 3 \to 1$. In other words,
   $$
   d[2,3] + d[3,1] < d[2,1]
   $$
   So $p[2,1] = p[3,1] = 3$, because the direct predecessor of 1 in this new path is now intermediate vertex 3. 
   $$
   P = 
   \begin{bmatrix}
        1 & 1 & 2 \\
        3 & 2 & 2 \\
        3 & 1 & 3 \\
   \end{bmatrix}
   $$

We are done! Now, our $P$ stores the direct predecessor of $j$ in the shortest path from $i \to j$, allowing all intermediate vertices! To reconstruct a path, we start at a cell, and work backwards.

For example, suppose we wanted to know the path from 2 to 1. Then, we see that:
- Because $p[2,1] = 3$, the shortest path from 2 to 1 has direct predecessor 3.
- Furthermore, because $p[2,3] = 2$ we know that there are no other nodes in shortest path, because our starting node is equal to our predecessor.

This gives us shortest path
$$
2 \to 3 \to 1
$$

# Floyd's Algorithm
## Pseudocode
Let's now implement this algorithm in code. While we defined and created two arrays separately above, we can actually create both of them at the same time in code!

Let `graph` have $V$ vertices. Then, we have the following pseudocode:

```python
def floyds(graph):
    A = adjacency_matrix(graph) # V x V
    P = predecessor_matrix(graph) # V x V

    # iterate through all intermediate vertices
    for intermediate in vertices(graph): 
        # iterate through all possible paths
        for start in vertices(graph): # choose start of path
            for end in vertices(graph): # choose end of path
                # see if taking the intermediate yields a shorter path
                if A[start][intermediate] + A[end][intermediate] < A[start][end]:
                   # update weight
                   A[start][end] = A[start][intermediate] + A[end][intermediate]
                   # update predecessor
                   P[start][end] = P[intermediate][end] 

    return P
```

## Time Complexity
Let's analyze this algorithm for its time complexity.
- We see that our array initialization on lines $L_2$ and $L_3$ both take $V \times V$ time.
- Furthermore, the loops on lines $L_6, L_8, L_9$ all take $V$ time, giving us complexity $V^3$.

This gives us total time complexity
$$
\Theta(V^3)
$$