---
title: Graph Traversability
tags:
- math475
---

# Section 4: Graph Traversability
There are two notions of traversability-- traversing through all the vertices, or all the edges.

## 4.1: Eulerian Graphs
We ask: Can we begin at a vertex in a graph, and traverse all **edges** exactly once?
> It's okay to repeat vertices!

If the start and end vertex are different, it is a **Eulerian Trail**. Otherwise, if they are the same, it is a **Eulerian Circuit**, and we say $G$ is **Eulerian**.

> [!Example]+ Example: Eulerian Trails
> ```mermaid
> graph LR
> 1 o--o 2 & 3;
> 2 o--o 4 & 5;
> 3 o--o 4 & 5;
> 4 o--o 5;
> 2 o--o 3;
> ```
> 
> An eulerian trail exists, but NOT an eulerian circuit. One possible trail is given as follows:
> $$
> 5 \to 3 \to 1 \to 2 \to 3 \to 4 \to 5 \to 2 \to 4
> $$

> [!Example]+ Example: Lack of Eulerian Trail
> ```mermaid
> graph LR
> 1 o--o 2 & 2 & 3;
> 2 o--o 3 & 4 & 4;
> 3 o--o 4;
> ```
> This is a graphical representation of the "Seven Bridges of Konigsberg".
> 
> There does not exist any possible eulerian or trail circuit for the graph. 

> [!Abstract] Theorem
> Let $G$ be a connected (multi) graph. Then, $G$ is Eulerian if and only if every vertex has an even degree.
> 
> > [!Note]- Proof
> > 
> > #### Proof $\rightarrow$
> > Given a Eulerian circuit, take an intermediate vertex in the circuit. Our first encounter with the vertex is "in", and we must go "out" since this is NOT the start / end vertex. 
> > 
> > We find that the total in's must equal the total out's, so there must be an even number of edges incident to the vertex.
> > 
> > For the starting vertex, our first encounter is "out", and we must go "in". Along the same logic, this vertex must have an even number of edges.
> > 
> > #### Proof $\leftarrow$
> > Consider a $uv$-trail of maximum length. We show that it must be closed, i.e. $u = v$, so it is a circuit.
> > 
> > Observe if $u \ne v$, ending at $v$, the first encounter is "in". We end at $v$, so there will be 1 more "in" than "out", meaning $v$ cannot have an even degree. Because $v$ does have an even degree, however, there must be one more "out" we can take, some $v \sim w$ NOT in the trail! This contradicts our claim that the $uv$ trail is of maximum length, so $u = v$, giving us a circuit.
> > 
> > Now, $C$ be a circuit of max length, and assume $x \sim y$ is NOT in the circuit, with $x$ in $C$. Now consider $H = G / E(C)$, the graph without edges in $C$. Let $H_1$ be the component containing $x \sim y$. 
> > 
> > Create a trail in $H_1$ of max length, and repeat the above argument to show that we must have a circuit. Now, append this circuit onto our original circuit $C$ to get a new (and longer) circuit. This contradicts that $C$ is the longest length circuit, so there cannot possibly be any $x \sim y$ not accounted for in the circuit!
>
> > **Corollary**: Graph $G$ has an Eulerian trail if and only if exactly 2 vertices have odd degree.

> [!Example]- Example: Eulerian Proof
> Let $G$ be a connected $r$-regular graph that is not Eulerian. Suppose $\bar{G}$ is also connected. Prove that either $G$ or $\bar{G}$ must be Eulerian.
>
> Suppose $G$ is Eulerian. We are done.
>
> Suppose $G$ is not Eulerian. Then, $\exists v \in V(G)$ such that $\deg{v} = r$ odd. So, $G$ is an odd-regular graph. 
>
> If $G$ is an $r$-regular graph, then $\bar{G}$ is a $n - 1 - r$ regular graph, meaning $n - 1 - r$ is even. So, all vertices in $\bar{G}$ have an even degree, meaning $\bar{G}$ is Eulerian. 

## 4.2: Hamiltonian Graphs
We ask: Can we begin at a vertex in a graph, and traverse all **vertices** exactly once? 
> We cannot repeat any vertices or edges! We don't have to use all the edges, however.

A **cycle** (no vertex repeated except the start and end) in graph $G$ that contains every vertex is known as a **Hamiltonian cycle** of $G$, and if such a cycle exists we say $G$ is **Hamiltonian**.

A **Hamiltonian path** is a path containing all vertices.

Let $c (G / S)$ be the total components of graph $G$ after deleting vertex set $S$ and all edges incident to these vertices.

A graph $G$ is **$t$-tough** if 
$$
t \le \frac{|S|}{c(G / S)}
$$
For every $S \subseteq V(G)$ that disconnects $G$. The **toughness** of $G$ is the smallest $t$ for which $G$ is $t$-tough,
$$
t(G) = \min_{S \subseteq V(G)} \frac{|S|}{c (G/S)}
$$
Intuitively, the toughness value $t(G)$ of a graph is small if we can delete only a few vertices, and separate the graph into many disconnected components. 
> Deleting a few vertices breaks the graph up into many subcomponents!

> [!Example] Example: Toughness in the Petersen Graph
> ```mermaid
> graph LR
> 1 o--o 6;
> 2 o--o 7;
> 3 o--o 8;
> 4 o--o 9; 
> 5 o--o 10;
> 1 o--o 2 o--o 3 o--o 4 o--o 5 o--o 1;
> 6 o--o 7 o--o 8 o--o 9 o--o 10 o--o 6;
> ```
> 
> If we delete 7 vertices: 1, 3, 6 to 10, we get 2 components. Then, the toughness we calculate from this is $\frac{7}{2}$, which is an **upper bound** of the graph's actual toughness (maybe we can find a value smaller!)
>
> Similarly, we could delete 4 vertices to get 3 components, giving us toughness $\frac{4}{3}$! It can actually be proven that this is the minimum.
> > This graph is a very common "counterexample" for many claims in graph theory!

> [!Abstract] Theorem
> The toughness of the Petersen Graph is $\frac{4}{3}$.
>
> This means that the Petersen Graph is 1-tough, 1/2-tough, etc.

We define toughness, as we may be curious in finding if a Hamiltonian cycle can be found given some toughness of the graph!

> [!Abstract] Theorem: Necessity Condition for Hamiltonian Graphs 
> If $G$ is Hamiltonian, then $t(G) \ge 1$. In other words, for all disconnecting subsets $S$, we have $|S| \ge c(G / S)$. 
>
> > [!Note]- Proof
> > 
> > Let $c(G / S) = k$, $G_1, G_2, \dots G_k$ are the components. 
> > 
> > If a cycle exists, start in $G_1$. Every time we want to move into another component, we need to traverse one vertex in $S$ (as $S$ connects all the components). Hence for each component traversed we must visit a different vertex (by assumption of Hamiltonian cycle) in $S$, so the size of $S$ must equal or be greater than the number of components.
> > $$
> > |S| \ge c(G / S) \to t(G) \ge 1
> > $$

> The contrapositive of the theorem is quite useful to disprove Hamiltonicity! We find the existence of a set such that $\frac{|S|}{c(G/S)} < 1$.

Note that the converse of the theorem is not true. If $t(G) \ge 1$, that does not necessarily mean that the graph is Hamiltonian. As a counterexample, consider the Petersen Graph, with $t(G) = 4/3 > 1$, but shown to not be Hamiltonian.

Then, what toughness value is enough?

> [!Tip] Conjecture: $t(G) \ge 2$
> It used to be conjectured that $t(G) \ge 2$ worked for Hamiltonian graphs, which was disproved in 2000. This is an open problem:
> 
> Is there a $t_0$ threshold such that every $t_0$-tough graph is Hamiltonian?
>
> It is known that $t_0 > \frac{9}{4}$, but no exact number is yet known.

Then, do we know any sufficiencies for Hamiltonian Graphs (given a condition, we know the graph is Hamiltonian)? Well, intuitively we should think of graphs wiht high degrees / lots of edges, as this gives us more connections to move around on.

> [!Abstract] Theorem (Ore's): Sufficiency for Hamiltonian Graphs
> Let $G$ have order $n \ge 3$. 
> 
> If $\deg(u) + \deg(v) \ge n$ for all 2 **non-adjacent** vertices $u,v$, then $G$ is Hamiltonian.
> > This is quite useful for $k$-regular graphs! Say we have a 6-regular graph on 10 vertices. Then, the graph must be Hamiltonian, as $6 + 6 \ge 10$ for any two vertices!
>
> > [!Note]- Proof
> > 
> > Suppose $G$ is NOT hamiltonian. 
> > 
> > We will add edges to $G$ so that any additional edge makes $G$ Hamiltonian. Let $H$ be the new graph. It's clear that the graph is not complete, as if it were we would have a Hamiltonian graph trivially. 
> > 
> > Let $x, y$ be non-adjacent vertices. If adding 1 more edge between them, then there must exist at least a Hamiltonian path! Consider this path,
> > $$
> > x = x_1 \to x_2 \to \dots x_n =  y
> > $$
> > 
> > Suppose $x$ has an adjacency to some random $x_i$ along this path. Then, $y$ cannot be adjacent to any $x_{i-1}, x_{i-2}, \dots$ as if it were, we could form a Hamiltonian cycle as
> > $$
> > x \to x_i \to x_{i+1} \to \dots y \to x_{i-j} \to x_{i-j-1} \to \dots x
> > $$
> > Thus, the degree of $y$ must be less than $n - 1 - \deg{x}$.
> > $$
> > \deg(x) + \deg{y} \le n - 1 \Longrightarrow \deg{x} + \deg{y} < n
> > $$

Note that the converse of the theorem does not hold. Consider the following counterexample.

> [!Example]+ Example: Failure of Ore's Converse
> ```mermaid
> graph LR
> 1 o--o 2 o--o 3 o--o 4 o--o 5 o--o 1;
> ```
> 
> Then, for any two non-adjacent vertices, say $1,3$,
> $$
> \deg{1} + \deg{3} = 4 < 5 
> $$
> 
> But $G$ is Hamiltonian!

> [!Example]- Example
> ```mermaid
> graph LR
> 1 o--o 2 o--o 3 o--o 4 o--o 1;
> 2 o--o 4; 1 o--o 3;
> 
> 5 o--o 6 o--o 7 o--o 8;
> 5 o--o 7; 6 o--o 8;
> 
> 9 o--o 1 & 2 & 3 & 4 & 5 & 6 & 7 & 8;
> ```
> 
> If we delete $9$, we get $t(G) \le \frac{1}{2}$, so $G$ is NOT Hamiltonian. Furthermore, for any two non-adjacent vertices,
> $$
> \deg{u} + \deg{v} = 8 < 9
> $$
> > Ore's theorem is "best possible"! For a graph to be Hamiltonian given $n$, we have a requirement on the degrees that must be true!

## 4.3: Planar Graphs
A graph $G$ is **planar** if it ca be drawn in the plane so that no edges cross each other.

> [!Example]+ Example: Planar Graph
> ```mermaid
> graph LR
> 1 o--o 2 o--o 3 o--o 4;
> 1 o--o 3; 2 o--o 4;
> ```
> 
> This is a planar graph, even though what we currently see has edges crossing! We can have $2 \to 4$ go above 3 so that the edges don't cross.

Every planar graph can divide the plane into **regions (faces)**. Note that we include the space outside the edges graph as its own separate region.

If $G$ is on at least 3 vertices that is NOT a tree, every region / face is surrounded by at least 3 edges, known as its **boundary**.

> [!Abstract] Theorem: Euler's Identity
> If $G$ is a connected, planar (potentially multi) graph with "n" vertices, "m" edges, and "f" faces, then
> $$
> n - m + f = 2
> $$
>
> > Intuitively, this is telling us that if we have too many edges, then we cannot have a planar graph!
>
> > [!Note]- Proof
> > 
> > By induction on $m$, if $m = 0$, then $n = 1$, so we have 1 region. 
> > $$
> > 1 - 0 + 1 = 2
> > $$
> > 
> > Assume the statement holds for all graphs up to $m$ edges. Let $G$ be on $m + 1$ edges. 
> > 
> > If $G$ is a tree, then $n = m + 2$, $m + 1$ edges, $f = 1$. which satisies the equation. 
> > 
> > If $G$ is NOT a tree, then it has a cycle $C$. Delete an edge in the cycle, and let $H$ be the resultant graph. Deleting one edge also deletes one face (it merges two faces together). If has $m$ edges after deletion, so by the inductive hypothesis,
> > $$
> > \begin{align*}
> > 2 
> > &= | V(H) | - m + | f(H) | \\
> > &= |V(G)| - m + |f(G)| - 1 \\
> > &= |V(G)| - (m + 1) + |f(G)|
> > \end{align*}
> > $$

> [!Abstract] Theorem
> Let $G$ be a connected, planar graph of order $n \ge 3$, size $m$. Then, 
> $$
> m \le 3n - 6
> $$
>
> > The contrapositive is very importnat! If $m > 3n - 6$, then we cannot have a planar graph!
>
> > [!Note]- Proof (Know This Proof!!)
> > 
> > If $n = 3$ and it is a tree, then the result holds.
> > 
> > Assume $m \ge 3$. Let $R_1, R_2, \dots R_f$ be the faces / regions. Let $m_i$ be the number of edges on the boundary of $R_i$. Since there's at least 3 edges for each boundary,
> > $$
> > \sum_{i=1}^f m_i \ge 3f
> > $$
> > Now look at every edge. Each edge could lie on the boundary of at most 2 faces (it could be a bridge, in which case it would only border 1 region). So, in the sum, each edge will only be counted at most 2 times!
> > $$
> > \sum_{i=1}^f m_i \le 2m
> > $$
> > Combining these, we get
> > $$
> > 3f \le \sum_{i=1}^f m_i \le 2m \Longrightarrow 3f \le 2m
> > $$
> > 
> > We now apply Euler's identity, $f = 2 - n + m$, to get
> > $$
> > \begin{align*}
> > 3(2 - n + m) \le 2m \\
> > 6 - 3n + 3m \le 2m \\
> > m \le 3n - 6
> > \end{align*}
> > $$
>
> > [!Info]
> > 
> > Corollary: If $G$ is planar, there is a vertex of degree 5 or less. If all vertices have degree 6 or more, then $m \ge (6n) / 2 = 3n$, yielding a contradiction.

> [!Example]+ Example
> $K_5$ has $\binom{5}{2} = 10$ edges. To be planar, $m \le 3n - 6$. Because
> $$
> 10 \not< 3(5) - 6
> $$
> $K_5$ cannot possibly be planar.

> [!Example]- Example: House and Utilities Problem
> Three houses need to connect gas, water, and electricity lines to their houses. Can can they all be connected without crossing lines?
> 
> Consider 3 nodes, one for gas, water, and electricity. Now consider 3 other nodes, 1 for each house. This yields a $K_{3,3}$ graph, and we're essentially asking if it is planar. 
> > Unfortunately, we cannot use the theorem, as we get 
> > $$
> > 9 \le 3(6) - 6
> > $$
> > Yielding an inconclusive result.
> 
> Assume that the graph is planar. If it is, then we can apply Euler's identity
> $$
> n - m + f = 2 \Longrightarrow 6 - 9 + f = 2 \Longrightarrow f = 5
> $$
> Thus, if the graph is planar, it must have 5 faces. Since $K_{3,3}$ is bipartite, there are no odd cycles, so the boundary of each face has at least 4 edges. This gives us an upper bound, if we sum the number of edges at each face
> $$
> \sum m_i \ge 4(5) = 20
> $$
> Now, each edge can only border at most 2 regions, and in fact, with no bridges in $K_{3,3}$, every edge must be counted twice in the sum.
> $$
> \sum m_i = 2m = 2(9) = 18
> $$
> This tells us
> $$
> 20 \le \sum m_i = 18 \Longrightarrow 20 \le 18
> $$
> Which is a contradiction!
>
> So, $K_{3,3}$ is not planar.

---

A **subdivision** of edge $u \sim v$ is the operation of replacing $u \sim v$ with the path $u, w, v$. A **subdivision** of graph $H$ is the graph obtained from $H$ by successive edge subdivisions. 

> [!Example] Example: Subdivided Graph
> ```mermaid
> graph LR
> 1 o--o 2 o--o 3 o--o 4 o--o 1 o--o 5;
> 6[1] o--o 7[ ] o--o 8[2] o--o 9[ ] o--o 10[3] o--o 11[ ] o--o 12[4] o--o 13[ ] o--o 6 o--o 14[ ] o--o 15[5];
> ```

Clearly, if $G$ is planar, then any subdivision of $G$ is also planar! Similarly, the converse holds. If a subdivision is planar, then $G$ must also be planar!
> Subdividing an edge doesn't change how we can draw the graph!

This is important, as we can check for non-planar subgraphs to see if our graph is planar! For example we've shown that $K_5$ and $K_{3,3}$ are not planar. Hence, if $G$ has a subgraph that is $K_5$, $K_{3,3}$ or a subdivision, it cannot be planar.

Amazingly, the converse of this statement holds!

> [!Abstract] Theorem: Kuratowski
> A graph $G$ is planar if and only if $G$ does NOT contain $K_5$ or $K_{3,3}$, or any subdivision of $K_5$ or $K_{3,3}$.

> [!Example]+ Example: Petersen Graph
> ```mermaid
> graph LR
> 1 o--o 6; 2 o--o 8; 3 o--o 10; 4 o--o 7; 5 o--o 9;
> 1 o--o 2 o--o 3 o--o 4 o--o 5 o--o 1;
> 6 o--o 7 o--o 8 o--o 9 o--o 10 o--o 6;
> ```
>
> Let $A = \{1,7,10\}$, $B = \{2,5,6\}$. We can form $K_{3,3}$ graph
> ```mermaid
> graph TD
> 1 o--o 2 & 5 & 6;
> 
> 7 o--o 8 o--o 21[2];
> 7 o--o 4 o--o 51[5];
> 7 o--o 61[6];
> 
> 10 o--o 3 o--o 22[2];
> 10 o--o 9 o--o 52[5];
> 10 o--o 62[6];
> ```
> > Note that during subdivisions, you can't use the same vertices multiple times!
>
> Thus, the Petersen Graph is not planar.

> [!Example]+ Example: Petersen Graph (2)
> Show the Petersen graph is NOT planar by using the fact that it has girth 5. 
> 
> We know $n = 10, m = 15$. If it is planar, then
> $$
> 2 = n - m + f \Longrightarrow f = 7
> $$
> So, we must have 7 faces! Let $m_i$ denote the total edges on the boundary of face $f_i$. With girth 5, 
> $$
> \sum_{i=1}^7 m_i \ge 5f
> $$
> > Every face is a cycle!
> Every edge is counted at most twice in the sum, so
> $$
> \sum_{i=1}^7 m_i \le 2m = 30 
> $$
> So, $5f \le 30$, meaning $f \le 6$! This gives us a contradiction!

Many graphs aren't planar. But "how close to planar" are they? Could we define a measure for this?

The minimum number of edge crossings of a graph drawn on the plane is the **crossing number** of $G$, denoted $\text{cr}(G)$.
> This is a very difficult question to find exactly! Bounds are known for $K_$ and $K_{a,b}$, but its unknown what the exact formulas are.

This is a very topological question, and note that the number of edge crossings depends on the "surface" the graph is on! For example, $K_5$ can be drawn to be planar on a Torus!
> The edge crossing on $K_5$ can be drawn to loop through the center of the Torus, avoiding an edge crossing!

If a graph is planar, then we can also draw it on a sphere without crossing! Now, if we attach "handles" onto the sphere to draw without crossings, then our question is the minimum number of "handles" we need to make the graph planar! In other words, for a planar graph, we can imagine a "bridge" that edges (possibly multiple) can take to avoid crossing others.

The **genus** of grpah $G$ is the fewest handles needed on the sphere to avoid any edge crossings.
> Note that the Petersen graph has crossing number 2, but genus 1.

## 4.4: Graph Colorings
A **proper coloring** of a graph $G$ is labeling the vertices of $G$ so that each vertex is asigned 1 color, such that adjacencies have different colors. We say graph $G$ is **$k$-colorable** if there is a proper coloring with $k$ colors.

The **chromatic number** of $G$, denoted $\chi (G)$, is the fewest number of colors $k$ such that $G$ is $k$-colorable.

> [!Example] Example
> Let's color a map! Vertices are countries / states, with an adjacency if two regions share a border. 

> [!Abstract] Theorem: 4 Color Theorem (Appel, Haken, 1976)
> Any map (planar graph) can be colored with 4 colors. 

Note that an explicit coloring of a graph yields an **upper bound** on the chromatic number!

> [!Abstract] Theorem
> $G$ is bipartite with at least 1 edge if and only if $\chi(G) = 2$.

### Lower Bounds on $\chi(G)$
A subset $S$ of vertices is an **independent set** if no two vertices are adjacent in $S$. It is **maximal** if no more vertices can be added to $S$. It is **maximum** if it has the largest cardinality of all independent sets for a graph. The value of the maximum, the **independence number**, is denoted $\alpha(G)$.

> [!Example] Example: Maximum Independent Set
> ```mermaid
> graph LR
> 1 o--o 2 & 3;
> 2 o--o 6 & 3;
> 6 o--o 5;
> 3 o--o 4 & 5;
> 4 o--o 5;
> ```
> 
> A possible independent set is $\{1,4,6\}$. This is maximum!
>
> Another possible independent set is $\{1,5\}$. This is maximal, but not maximum!

Given a proper coloring of $G$, each "color class" (group of vertices with the same color) is an independent set!

A **clique** is a complete subgraph $K_t$ of $G$. The **clique number** of $G$, denoted $\omega(G)$, is the order of the largest clique in the graph!

In the above example, $\omega(G) = 3$ (consider $1,2,3$), so clearly, at least 3 colors are needed. Observe, we have the following: 

> [!Abstract] Theorem
> For any graph $G$, 
> $$
> \omega(G) = k \iff \alpha(\bar{G}) = k
> $$
> In other words, the clique number of the graph is the same as the independence number of $G$'s complement.

> [!Abstract] Theorem
> If $G$ has order $n$, then 
> 1. $\chi (G) \ge \omega (G)$: The chromatic number is bounded below by the clique number.
> 2. $\chi (G) \ge \frac{n}{\alpha(G)}$: The chromatic number is bounded by number of vertices divided by the independence number. 
> 
> > [!Note]- Proof
> > 
> > Clearly, every vertex in a clique is a different color as they are all adjacent to each other.
> > 
> > Let $\chi(G) = k$, Let $V_1, V_2, \dots V_k$ be the color classes (ex. $V_1$ is the vertices colored color 1). Then,
> > $$
> > n = \sum_{i=1}^K |V_i|
> > $$
> > But each vertex color class is the same as an independent set, and we can bound this by the independence number! 
> > $$
> > n = \sum_{i=1}^K |V_i| \le \alpha(G) + \alpha(G) + \dots + \alpha(G) = k \cdot \alpha(G)
> > $$
> > So,
> > $$
> > k \ge \frac{n}{\alpha(G)}
> > $$

> [!Example] Example
> Consider a $C_3$ and $C_5$ graph, where each node in the cycle is connected to all nodes in the other cycle.
> ```mermaid
> graph LR
> 1 o--o 2 o--o 3 o--o 1;
> 4 o--o 5 o--o 6 o--o 7 o--o 8 o--o 4;
> ```
> 
> Here, the clique number is $\omega(G) = 5$, as we take 2 nodes from $C_5$ and 3 nodes from $C_3$ to form a $K_5$ graph.
>
> Clearly, $\chi (C_3) = 3$ and $\chi (C_5) = 3$. Furthermore, since everything in the $C_3$ joins to $C_5$, they must use different colors. Thus, $\chi (G) = 6$, even though $\omega (G) = 5$.

Intuitively, we may think that as the smallest cycle in a graph increases in size, it may serve as a bound for the chromatic number! However, this intuition unfortunately doesn't work. See the below theorem.

> [!Abstract] Theorem: 
> For any positive integers $k$ and $l$, there exists a graph $G$ with girth (smallest cycle) greater than $l$, and $\chi (G) > k$.

### Upper Bounds on $\chi(G)$
Explicit colorings provide an upper bound on the chromatic number. Consider coloring the graph in a greedy manner:
- Let $v_1 \dots v_n$ be the vertices. 
- Color $v_1$ color 1. 
- Go to $v_2$. If $v_2 \sim v_1$, color $v_2$ color 2. Otherwise, color $v_2$ color 1.
- Repeat for all $v_i$'s, coloring $v_i$ with the lowest index color NOT used by the neighbors of $v_i$.

A consequence of this algorithm, is that at vertex $v_i$, we use at most $\deg(v_i) + 1$ colors. As we do this for every vertex, we can bound the maximum colors needed above with the maximum degree!
> The +1 is in case we need to use a new color!

> [!Abstract] Theorem
> We have $\chi(G) \le \Delta(G) + 1$, where $\Delta (G)$ is the maximum degree in $G$.

This was further refined as follows:

> [!Abstract] Theorem (Brooks)
> We have $\chi (G) \le \Delta (G)$ (remove the +1) provided $G$ is NOT $K_n$ or an odd cycle (must be exactly equal to).

> [!Example] Example: Petersen Graph
> ```mermaid
> graph LR
> 1 o--o 6; 2 o--o 8; 3 o--o 10; 4 o--o 7; 5 o--o 9;
> 1 o--o 2 o--o 3 o--o 4 o--o 5 o--o 1;
> 6 o--o 7 o--o 8 o--o 9 o--o 10 o--o 6;
> ```
>
> We know that the Petersen Graph contains a $C_5$, so it is NOT bipartite, meaning $\chi(G) > 2$.
> 
> We furthermore know that it is not $K_n$ or $C_{2k+1}$, so by Brook's theorem, $\chi(G) \le \Delta(G) = 3$. So, $\chi(G) = 3$.

### Critical Graphs
Graph $G$ is **$k$-critical** if $\chi(G) = k$ and for every **proper** subgraph $H$, $\chi(H) < k$.
> Basically, the graph $G$ is reduced so that any further deletion will change the chromatic number!

> [!Example] Example: 
> Consider a graph on Odd Cycles.
> ```mermaid
> graph LR
> 1 o--o 2 o--o 3 o--o 4 o--o 5 o--o 6 o--o 7 o--o 1;
> ```
> 
> Here, $\chi(C_{2k+1}) = 3$, but the deletion of any vertex or edge turns the graph into a forest, making the graph Bipartite, so $\chi(H) = 2$! Thus, any graph on odd cycles is 3-critical.

> [!Abstract] Lemma
> If $G$ is $k$-critical, then $\delta(G) \ge k - 1$, where $\delta(G)$ is the minimum degree.
>
> > [!Note]- Proof
> >
> > By way of contradiction, let $x$ be a vertex of $G$, and assume $\deg(x) < k - 1$. Consider the graph without $x$. Because $G$ is $k$-critical, if we remove $x$ then $G / x$ must have $\chi(G) < k$, so $G$ is $k - 1$ colorable.
> > 
> > If $G$ is $k - 1$ colorable, and $x$ is adjacent to only $k - 2$ vertices, then our $k - 2$ vertices must be colored with at most $k - 2$ colors, with 1 remaining! So, we color $x$ with this remaining color, meaning $G$ is $k - 1$ colorable, contradicting the fact that $\chi(G) = k$.

> [!Abstract] Theorem
> We have
> $$
> \chi(G) \le 1 + \max_{H \subseteq G} \delta(H)
> $$
> 
> In other words, we can find an upper bound for our chromatic number if we go through all possible subgraphs of $G$. 
> > $G$ does not have to be $k$-critical!
>
> > [!Note]- Proof
> > 
> > Suppose $\chi(G) = k$, and let $H'$ be a $k$-critical subgraph of $G$. Then, $\chi(G) - 1 = \chi(H') - 1 \le \delta(H') \le \max_{H \subseteq G} \delta(H)$, by the Lemma.

> [!Example] Example
> ```mermaid
> graph LR
> 1 o--o 2 o--o 3 o--o 4 o--o 1;
> 1 o--o 3; 2 o--o 4;
> 1 o--o 5 & 6;
> 2 o--o 7 & 8;
> 3 o--o 9 & 10;
> 4 o--o 11 & 12;
> ```
> 
> Here, our minimum degree is 1. But if we removed all vertices 5 to 12, then our min degree would be 3! Because this is the "best" we can get, our chromatic number can be at most $1 + 3 = 4$.
> 
> This is a better bound than Brooks!

### Edge Colorings
An **edge coloring** of $G$ is an assignment of colors to edges such that edges incident to the same vertex are different colors.

The minimum colors needed is the **chromatic index**, $\chi_1 (G)$.

> [!Abstract] Theorem (Vizing)
> For any graph $G$, $\chi_q (G) = \Delta (G)$, or $\chi_1 (G) = \Delta(G) + 1$. In other words, the chromatic index can only take on 2 possible values.

## 4.5: Mycielski's Construction
We know that the chromatic number is bounded below by the clique number.
$$
\chi(G) \ge \omega(G)
$$

We let $G$ be a triangle-free graph (no $K_3$'s) and construct a new graph with higher chromatic number, but same clique, but remains triangle free. Thus, $G$ **and** the new graph have clique number 2.
> This section teaches us how to construct graphs super large, while keeping the clique number small! This shows that the "intuition" that smaller clique numbers are better doesn't work the best.

Let $G$ have vertex set $\{v_1, v_2, \dots v_n\}$. We construct the graph as follows.
1. Add $n + 1$ vertices, denoted $w, u_1, \dots u_n$.
2. Join $w$ to all of the $u_i$'s.
3. Join $u_i$ to the $v_j$'s such that $v_j \sim v_i$.

> [!Example]+ Example
> Suppose we have initial graph
> ```mermaid
> graph LR
> v1 o--o v2 o--o v3;
> ```
> Now, we add $3 + 1 = 4$ vertices, and join $w$ to all of the $u_i$'s.
> ```mermaid
> graph LR
> v1 o--o v2 o--o v3;
> w o--o u1 & u2 & u3;
> ```
> For step 3,
> - For $u_1$, join it to all neighbors of $v_1$: $v_2$.
> - For $u_2$, join it to all neighbors of $v_2$: $v_1, v_3$.
> - For $u_3$, join it to all neighbors of $v_3$: $v_2$.
> ```mermaid
> graph LR
> v1 o--o v2 o--o v3;
> w o--o u1 & u2 & u3;
> u1 o--o v2;
> u2 o--o v1 & v3;
> u3 o--o v2;
> ```

We prove below that under this algorithm, the new graph remains triangle free. In other words, the clique number remains 2.

> [!Note]- Proof: Triangle-Free
> We prove that the new graph is triangle free.
> 
> Clearly, there you cannot form a triangle with any $u_i, u_j, v_k$ as there are no edges among $u$'s. So, if a triangle occurs, it must occur between $u_i v_j v_k$. 
> 
> So, if there is a triangle between $u_i v_j v_k$, then by step 3, $v_i \sim v_j$, and $v_i \sim v_k$. We use the edge in the triangle $v_j \sim v_k$ to form a triangle
> $$
> v_i v_j v_k
> $$
> This means that the original graph had a 3-cycle, which is a violation of our assumptions!

We now show that the **chromatic number increases by 1** for every additional construction we do.

> [!Note]- Proof: Chromatic Number 
> We now show that the chromatic number increases.
> 
> Let $G_m$ denote the $m^{th}$ level of the construction, with $\chi(G_m) = k$, and $G_m$ is on $n$ vertices.
> 
> We show $\chi(G_{m+1}) \le k + 1$ first, by showing a coloring. For each $u_i$, we know by step (3) that is is joined with the neighbor(s) of $v_i$, so, we can color $u_i$ the color of $v_i$ without any violations:
> - $u_i$ cannot have an edge to $v_i$, so the same color won't be adjacent
> - $u_i$ is only adjacent to neighbors of $v_i$, which will have different colors than $v_i$ by definition of a coloring
> 
> So, $u_i$ is never adjacent to a vertex of $v_i$'s color.
> 
> Coloring each $u_i$, we may use all $k$ colors as $\chi(G_m) = k$. Then, with $w$, let's just color it an extra $k + 1$ color as we may have used each of the $k$ colors in our $u$'s! This gives us a $k + 1$ coloring, so $\chi(G_{m+1}) \le k + 1$.
> 
> ---
> 
> Now assume to the contrary that $\chi(G_{m+1}) = k$ (it is not possible for it to be less than $k$, as $G_m$ is a subgraph). We show that it is not possible. 
> 
> Without loss of generality, let vertex $w$ be color $k$. Then, as $w$ is adjacent to all $u_i$'s by step (2), the $u_i$'s can only use at most $k - 1$ colors. However, as $\chi(G_m) = k$, we must use $k$ colors in $G_m$, so there must exist a vertex $v_i$ with color $k$.
> 
> Because $u_i$ is adjacent to all neighbors of $v_i$ by step (2), we can guarantee that $v_i$'s neighbors are not colored the same as $u_i$, because $u_i$ is adjacent to all of them! Furthermore, as $u_i$ is either color 1 to $k - 1$, $v_i$ can be recolored as $u_i$! Doing this for all $v_i$'s of color $k$, we can find a $k - 1$ coloring for the graph. But this is a contradiction, as $\chi(G_m) = k$, so no smaller coloring exists!

We have proven the following: 

> [!Abstract] Theorem: Mycielski
> There exists graphs $G$ with $\omega(G) = 2$, but $\chi(G)$ is arbitrarily large.

The proofs also give us a way to color a graph constructed using Mycielski's Construction! Color the base graph, and then follow the $k + 1$ coloring scheme that was given above.
