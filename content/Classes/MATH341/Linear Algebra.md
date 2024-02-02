---
title: Linear Algebra
tags:
- math341
---

# Fields
A **field** $\mathbb{F}$ is any set of elements satisfying the following axioms:

| **Axiom Name** | **Addition** | **Multiplication** |
| - | - | - |
| **Associativity** | $(a + b) + c = a + (b + c)$ | $(ab) c = a (bc)$ |
| **Commutativity** | $a + b = b + a$ | $a b = b a$
| **Distributivity** | $a (b + c) = ab + ac$ | $(a + b) c = ac + bc$ |
| **Identity** | $a + 0 = a = 0 + a$ | $a \cdot 1 = a = 1 \cdot a$ |
| **Inverses** | $a + (-a) = 0 = (-a) + a$ | $a a^{-1} = 1 = a^{-1} a$ if $a \ne 0$ |

Very common examples of fields are as follows:
- **Field of All Real Numbers**, denoted $\mathbb{R}$.
- **Field of All Complex Numbers**, denoted $\mathbb{C}$.

> Integers ($\mathbb{Z}$), do not satisfy the field axioms, and thus are not a field.

# Matrices
A **matrix**, in its simplest form, is an arrangement of elements scalars $c \in \mathbb{F}$ into rows and columns. We describe a matrix $A$ with $n$ rows and $m$ columns as an $n \times m$ matrix.
> Matrices are highly useful in describing many things, and have tons of real world applications! 

We commonly use uppercase letters, such as $A, B, C, \dots$ to denote matrices. We also lowercase letters, like $[a]_{ij}$ to denote the entry on the $i^{th}$ row and $j^{th}$ column in matrix $A$.

The set of all $m \times n$ matrices in field $\mathbb{F}$ is denoted as $M_{m \times n} (\mathbb{F})$.

## Matrix Operations
### Addition and Scalar Multiplication
Let $A, B \in M_{m \times n} (\mathbb{F})$, and scalar $c \in \mathbb{F}$.

We define **matrix addition** as the operation adding all corresponding entries of the matrices together.
$$
A + B = [a]_{ij} + [b]_{ij}
$$

We define **scalar multiplication** as the operation multiplying all entries of a matrix with a scalar.
$$
c \cdot A = [c \cdot a]_{ij}
$$

Now define $A$ as an $m \times n$ matrix, and $B$ as an $n \times p$ matrix. 

We have the following properties of matrix addition and scalar multiplication:
- **Commutative Property of Addition**: $A + B = B + A$
- **Associative Property of Multiplication**: $A + (B + C) = (A + B) + C$
- **Associative Property of Addition** $(cd) A = c (dA)$
- **Additive Identity**: $A + 0 = A$
- **Multiplicative Identity**: $1A = A$
- **Distributive Property**: $c( A + B) = cA + cB$ and $(c + d)A = cA + dA$

### Matrix Multiplication
We define **matrix multiplication** as the operation where the product of $A \cdot B$, say $C$, is equal to
$$
[c]_{ij} = [a]_{i1} [b]_{1j} + [a]_{i2} [b]_{2j} + \dots + [a]_{in} [b]_{ni}
$$
In other words, the entry $[c]_ij$ is found by multiplying each entry of the $i^{th}$ row of $A$ with its corresponding entry on the $j^{th}$ row of $B$, and summing the result.
> Matrix multiplication is not commutative ($AB \ne BA$).

We have the following properties of matrix multiplication:
- **Associative Property of Matrix Multiplication**: $A(BC) = (AB)C$
- **Distributive Property of Matrix Multiplication**: $A(B + C) = AB + AC$ and $(A + B)C = AC + BC$
- **Multiplicative Identity**: $AI = A$, where $I$ is the **identity matrix**, a matrix of order $n$ with only 1s on the main diagonal.

## Systems of Linear Equations
We define a **linear equation** on $n$ variables as
$$
a_1 x_1 + a x_2 + \dots + a_n x_n = b
$$
where $a_i$ is a constant, and $x_i$ stands for any variable in the first power.
> We commonly use matrices to represent and solve systems of linear equations. 

Let $A$ be some matrix. We have a set of **row operations**, which are operations which can be used to **row reduce** a matrix to a triangular form.
> While these operations do change the matrix, they preserve the solution set of the matrix!
- **Interchanging 2 Rows**: $R_i \leftarrow \rightarrow R_j$
- **Multiplying a Row By a Scalar**: $c R_i \to R_i$
- **Multiplying a Row by a Scalar and Adding it to Another Row**: $c R_i + R_j \to R_j$

We use these row operations to transform the matrix to **row-echelon form**.

> [!Info] Row-Echelon Form
> A matrix is described to be in **row-echelon form** if it satisfies the following properties:
> - All rows consisting of only 0s are at the bottom.
> - The leading entry (left-most entry) of every non-zero row is to the right of the leading entry of the row above.

We can further apply row operations to obtain **reduced row-echelon form**.

> [!Info] Reduced Row-Echelon Form
> A matrix is described to be in **reduced row-echelon form** if it satisfies the following properties:
> - The matrix is in row echelon form.
> - The leading entry in each non-zero row is 1.
> - Each column with a leading 1 has 0s in all other entries

These forms can be used to easily deduce the solution to the system of requations.

### Elementary Matrices
An **elementary matrix**, commonly denoted as an $E$, is a matrix obtained from applying one elementary row operation to $I$, the identity matrix. 

Given any matrix $A$, multiplying a matrix $A$ with elementary matrix $E$ ($EA$) performs the elementary row operation on it.
> Multiplying on the left ($EA$) modifies $A$'s rows, and multiplying on the right ($AE$) modifies $A$'s columns.


## Associated Matrices
### Matrix Transpose
The **transpose** of $A \in M_{m \times n} (\mathbb{F})$, denoted $A^T$, is the $n \times m$ matrix created by flipping it's rows and columns.
$$
[a^T]_{ij} = [a]_{ji}
$$

We have the following properties of transposes:
1. **Transpose of a Transpose**: $(A^T)^T = A$
2. **Transpose of a Sum**: $(A + B)^T= A^T + B^T$
3. **Transpose of a Scalar**: $(cA)^T=c (A^T)$
4. **Transpose of a Product**: $(AB)^T=B^T \cdot A^T$

We define a **symmetric matrix** as one which is equal to its transpose.
$$
A = A^T
$$
> The product of a matrix and its transpose is always a symmetric matrix!

### Matrix Inverse
We define the **inverse** of square matrix $A \in M_{n} (\mathbb{F})$, denoted $A^{-1}$, as the matrix such that
$$
A \cdot A^{-1} = A^{-1} A = I
$$
> A matrix is **invertible** if it has an inverse (not all square matrices have inverses!)

We can find the inverse by writing and row-reducing the system of equations
$$
\left[ A \; \vert \; I \right] \to \left[ I \; \vert \; A^{-1} \right]
$$
> When finding $A^{-1}$, we're technically multiplying $A$ by elementary matrices $E$ to find $I$. Multiplying these matrices yields the inverse such that $A^{-1} A = I$ (which is what this system of equations is doing for us!)

Let $A$ be an invertible matrix. We have the following properties of inverses:
- $(A^{-1})^{-1} = A$
- $(cA)^{-1} = \frac{1}{c} A^{-1}$
- $(AB)^{-1} = B^{-1} A^{-1}$
- $(A^n)^{-1} = (A^{-1})^n$

### Similar Matrices
Let $A$ and $B$ be $n \times n$ matrices. Then, $A$ and $B$ are **similar** if there exists an invertible matrix $P$ such that
$$
B = P A P^{-1} \qquad A = P^{-1} B P
$$
> This will come up and be highly useful later!

## Properties of Square Matrices
A **square matrix** $A$ is one where its number of columns and rows are equal. 
> The set of all $n \times n$ matrices is commonly denoted as $M_n (\mathbb{F})$.

### Trace
The **trace** of $A \in M_n (\mathbb{F})$, denoted $tr(A)$, is the sum of its diagonal entries.
$$
tr(A) = \sum_{i = 0}^n [a]_{ii}
$$
> The trace is only defined for square matrices!

### Determinant
Define $A = \begin{bmatrix} a & b \\ c & d \end{bmatrix} \in M_2 (\mathbb{F})$ as a $2 \times 2$ matrix. The **determinant** of $A$, denoted $det(A)$, is defined as
$$
det(A) = \begin{vmatrix} 
	a & b \\ c & d 
	\end{vmatrix} = ad - bc
$$

Now let $A = [a]_{ij}$ be an $n \times n$ matrix. The **minor** of element $a_{ij}$, denoted $M_{ij}$ is the determinant of the submatrix obtained by deleting row $i$, and column $j$.
The **cofactor** of $a_{ij}$ is
$$
c_{ij} = (-1)^{i + j} M_{ij}
$$

Then, the **cofactor expansion** of $A$ is the determinant of this matrix, defined as
$$
\sum_{i = 1}^n = a_{1i} C_{1i}
$$
In order words, the summation of cofactors along the first row.

> [!Abstract] Theorem: Determinants
> The cofactor expansion does not depend on which row or column is used.

Let $A$ and $B$ be $n \times n$ matrices. We have the following properties of determinants:
- $det(cA) = c^n det(A)$
- $det(A \cdot B) = det(A) \cdot det(B)$
- $det(A) = det(A^T)$
- $det(A^{-1}) = \frac{1}{det(A)}$, provided the inverse exists.

Now suppose $B$ was obtained from $A$ by performing row operations. Then we have the following properties:
- If $B$ is obtained from $A$ by swapping 2 rows, then $det(A) = -det(B)$
- If $B$ is obtained from $A$ by scaling a row of $A$ and adding it to a different row, then $det(A) = det(B)$.

> [!Abstract] Theorem: Determinants and Inverses
> Let $A$ be an invertible matrix. Define $adj(A)$ as the **adjugate** of $A$, the transpose of the matrix of cofactors $C$.
> 
> Then,
> $$
> A^{-1} = \frac{1}{det(A)} adj(A)
> $$
> 
> > **Corollary**: $A$ is invertible if and only if $det(A) \ne 0$. 

# Vector Spaces
## Vector Spaces and Subspaces
A **vector space** is a set $V$, over field $\mathbb{F}$, with elements of $V$ called **vectors**, with:
- An element $\vec{0} \in V$ called zero
- An addition law $\alpha: V \times V \to V$
- A scalar multiplication law $\mu : \mathbb{F} \times V \to V$

And satisfying 8 axioms:

| **#** | **Axiom** | **Description** |
| - | - | - |
|1| **Commutativity of Vector Addition** | For all $v, w \in V$, $v + w = w + v$ |
|2| **Associativity of Vector Addition** | For all $u, v, w \in V$, $u + (v + w) = (u + v) + w$ |
|3| **Identity of Vector Addition** | For all $v \in V$ we have $0 + v = v$ |
|4| **Additive Inverse** | For each $v \in V$ there is some $w \in V$ such that $v + w = 0$ |
|5| **Identity of Scalar Multiplication** | For all $v \in V$ we have $1 \cdot v = v$ |
|6| **Associativity of Scalar Multiplication** | For all $\lambda, \mu \in \mathbb{F}$ and $v \in V$, $(\lambda \mu) v = \lambda (\mu v)$ |
|7| **Distributivity of Scalar Multiplication Over Vector Addition** | For all $\lambda \in \mathbb{F}$ and $v, w \in V$, we have $\lambda (v + w) = \lambda v + \lambda w$ |
|8| **Distributivity of Scalar Multiplication Over Scalar Addition** | For all $\lambda, \mu \in \mathbb{F}$ and $v \in V$, we have $(\lambda + \mu) v = \lambda v + \mu v$ |

> [!Example]- Example: Real Vector Spaces
> 1. The space of real numbers
>    $$
>    \mathbb{R}^n = \{ (a, \dots, a_n) \; | \; a_i \in \mathbb{R} \}
>    $$
>    With $\vec{0} = (0, 0, \dots, 0)$, known as the **origin**.
> 
> 2. The set of polynomials of degree $\le n$
>    $$
>    P_n (\mathbb{R}) = \{ a_0 + a_1 t + a_2 t^2 + \dots + a_n t^n \; | \; a_i \in \mathbb{R} \}
>    $$
> 
> 3. The set of $m \times n$ matrices
>    $$
>    M_n(\mathbb{R}) = \begin{bmatrix} 
>    a_{11} & a_{12} & \dots & a_{1n} \\
>    a_{21} & a_{22} & \dots & a_{2n} \\
>    \vdots & \vdots & \ddots & \vdots \\
>    a_{m1} & a_{m2} & \dots & a_{mn}
>    \end{bmatrix}
>    $$
> 
> 4. The set of all continuous functions on $\mathbb{R}$
>    $$
>    C^0 (\mathbb{R}) = C(\mathbb{R}) = \left\{ f(t) \; | \; \begin{cases} f: \mathbb{R} \to \mathbb{R} \\ f \text{ is continuous}\end{cases} \right\}
>    $$
>
> 5. The set of infinitely differentiable functions
>    $$
>    C^\infty = \left\{ f(t) \; | \; \begin{cases} f: \mathbb{R} \to \mathbb{R} \\ f', f'', \dots, f^n \text{ exist}\end{cases} \right\}
>    $$
>    
> 6. The set of all complex numbers $\mathbb{C}$, as one can scale by real numbers. $\mathbb{C}$ has dimension 2, as its basis would be $\{ 1, i \}$

Let's look at $\mathbb{C}$ as a **complex vector space** under field $\mathbb{C}$. Because we can scale by any complex number,
- The basis of $\mathbb{C}^1$ is $\{ 1 \}$.
- The basis of $\mathbb{C}^2$ is $\{  (1,0), (0,1) \}$.

All complex vector spaces can also be real vector spaces.


Suppose we have vector space $V$ over field $\mathbb{F} = \mathbb{R}$.
We define $W$ as a **subspace** of $V$ ($W \subset V$) if the following properties are satisfied:
- **Closure Under Addition**: For all $v, w \in W$, we have $v + w \in W$
- **Closure Under Scalar Multiplication**: For all $c \in \mathbb{F}, v \in W$,  we have $c \cdot v \in W$
- **Contains Zero**: The zero vector $\vec{0} \in W$

> Given two subspaces $W_1$, and $W_2$, we can show that the intersection of the two subspaces $W_3 = W_1 \cap W_2$ is also a subspace.
> A subspace is a vector space contained within another vector space.

Moreover, if $W$ is a **proper subset** of $V$ (excludes some elements in $V$), then $U$ is a **proper subspace** of $V$.

> [!Example]- Example: Matrix Subspace
> Consider the set of $3 \times 3$ **skew-symmetric matrices**:
> $$
> W = \{ A \in M_3(\mathbb{R}) \; | \; A = -A^T\}
> $$
> 
> We can show that the set is a subspace of $M_3(\mathbb{R})$.

## Independence, Span, Basis
### Linear Combinations and Independence
Let $V$ be a vector space, and $v_1, v_2, \dots v_m$ be vectors in $V$. Then, $\vec{v} \in V$ is a **linear combination** of $v_1, v_2, \dots v_m$ if there exists scalars $c_1, c_2, \dots, c_m$ such that
$$
v = \sum_{i=1}^m c_i v_i
$$
> Vector $v$ is a sum of the set of vectors $v_1, v_2, \dots, v_m$.

Let $v = 0$. Then, the set of vectors $v_1, v_2, \dots v_m$, is **linearly independent** if
$$
\sum_{i=1}^m c_i \vec{v}_i = 0
$$ 
is true only for $c_1 = \dots = c_m = 0$. 
> If this is not the case (any $c_i$ is non-zero), the set of vectors is **linearly dependent**.

> [!Abstract] Theorem: Linear Dependence
> A set of non-zero vectors $v_1, v_2, \dots v_m$ is linearly dependent if and only if there exists a $v_i$ that is a linear combination of the others.

> [!Abstract] Theorem: Linear Dependence
> Any set of $m$ vectors on $\mathbb{R}^n$ is linearly dependent if $m > n$.

> [!Example]- Example: Linear Independence
> Suppose we have set $S = \{ e^t, e^{2t}, e^{3t} \} \in C^\infty (\mathbb{R})$. Is $S$ linearly independent?
> 
> We can write the elements of the set as a linear combination.
> $$
> c_1 e^t + c^2 e^{2t} +c^3 e^{3t} = 0 = z(t)
> $$
> Because this is an equality of functions, we know their derivatives must also necessarily be equivalent.
> $$
> c_1 e^t + 2 c^2 e^{2t} + 3 c^3 e^{3t} = 0 = z(t)
> $$
> $$
> c_1 e^t + 4 c^2 e^{2t} + 9 c^3 e^{3t} = 0 = z(t)
> $$
> 
> We can rewrite this in matrix form to solve for $c_1, c_2, c_3$.
> $$
> \begin{bmatrix}
>	1 & 1 & 1 \\
>	1 & 2 & 3 \\
>	1 & 4 & 9
> \end{bmatrix}
> \begin{bmatrix}
> 	c_1 e^t \\ c_2 e^{2t} \\ c_3 e^{3t}
> \end{bmatrix} =
> \begin{bmatrix}
> 	0 \\ 0 \\ 0
> \end{bmatrix} 
> $$
>
> Solving this system of equations, we see that
> $$ 
> \begin{bmatrix}
> 	c_1 e^t \\ c_2 e^{2t} \\ c_3 e^{3t}
> \end{bmatrix} =
> \begin{bmatrix}
> 	0 \\ 0 \\ 0
> \end{bmatrix} 
> $$
> Which can only be true when $c_1 = c_2 = c_3 = 0$.

### Span and Basis
Given any arbitrary set of vectors $S = \{ v_1, v_2, \dots, v_n \}$, the **span** of $S$ is the set of all linear combinations of $S$.
> The span of $S$ is the smallest subspace that contains $S$.

A set of vectors $S$ that is linearly independent such that $span(S) = V$  is a **basis** of $V$.
> Given a vector space $V$, if there exists a finite basis $S$, we say $V$ is **finite-dimensional**, with **dimension**
> $$
> dim(V) = |S|
> $$
> Where $|S|$ is the size of the set $S$.

> [!Info] Bases Outside of $\mathbb{R}^n$
> Given vector space $V$ with basis $B = \{ b_1, b_2, \dots, b_n \}$, we can transform any vector $v$ into a vector in $\mathbb{R}^n$ by taking its **coordinate vector** with respect to basis $B$.
> 
> The coordinate vector is defined as the "weights", or coefficients of each basis vector which represent vector $v$.
> $$
> v = a_1 b_1 + a_2 b_2 + \dots a_n b_n \to [v]_b = (a_1, a_2, \dots, a_n) \in \mathbb{R}^n
> $$

> [!Abstract] Theorem: Dimension and Basis
> If $dim(V)$ is finite, then any two bases of $V$ have the same size.
> 
> > [!Proof]- Proof
> > Suppose we have two bases, $B = \{ b_1, \dots, v_n \}$, $B' = \{ b_1', \dots, b_m' \}$. By definition, $span(B) = span(B') = V$, and both $B$ and $B'$ are linearly independent.
> > 
> > $B$ is a basis with $n$ elements, and $B'$ is linearly independent. However, as any set of $m > n$ vectors is linearly independent (by a previous theorem) $m = n$.

> [!Abstract] Theorem: Dimension and Linear Independence
> Let $v_1, v_2, \dots, v_m$ be the vectors in a set within vector space $V$, $dim(V) = n$. Then,
> 1. If $m < n$, there exists $v_{m+1}, \dots, \vec{v}_n \in V$ such that 
>    $$
>    v_1, \dots, v_n
>    $$ 
>    forms a basis for $V$.
> 2. If $m > dim(V)$, then any set of $m$ vectors in $V$ is linearly dependent.
> > [!Proof]- Proof
> >
> > Pick a basis $B = \{b_1, \dots, b_m \}$. 
> > 
> > Choose a map $T: V \to \mathbb{R}^n$ which is an isomorphism.
> > $$
> > T(v) = [v]_B \qquad T(cv) = cT(v)
> > $$
> > 
> > If any set of $m$ vectors in $V$ is linearly dependent, then they must also be linearly dependent in $\mathbb{R}^n$ by property of isomorphisms. 

> [!Example]- Example: Standard Basis
> The standard basis for $\mathbb{R}^n$ is
> $$
> \{ (1, 0, \dots, 0), (0, 1, \dots, 0), \dots, (0, 0, \dots, 1) \}
> $$

> [!Example]- Example: Dimension
> The subspace of $n \times n$ **skew-symmetric matrices**:
> $$
> W = \{ A \in M_n(\mathbb{R}) \; | \; A = -A^T\}
> $$
> Has dimension $\frac{n(n-1)}{2}$. 

> [!Example]- Example: Change of Bases
> Let $V = \mathbb{R}^2$ with basis
> $$
> B = \left\{ 
> 	\begin{bmatrix} 1 \\ 1 \end{bmatrix},
> 	\begin{bmatrix} 1 \\ 2 \end{bmatrix} 
> 	\right\}
> $$
> 	
> Define $v = (3,4)$. What is $[v]_B = (c_1, c_2)$?
> 
> We know that
> $$
> v = 
> 	c_1 \begin{bmatrix} 1 \\ 1 \end{bmatrix} + 
> 	c_2 \begin{bmatrix} 1 \\ 2 \end{bmatrix}
> $$
> Which creates the system of equations
> $$
> \begin{bmatrix} 
> 	1 & 1 \\ 
> 	1 & 2 
> 	\end{bmatrix}
> 	\begin{bmatrix} 
> 	c_1 \\ 
> 	c_2 
> 	\end{bmatrix} \to 
> 	\begin{bmatrix} 
> 	c_1 \\ 
> 	c_2 
> 	\end{bmatrix} = 
> 	\begin{bmatrix} 
> 	2 \\ 
> 	1 
> 	\end{bmatrix}
> $$
> 
> Thus, $[v]_B = (2,1)$.


> [!Example]- Example: Orthonormal Bases
> How many orthonormal bases are there for $\mathbb{R}^n$?
> 
> We begin by examining $\mathbb{R}^2$. Let $S^1$ denote all possible vectors composing the unit circle.
> $$
> S^1 = \{ (x,y) \; \vert \; x^2 + y^2 = 1 \}
> $$
> Then the number of $\mathbb{R}^2$'s orthonormal bases are $S^1 \times \{ \pm 1 \}$, where the $\pm 1$ comes from the choice of 2 orthogonal vectors.
> 
> Generalizing to  $\mathbb{R}^n$, we see that the set of all orthonormal bases in $\mathbb{R}^n$ is
> $$
> S^{n-1} \times S^{n-2} \times \dots \times S^2 \times S^1 \times \{ \pm 1 \}
> $$
> Where $\pm 1$ is $S^0$, the number of unique basis vectors in $\mathbb{R}^1$ (positive direction, negative direction).

# Linear Transformations
## Fundamental Subspaces
A $m \times n$ matrix $A \in M_{n \times n} (\mathbb{F})$ has the following **fundamental subspaces** associated with it:
1. **Column Space** ($Col(A) \subseteq \mathbb{F}^m$): The set of all linear combinations (span) of the column vectors.
2. **Row Space** ($Row(A) \subseteq \mathbb{F}^n$): The set of all linear combinations (span) of the row vectors.
3. **Null Space / Kernel** ($Null(A) / Kerl(A) \subseteq \mathbb{F}^n$): All vectors $v$, where $A \cdot v = 0$.

Additionally, we define the **rank** of $A$ as $dim(col(A))$.

> [!Abstract] Theorem: Fundamental Subspaces
> 1. Row equivalent matrices have the same rank.
> 2. The pivot columns (leading 1 locations) of $A$ form a basis of $col(A)$.
> 3. The non-zero rows of the reduced row echelon form of $A$ form a basis for $row(A)$.
> 4. $dim( row( A ) ) = dim( col ( A ) )$
> 
> > Theorem 4 does not state that $row(A)$ and $col(A)$ are the same - only that they have the same number of vectors.
> > 
> > We can find $A's$ fundamental subspaces by finding its echelon form of $A$, using scalar coefficients $c \in \mathbb{F}$

> [!Abstract] Theorem
> Matrix $A \in M_{n \times n} (\mathbb{F})$ is invertible if and only if
> - $Col(A) = \mathbb{F}^n$
> - $Ker(A) = \{ \vec{0} \}$

## Linear Transformations
Let $V$ and $W$ be two vector spaces spaces over field $\mathbb{F}$. 

A map $T: V \to W$ is a **linear transformation** if it satisfies the following properties:
1. $T(v + v') = T(v) + T(v')$ for $v,v' \in V$
2. $T(c \cdot v) = c \cdot T(v)$ for all $c \in \mathbb{F}, v \in V$.

> [!Example]- Example: Linear Transformations in $\mathbb{R}$
> 1. Let $V = C(\mathbb{R})$, the space of all continuous functions. We can define a map $S: V \to V$ (integration)
>    $$
>    S(f(t)) = \int_0^t f(s) \; ds
>    $$
>    Which is a linear transformation.
> 
> 2. Let $V = C^\infty (\mathbb{R})$, the space of all infinitely differentiable functions. We can define a map $S: V \to V$ (differentiation)
>    $$
>    S(f(t)) = f'(t)
>    $$
>    Which is a linear transformation.
>    
>    *Note: $V$ must be the space of all infinitely differentiable functions, as after taking a derivative, we move from space $C^n (\mathbb{R}) \to C^{n-1} (\mathbb{R}$.*
>    
> 3. We define $T: \mathbb{C} \to \mathbb{C}$
>    $$
>    T(a + ib) = T(z) = \bar{z} = a - ib
>    $$
>    This is certainly a real linear transformation, as it works over field $\mathbb{R}$. 
>    
>    But what about over $\mathbb{C}$?
>    By property of linear transformation, $(a - bi) T(1) = T(a - bi)$ must hold. However, $(a - bi) T(1) = a - bi \ne a + bi = T(a - bi)$. 
>    
>    Thus, we call this map $\mathbb{R}$ linear, but not $\mathbb{C}$ linear. Even though it is defined over the complex plane, it only works on field $\mathbb{R}$.

> [!Example]- Example: Properties of Linear Transformations
> How many linear transformations are there that satisfy
> $$
> T: \mathbb{R}^2 \to \mathbb{R}^3
> $$
> $$
> T(1,1) = T(1,2) = T(2,1) = (1,2,3)
> $$
> 
> None! We can prove this by counterexample. We know that
> $$
> 3 (1,1) = (2,1) + (1,2)
> $$
> But 
> $$
> T( 3(1,1) ) = (3,6,9) \ne (2,4,6) = T(2,1) + T(1,2)
> $$ 
> So no linear transformations satisfying this property exist.

### Transformations as Matrices
Any linear transformation $T: \mathbb{R}^n \to \mathbb{R}^m$ has a unique matrix representation, known as a **matrix transformation**.

Given an $m \times n$ matrix $A$, we define $T: \mathbb{R}^n \to \mathbb{R}^m$ as:
$$
T(v) = A \cdot v
$$ 
> To find $A$, we compute the linear transformation output for the standard basis vectors $e_i$, where $e_i$ gives us the $i^{th}$ column of $A$.

> [!Abstract] Theorem: Transformation Uniqueness
> Transformation $T: \mathbb{R}^n \to \mathbb{R}^m$ is determined uniquely by its values
> $$
> T(b_1), T(b_2), \cdots, T(b_n)
> $$
> for any basis $\{ b_1, \dots, b_n \}$ of $\mathbb{R}^n$.

> [!Abstract] Theorem: Linear Transformations and Matrices
> Let $V$ be a vector space with basis $B = \{ b_1, b_2, \dots, b_n \}$, and $W$ be another vector space with basis $C = \{ c_1, c_2, \dots, c_m \}$. Let $T: V \to W$ be a linear transformation.
> 
> Then there exists a unique matrix $A \in M_{m \times n} (\mathbb{F})$ such that 
> $$
> A \cdot [v]_B = [ T(v) ]_C
> $$
> > There exists a matrix for the linear transformation which automatically converts between the two bases.
> 
> This matrix is denoted as $A$, the matrix of $T$ relative to $B$, $C$
> $$
> A = [T]_{C,B} : [T(v)]_C = [T]_{C,B} [v]_B
> $$
> > $[T]_{C,B}$ transforms a vector in basis $B$ to a transformed vector in basis $C$ ($B \to C$).
> 
> > [!Note]- Proof
> >
> > Let $b_i$ be the $i^{th}$ basis vector of $V$. Then,
> > $$
> > A \cdot [b_i]_B = [T(b_i)]_C \to A \cdot e_i = [T(b_i)]_C
> > $$
> > Showing that each column $i$ of $A$ is equal to $[ T(b_i) ]_C$.

> [!Example]- Example: Linear Transformations as Matrices
> Let $V = \mathbb{P}_3 (\mathbb{R})$ with basis $B = \{ 1, x, x^2, x^3 \}$ and $W = \mathbb{P}_2 (\mathbb{R})$ with basis $C = \{ 1, x, x^2 \}$. 
> 
> Define linear transformation $T: \mathbb{P}_3 (\mathbb{R}) \to \mathbb{P}_2 (\mathbb{R})$ as the derivative operator. Then
> $$
> [T]_{C,B} = \begin{bmatrix} 
> 	0 & 1 & 0 & 0 \\
> 	0 & 0 & 2 & 0 \\
> 	0 & 0 & 0 & 3
> 	\end{bmatrix}
> $$

> [!Example]- Example: Matrix Transformation
> Define $T: \mathbb{R}^2 \to \mathbb{R}^2$ as $T(a,b) = (a + 3b, 2a + 4b)$. Then, $A$ is
> $$
> A = \begin{bmatrix} 1 & 3 \\ 2 & 4 \end{bmatrix}
> $$
> 
> Given vector $(1,1)$, $T(1,1)$ is
> $$
> T(1,1) = \begin{bmatrix} 1 & 3 \\ 2 & 4 \end{bmatrix} \begin{bmatrix} 1 \\ 1 \end{bmatrix} = \begin{bmatrix} 4 \\ 6 \end{bmatrix}
> $$

### Compositions of Transformations
We can use ideas of transformation composition to find the matrices for complex transformations, by combining multiple elementary transformations together.

Suppose we have vector spaces 
- $U$ with basis $A$ and dimension $p$ 
- $V$ with basis $B$ and dimension $n$
- $W$ with basis $C$ and dimension $m$ 

Now suppose we have transformations $S: U \to V$ and $T: V \to W$. Then, if all transformations are linear, then
$$
[T \cdot S]_{C,A} = [T]_{C,B} \cdot [S]_{B,A}
$$
Where 
- $[T \cdot S]_{C,A}$ is an $m \times p$ matrix
- $[T]_{C,B}$ is a $m \times n$ matrix
- $[S]_{B,A}$ is a $n \times p$ matrix.

> Multiplying the matrices together will yield us a transformation from $U \to W$. 

> [!Abstract] Theorem: Linearity of Compositions
> If$S: U \to V$ and $T: V \to W$ are linear transformations, then $T \cdot S$ is also a linear transformation.

Now consider an **identity transformation $Id$**, one such that $T: V \to V$ maps back to the same vector space. 

Define $B$ and $C$ as bases of $V$. Then,
$$
[Id]_{B,B} \cdot [v]_B = [v]_B \qquad [Id]_{B,C} \cdot [Id]_{C,B} \cdot [v]_B = [v]_B
$$
$$
[Id]_{B,B} = I_{n \times n} = [Id]_{B,C} \cdot [Id]_{C,B}
$$
Thus, the transformations $[Id]_{B,C}$ and $[Id]_{C,B}$ must be inverses of one another! 
> This means we can find $T: C \to B$ in vector space $V$, by taking the inverse of $T: B \to C$ (and vice versa)!
> We can additionally use this to chain transformations in different bases together, by converting the bases to one another.

### Transformations and Differential Equations 
Take mapping $L: C^2 (\mathbb{R}) \to C^0 (\mathbb{R})$
$$
L(f(t)) = f'' + (1 - t^2) \; f' + 7f
$$
We can show that $L$ is linear, as $L(f + g) = L(f) + L(g)$, and $L(cf) = c L(f)$.

1. Take 2nd order [[Ordinary Differential Equations | differential equation]]
$$
f'' + (1 - t^2) \; f' + 7f = 0
$$
With solutions $f(t)$ satisfying this relationship. Comparing with our mapping $L$, the solutions of this differential equation are the kernel of $L$, $ker(L)$!
$$
L(f) = 0
$$

2. Now take another 2nd order differential equation
$$
f'' + (1 - t^2) \; f' + 7f = \sin(t)
$$
With solutions satisfying this relationship. Comparing with our mapping $L$, the solutions of this differential equation satisfy
$$
L(f) = \sin(t)
$$
Or in other words, the solutions must all map to a function in $W$, $\sin(t)$! 
> So we ask, is **forcing function** $\sin(t) \in Im(L)$?

In both examples, if we find the finite dimensional subspace in $C^2 (\mathbb{R})$, and find what functions (vectors) span this subspace, we can find **all** solutions to the differential equation!

## Kernel and Image
We define the **kernel** of linear transformation $T: V \to W$ as
$$
ker(T) = \{ v \in V \; | \; T(v) = \vec{0}_W \}
$$
Or in other words, the set of all inputs of the linear transformation, which map to $\vec{0}$ in the codomain (the nullspace of $A$).
> We can show that $ker(T) \subseteq T$.
> $ker(T)$ is equivalent to the solution set of $A \cdot v = 0$.

We define the **image (range)** of linear transformation $T: V \to W$ as
$$
Im(T) = \{ w \in W \; | \; w = T(v) \text{ for some } v \in V \}
$$
Or in other words, the set of all outputs of the linear transformation.
> $Im(T)$ is equivalent to the column space of standard matrix $A$ representing $T$.

> [!Example]- Example: Kernel and Image
> 1. We define following linear transformation $T: \mathbb{R} \to \mathbb{R}$:
>    $$
>    T(x,y) = (x + y, x + y)
>    $$
>    
>    The kernel of the linear transformation is the line $y = -x$. 
>    The image of the linear transformation is the line $y = x$.
>   
> 3. From before, we defined linear transformation $D: V \to V$ 
>    $$
>    D(f(t)) = f'(t)
>    $$
>    
>    The kernel of the linear transformation is all constant functions.
>    The image of the linear transformation is all continuous functions.

> [!Example]- Example: Kernel and Image 2
> Take linear mapping $S: C(\mathbb{R}) \to C(\mathbb{R})$
> $$
> S(f(t)) = \frac{f(t) + f(-t)}{2}
> $$
> 
> The only functions mapping $S(f(t)) = 0$ are those where $f(t) = -f(-t)$, or in other words, all odd functions.
> 
> Thus, the kernel of $S$ is the set of all odd functions.
> 
> Let $h(t) = \frac{f(t) + f(-t)}{2}$. We show $h(-t) = \frac{f(-t) + f(t)}{2}$, so $h(t) = h(-t)$, or in other words, an even function. 
> 
> Thus, $Im(T)$ is the set of all even functions.

> [!Example]- Example: Image and Kernel 3
> Define $L: \mathbb{P}_5 \to \mathbb{R}^2$ as the linear transformation where 
> $$
> L(f(t)) = \begin{bmatrix} f(1) \\ f(2) \end{bmatrix}
> $$ 
> 
> ##### What is $L$'s Image and Kernel?
> We show that we can obtain $(1,0)$ using polynomial $2 - t$. 
> We also show that we can obtain $(0,1)$ using polynomial $t - 1$.
> 
> Thus, $dim(Im(T)) = 2$, and as $\mathbb{R}^2$ is a 2 dimensional space, the other dimensions in $\mathbb{P}_5$ must have been collapsed.
> Thus, $ker(T) = 4$.
> 
> ##### What is the Basis for $L$'s Kernel?
> The kernel is formed from all functions such that $f(1) = 0 = f(2)$. In other words, polynomials with roots at 1 and 2!
> $$
> p(t) = (t - 1) (t - 2)
> $$
> We find the kernel to be
> $$
> \{ p(t), t p(t) , t^2 p(t), t^3 p(t) \}
> $$

> [!Abstract] Theorem: Rank-Nullity
> If $T: V \to W$ is a linear mapping, and $V$ is finite dimensional, then:
> $$
> dim(V) = dim(ker(T)) + dim(Im(T))
> $$
> 
> > [!Note]- Proof
> >
> > Let $\{ u_1, \dots, u_k \}$ be a basis for $ker(T)$, and $\{ w_1, \dots, w_l \}$ be a basis for $Im(T)$.
> > 
> > Pick vectors $v_1, \dots, v_l$ such that $T(v_i) = w_i$, and define set $S = \{ u_1, \dots, u_k, v_1, \dots, v_l \}$. 
> > 
> > ---
> > *Proof of Span*
> > Let $v \in V$. Consider $T(v) \in Im(T) \subseteq W$. By definition of basis, we can write
> > $$
> > T(v) = d_1 w_1 + \dots + d_l w_l
> > $$
> > $$
> > \to T(v) - d_1 w_1 - \dots - d_l w_l = 0
> > $$
> > By property of linear transformation (addition), this is equivalent to
> > $$
> > v - d_1 w_1 - \dots - d_l w_l = 0 \to T(v) - T(v) = 0 \in W
> > $$
> > Define $z = v - d_1 v_1 - \dots - d_l v_l \in ker(T)$. By definition of basis, we can find $c_1, \dots, c_k$ such that
> > $$
> > z = c_1 u_1 + \dots + c_k u_k
> > $$
> > Which we can apply algebra to to obtain
> > $$
> > v = d_1 v_1 + \dots + d_l v_l + c_1 u_1 + \dots + c_k u_k
> > $$
> > Proving that the vectors in set $S$ spans $V$.
> > 
> > ---
> > *Proof of Linear Independence*
> > Now take the vectors in set $S$.
> > $$
> > c_1 u_1 + \dots + c_k u_k + d_1 v_1 + \dots + d_l v_l = 0
> > $$
> > Applying the transformation to both sides, we obtain
> > $$
> > T(0) = c_1 T(u_1) + \dots + c_k T(u_k) + d_1 v_1 + \dots + d_l v_l = 0
> > $$
> > $$
> > 0 = d_1 v_1 + \dots + d_l v_l
> > $$
> > But because we know $\{ v_1, \dots, v_l \}$ is a basis, $d_1, \dots, d_l$ must be 0. If this is the case, then as $\{ u_1, \dots, u_k \}$ is a basis as well, $c_1, \dots, c_k$ must also be 0.
> > This, the vectors in set $S$ is linearly independent.
> > 
> > Because we know the vectors in $S$ are linearly independent and spans $V$,  it must be a basis for $V$. Thus, the size of $S$ ($dim(V)$) is equal to the sum of the number of basis vectors in the kernel ($ker(T)$) and the image ($Im(T)$.

> [!Example]- Example: Rank-Nullity 
> Suppose we have set
> $$
> \{ f \in \mathbb{P}_5(\mathbb{R}) \; \vert \; f(1) = 0, f(2) = 0 \}
> $$
> 
> Now define a linear mapping $L: \mathbb{P}_5 (\mathbb{R}) \to \mathbb{R}^2$
> $$
> L(f) = \begin{bmatrix} f(1) \\ f(2) \end{bmatrix}
> $$
> 
> We know there exists polynomials such that $f(1) = 1, f(2) = 0$ and $f(1) = 0, f(2) = 1$. Thus, $Im(L) = \mathbb{R}^2 \to dim(Im(L)) = 2$.
> 
> By the Rank-Nullity theorem, then, $dim(ker(L)) = 6 - 2 = 4$.

### Isomorphisms
Let $T: V \to W$ be a linear transformation.

$T$ is **one to one (injective)**, if for arbitrary vector $w \in W$, there is at most one vector $v$ that maps to it.
> In other words, $T(v_1) = T(v_2)$ is only true when $v_1 = v_2$.

> [!Abstract] Theorem: Kernel and Injection
> Let $T$ be a linear transformation. Then, $T$ is injective if and only if $ker(T) = \{ 0 \}$. 

$T$ is **onto (surjective)**, if for any arbitrary vector $w \in W$, there is at least one vector $v$ that maps to it.
> In other words, $Im(T) = W$ ($T$ maps onto the entire output domain).

$T$ is an **isomorphism** if and only if $T$ is both injective and surjective.
> In other words, all vectors $w \in W$ have one vector $v \in V$ which map to it.
> We commonly denote an isomorphic linear transformation as $T: V \tilde{\to} W$.

> [!Abstract] Theorem
> If $T: V \to W$ is a linear map, $T$ is an isomorphism if and only if 
> $$
> ker(T) = \{ \vec{0} \} \qquad Im(T) = W
> $$
> 
> >  If $T$ has standard matrix $A$, then $A$ must be invertible for $T$ to be an isomorphism.
> > However, not all linear transformations have a matrix.

> [!Example]- Example: Non-Invertible Isomorphism
> The isomorphic linear transformation 
> $$
> T: M_{2 \times 2} (\mathbb{R}) \tilde{\to} \mathbb{R^4}
> $$
> 
> Does not have any invertible matrix (it is not from $\mathbb{R^n} \to \mathbb{R^m}$).

If $T: V \tilde{\to} W$, then anything that occurs in $V$ also occurs in $W$.
> Properties of a set $\{ v_1, v_2, \dots, v_k \}$ for $V$ can all be found in the set $\{ T(v_1), T(v_2), \dots, T(v_k) \}$ for $W$.

> [!Example]- Example: Isomorphic Properties
> Given a linear transformation $T: V \to W$, if $\{ v_1, v_2, \dots, v_k \}$ is a basis for $V$, then $\{ T(v_1), T(v_2), \dots, T(v_k) \}$ is a basis for $W$.

> [!Example]- Example: Applying Isomorphic Properties
> Is $\{ 1 + t^2 - t^3, 7 - t + t^4, t + t^2 - t^3 \} \subset \mathbb{P}_4$ linearly independent?
> 
> Let $B = \{ 1, t, t^2, t^3, t^4 \}$ be a basis for $\mathbb{P}_4$.
> 
> Now, we can apply isomorphic linear transformation $T: \mathbb{P}_4 \to \mathbb{R}^5$ such that each of the basis vectors maps to
> $$
> \begin{bmatrix} 1 \\ t \\ t^2 \\ t^3 \\ t^4 \end{bmatrix} \to \begin{bmatrix} 1 \\ 1 \\ 1 \\ 1 \\ 1 \end{bmatrix}
> $$
> 
> We apply this transformation to the set 
> $$
> \{ 1 + t^2 - t^3, 7 - t + t^4, t + t^2 - t^3 \} \to \{ (1, 0, 1, -1, 0), (7, -1, 0, 0, 1), (0, 1, 1, -1, 0) \}
> $$
> Which we can sub into a matrix and row reduce to see if it is linearly independent. If the transformed set is linearly independent, then so is the original (as the isomorphism preserves properties of sets).

# Eigenvalues
Define $A \in M_{n \times n}(\mathbb{F})$ as an $n \times n$ matrix. 

Then, a nonzero vector $v \in V$ satisfying
$$
A \cdot v = \lambda v
$$
Where $\lambda \in \mathbb{F}$ is an **eigenvector** with **eigenvalue** $\lambda$. Together, $(\lambda, v)$ is known as an **eigenpair**.

Matrices can have eigenvalues and eigenvectors in the complex field!

>[!Info] Eigenvalues and Linear Transformations
> We can think of $A$ as a linear transformation $T: V \to V$, under field $\mathbb{F}$, where the eigenvectors $v \in V$ are vectors mapping to a scalar multiple of themselves 
> $$
> A \cdot v = T(v) = \lambda v
> $$

> [!Example]- Example: Linear Transformations and Eigenvalues
> Define $D: C^\infty (\mathbb{R}) \to C^\infty (\mathbb{R})$ as the derivative operator, such that
> $$
> D(f) = f'
> $$
> 
> The eigenpairs of $D(f)$ are such that $f = \lambda f'$, or in other words, the $e^{\lambda t}$ function
> $$
> \frac{d}{dt} e^{\lambda t} = \lambda e^{\lambda t}
> $$
> Thus, the eigenpairs of the transformation are $(\lambda, e^{\lambda t}) : \lambda \in \mathbb{R}$.

## Characteristic Polynomials
We define
$$
P_A(z) = det(A - zI)
$$
as the **characteristic polynomial** of matrix $A \in M_{n \times n}(\mathbb{F})$, such that the roots of $P_A(z)$ are the eigenvalues of $A$.
> We use $P_A(A)$ to find $A$'s eigenvalues.

> [!Note]- Proof (Sketch)
> Let $A \in M_{n \times n}(\mathbb{F})$. We want to solve
> $$
> A v = \lambda v : v \in \mathbb{F}^n / 0, \lambda \in \mathbb{F}
> $$
> $$
> \to Av = \lambda I v \to (A - \lambda I) v = 0
> $$
> 
> Because $v$ is a nonzero vector, then $(A - \lambda I)$ cannot be invertible ($v$ lies in its kernel). Thus, we solve for
> 
> $$
> det(A - \lambda I) = 0
> $$
> To find values $\lambda \in \mathbb{F}$ such that $A - \lambda I$ are noninvertible.

> [!Abstract] Theorem: Properties of Eigenvalues
> Let $\lambda_1, \dots, \lambda_n$ be eigenvalues of $A$. Then,
> - $tr(A)$ is equal to the sum of $A$'s eigenvalues.
> - $det(A)$ is the product of $A$'s eigenvalues.

## Similar and Diagonalizable Matrices
Let $A, B \in \mathbb{M}_{n \times n}(\mathbb{F})$ be matrices. We say $A$ and $B$ are **similar matrices** if there exists an invertible matrix $P$ such that
$$
B = P^{-1} A P
$$

> [!Abstract] Theorem: Similar Matrices and Eigenvalues 
> Similar matrices have the same eigenvalues.

Moreover, $A$ is **diagonalizable** if  $A$ is similar to a diagonal matrix $D$.
$$
A = P D P^{-1} \iff D = P^{-1} A P
$$

> [!Abstract] Theorem: Diagonalizable Matrices
> Let $A \in M_{n \times n} (\mathbb{F})$. Then $A$ is diagonalizable if and only if there exists $n$ linearly independent eigenvectors for $A$ on $\mathbb{F}^n$.
> 
> The, let $(\lambda_1, v_1), \dots, (\lambda_n, v_n)$ be eigenpairs of $A$. Then
> $$
> A = P D P^{-1}
> $$
> Where
> $$
> P = \begin{bmatrix} 
> 	v_1 & \dots & v_n \\
> 	\downarrow & \dots & \downarrow
> 	\end{bmatrix}
> $$ 
> $$
> D = \begin{bmatrix} 
> 	\lambda_1 & 0 & \dots & 0 \\
> 	0 & \lambda_2 & \dots & 0 \\
> 	\vdots & \vdots & \ddots & \vdots \\
> 	0 & 0 & \dots & \lambda_n
> 	\end{bmatrix}
> $$
> Because $P$ is formed from basis vectors, we know $P$ is invertible.

> [!Example]- Example: Diagonalizable Matrices
> $$
> A = \begin{bmatrix} 
> 	2 & 1 & 2 \\
> 	0 & 3 & 2 \\ 
> 	0 & 0 & 5
> 	\end{bmatrix}
> $$
> 
> We know the eigenvalues of $A$ are the roots of $p(z) = det(A - zI)$.
> $$
> p(z) = (2 - z) (3 - z) (5 - z) \to \lambda = 2, 3, 5
> $$
> The eigenpairs of $A$ are
> $$
> (2, v_1), (3, v_2), (5, v_3)
> $$
> 
> We now solve for the corresponding eigenvectors. We solve for the vectors as so
> $$
> A v_1 = 2 v_1 \qquad A v_2 = 3 v_2 \qquad A v_3 = 5 v_3
> $$
> $$
> \to (A - 2I) v_1 = 0 \qquad (A - 3I) v_2 = 0 \qquad (A - 5I) v_3 = 0
> $$ 
> 
> We can then use these eigenvectors and eigenvalues to diagonalize $A$.

> [!Abstract] Theorem: Linearly Independent Eigenvectors
> If $v_1, \dots, v_k$ are eigenvectors of $A$ with distinct eigenvalues, then the set $\{ v_1, \dots, v_k \}$ is linearly independent.
> 
> Thus, if $A$ has $n$ distinct eigenvalues, then $A$ must be diagonalizable.

### Matrix Exponentials
Let $A \in M_n (\mathbb{F})$. We define $e^A$, the **exponential** of matrix $A$ such that
$$
e^A = I + A + \frac{A^2}{2} + \dots = \sum_{k=0}^\infty \frac{A^k}{k!}
$$

Exponentials have the following properties:
1. $det(e^A) = e^{tr(A)}$
2. $(e^A)^{-1} = e^{-A}$
3. $e^{A + B} = e^A \cdot e^B$ if and only if $AB = BA$

Diagonalizable matrices are quite useful in exponentials. Using a diagonalizable matrix creates a converging sum in each diagonal cell.
$$
e^D 
	= \sum_{k=0}^\infty \frac{A^k}{k!} 
	= \begin{bmatrix}
		\sum \frac{d_1^k}{k!} & 0 & \dots & 0 \\
		0 & \sum \frac{d_2^k}{k!} & \dots & 0 \\
		\vdots & \vdots & \ddots & \vdots \\
		0 & 0 & \dots & \sum \frac{d_n^k}{k!}
	\end{bmatrix}
	=\begin{bmatrix}
	e^{d_1} & 0 & \dots & 0 \\
	0 & e^{d_2} & \dots & 0 \\
	\vdots & \vdots & \ddots & \vdots \\
	0 & 0 & \dots & e^{d_n}
	\end{bmatrix}
$$

Being able to express $A$ as a diagonal matrix also allows us to easily calculate $e^A$
$$
A = P D P^{-1} \to A^k = P D P^{-1} P D P^{-1} \dots = P D^k P^{-1}
$$
$$
\to e^A = \sum \frac{P D^k P^{-1}}{k!} = P \left(\sum \frac{D^k}{k!}\right) P^{-1} = P e^D P^{-1}
$$

### Cayley-Hamilton Theorem
> [!Abstract] Theorem
> Let $A \in M_{n \times n}(\mathbb{F})$, and let $P_A(z)$ be the characteristic polynomial of $A$.
> 
> Then, $A$ is a root of its own characteristic polynomial.
> $$
> P_A (A) = 0
> $$

# Jordan Canonical Form
## T-Invariance
Let $T: V \to V$ be a linear map, where $V$ is a vector space over $\mathbb{C}$ with dimension $n$.

A subspace $W \subset V$ is **T-invariant** if $v \in W \to Tv \in W$. Or in other words, $T$ maps vectors in $W$ to vectors in $W$ ($TW \subseteq W$).
> We observe that 1 dimensional invariant subspaces correspond to eigenvectors of $T$.

> [!Example]- Example: 1 Dimensional T-Invariant Subspace
> Define $T: \mathbb{C}^3 \to \mathbb{C}^3$ such that
> $$
> \begin{bmatrix}
> 	3 & 5 & 0 \\ 
> 	5 & 3 & 0 \\
> 	0 & 0 & 6 \\
> 	\end{bmatrix}
> $$
> 
> We can find eigenvectors of $A$
> $$
> v_1 = \begin{bmatrix}
> 	1 \\ 1 \\ 0
> 	\end{bmatrix}
> 	\qquad
>    v_2 = \begin{bmatrix}
> 	1 \\ -1 \\ 0
> 	\end{bmatrix}
> 	\qquad
>    v_3 = \begin{bmatrix}
> 	0 \\ 0 \\ 1
> 	\end{bmatrix}
> $$
> 
> The spans of each eigenvector $span(v_1), span(v_2), span(v_3)$ are all T-invariant. 

We define a **flag** in $V$ as a sequence of subspaces
$$
0 \subset V_1 \subset V_2 \subset V_3 \subset \dots \subset V_n = V
$$
Where $dim(v_i) = i$.
> An ordered basis $B = \{ b_1, \dots, b_n \}$ of $V$ gives a flag of $V$.
> $$
> \begin{align*}
> 	V_1 &= span\{b_1\} \\
> 	V_2 &= span\{b_1, b_2\} \\
> 	&\vdots \\
> 	V_i &= span\{b_1, b_2, \dots, b_i\}
> \end{align*}
> $$

A flag is **T-invariant** if all $V_i$ is T-invariant.

> [!Abstract] Theorem: T-Invariant Flags and Matrices
> If $B = \{ b_1, \dots, b_n \}$ is an ordered basis of $V$ such that the corresponding flag
> $$
> V_i = span\{ b_1, \dots, b_i \}
> $$
> is T-invariant, then there exists a linear map $[T]_{B,B}$ in this basis $B$ whose matrix is upper triangular.
> 
> > The converse is true!
> 
> > [!Note]- Proof
> >
> > Because we know all $V_i$ is T-invariant, we know that for some vector $b_i \in V_i$,
> > $$
> > Tb_i = a_{1i} b_1 + a_{2i} b_2 + \dots + a_{ii} b_i
> > $$
> > Because we know by definition that $T b_i \in V_i$.
> > 
> > Constructing a matrix $A$ for $T$, we obtain an upper triangular matrix.

> [!Abstract] Theorem: Upper Triangular Matrices
> If $V$ is a $\mathbb{C}$-vector space with $dim(V) = n > 1$, and $T: V \to V$ is a linear map, then there exists a basis $B$ of $V$ such that $[T]_{B,B}$ is upper triangular.
> > **Corollary**: If $A$ is the standard matrix to $T$, then as eigenvalues are preserved on different bases, $A$ is similar to an upper triangular matrix.
> > $$
> > A = P^{-1} M P
> > $$
> > Where $M$ is an upper triangular matrix.
> 
> > [!Note]- Proof
> > 
> > We prove this by constructing a T-invariant flag for $T$, using induction.
> > 
> > **Base Case**: In the $n = 1$ case, we have a $1 \times 1$ matrix $T$, which by default is upper triangular.
> > 
> > **Inductive Hypothesis**: For $n > 1$, assume the theorem is true for all vector subspaces $W$ of dimension $n - 1$ and all linear maps $S: W \to W$.
> > 
> > **Inductive Step**: Take a basis $C = \{c_1, \dots, c_n \}$ of $V$, and take the characteristic polynomial of standard matrix $A$, $P_A(z)$. We know that for any basis, $P_A(z)$ will be the same. 
> > 
> > We know by the **Fundamental Theorem of Algebra** that $P_A(z)$ has a root $\lambda_1$ in $\mathbb{C}$. So, if we take an eigenvector $v \in \mathbb{C}^n$ for $\lambda_1$, 
> > $$
> > Av = \lambda_1 v \to Tv = \lambda_1 v
> > $$
> > Showing that we can find a $V_1 = span\{ v \}$ which is T-invariant.
> > 
> > We can extend $v$ to a basis $\{ v_1, v_2', \dots, v_n' \}$ of $V$. Taking $W = span\{ v_2', \dots, v_n' \} \subset V$, we see that $dim(W) = n - 1$.
> > Then, we define transformation $S: W \to W$ such that $S(w) = P(T(w))$, where $w \in W$ - or in other words, the projection of $T(w)$ onto $W$.
> > 
> > By the induction hypothesis, there exists an $S$-invariant flag of $W$.
> > 
> > **Conclusion:** Using the induction hypothesis, we can construct
> > $$
> > \begin{align*}
> > 	V_1 &= span\{v_1\} \\
> > 	V_2 &= span\{v_1, w_1 \} \\
> > 	V_3 &= span\{v_1, w_1, w_2 \} \\
> > 	&\vdots \\
> > 	V_i &= span\{v_1, w_1, \dots, w_{i-1}\} \\
> > 	&\vdots \\
> > 	V_n &= span\{v_1, v_2, \dots, v_n \}
> > \end{align*}
> > $$
> > Which is a T-invariant flag.
> 
> We can find this upper triangular matrix, by finding the **Jordan Canonical Form** of a matrix.

## Shift Maps
We define a **shift map** $S: \mathbb{R}^n \to \mathbb{R}^n$  as a linear transformation such that
$$
\begin{align*}
	S(e_n) &= e_{n-1} \\
	S(e_{n-1}) &= e_{n-2} \\
	&\vdots \\
	S(e_1) &= 0
\end{align*}
$$
> From this, we also observe that $S^2 (e_{n}) = e_{n-2}$.

The matrix of the map is
$$
A = \begin{bmatrix}
	0 & 1 & 0 & \cdots & 0 \\
	0 & 0 & 1 & \cdots & 0 \\
	0 & 0 & 0 & \cdots & 0 \\
	\vdots & \vdots & \vdots & \ddots & \vdots \\
	0 & 0 & 0 & \cdots & 0
	\end{bmatrix}
$$

We define the characteristic polynomial of $A$ as
$$
P_A(z) = \pm z^n
$$
> By the [[Linear Algebra#Cayley-Hamilton Theorem | Cayley-Hamilton Theorem ]], $A^n = 0$.

We observe that with the shift matrix, the kernel is as follows:
$$
\begin{align*}
	ker(S) &= span\{ e_1 \} \\
	ker(S^2) &= span\{ e_1, e_2 \} \\
	ker(S^3) &= span\{ e_1, e_2, e_3 \} \\
	&\vdots \\
	ker(S^n) &= \mathbb{F}^n
	\end{align*}
$$
> For every additional transformation, we shift another basis vector to the 0 vector.

## Jordan Matrices
As proven above, we've shown that all $n \times n$ matrices are similar to some upper triangular matrix.
> If a matrix $A$ does not have enough linearly independent eigenvectors to be diagonalized, what's the next best option?

We define a **Jordan Matrix** as an $n \times n$ matrix composed of $m \times m$ diagonal blocks ($m \le n$), called **Jordan Blocks**
$$
\begin{bmatrix}
	\lambda & 1 & 0 & \cdots & 0 \\
	0 & \lambda & 1 & \cdots & 0 \\
	0 & 0 & \lambda & \cdots & 0 \\
	\vdots & \vdots & \vdots & \ddots & \vdots \\
	0 & 0 & 0 & \cdots & \lambda
	\end{bmatrix}
$$
	
Where $\lambda$ is some eigenvalue.

> [!Abstract] Theorem: Jordan-Canonical Form
> Every matrix $A \in M_n (\mathbb{C})$ is similar to a unique Jordan matrix such that
> $$
> A = P J P^{-1}
> $$
> where $P$ is an invertible matrix formed of generalized eigenvectors of $ker((A - \lambda I)^k)$.
> 
> This is known as the **Jordan Canonical Form** of $A$.
> 
> > **Corollary:** All linear transformations $T: V \to V$ are equivalent to some scaling and some shift with respect to some basis $B$ 
> > (All Jordan blocks $J$ are equal to $S + \lambda I$, where $\lambda$ is an eigenvalue and $S$ is a [[Linear Algebra#Shift Map | shift map]], so all transformations $Av = S(v) + \lambda v$)

Why are we interested in the Jordan matrix? One application is with [[Linear Algebra#Matrix Exponentials | matrix exponentials]], as seen with diagonal matrices. 

Say we have matrix $A$ with Jordan form $J = P^{-1} AP \to A = P J P^{-1}$. Computing $e^A$, we see that
$$
e^A = \sum_{n=0}^\infty \frac{A^n}{n!} = \sum_{n=0}^\infty \frac{(P J P^{-1})^n}{n!} = \sum_{n=0}^\infty P \frac{J^n}{n!} P^{-1} = P e^J P^{-1}
$$
Where $J$ is $A$'s Jordan matrix, and $e^J$ is the matrix with diagonals $e^{J_\lambda}$, where $J_\lambda$ is some Jordan block in the matrix. We can easily compute the Jordan block exponential as
$$
e^{J_\lambda} = e^{\lambda I} \cdot e^S
$$
Because $J_\lambda = \lambda I + S$, and $\lambda I S = \lambda S I$ (so the property $e^{A + B} = e^A e^B$ holds). We know $e^S$ is a finite sum, as $S^n = 0$.
> It's still annoying to calculate, but definitely doable as there's only a finite number of terms.

> [!Example]- Example: Exponentiating a Jordan Block
> Say we have Jordan Block
> $$
> J = \begin{bmatrix}
> 	4 & 1 & 0 \\ 
> 	0 & 4 & 1 \\
> 	0 & 0 & 4
> 	\end{bmatrix}
> $$
> How do we find $e^J$?
> 
> First, observe that $J = 4I + S$, where $S$ is the $3 \times 3$ shift matrix. Then, we can take $e^J = e^{4I + S} = e^{4I} e^{S}$.
> $$
> e^{4I} = \begin{bmatrix}
> 	\sum_{n=0}^\infty \frac{4^n}{n!} & 0 & 0 \\ 
> 	0 & \sum_{n=0}^\infty \frac{4^n}{n!} & 0 \\
> 	0 & 0 & \sum_{n=0}^\infty \frac{4^n}{n!}
> 	\end{bmatrix} = \begin{bmatrix}
> 	e^4 & 0 & 0 \\ 
> 	0 & e^4 & 0 \\
> 	0 & 0 & e^4
> 	\end{bmatrix}
> $$
> $$
> e^S = I + S + \frac{S^2}{2} + \frac{S^3}{3!} + \dots
> $$
> > **Note**: $e^{cI}$ for any $c$ is equal to $e^c I$!
> 
> But we know that $S^3 = 0$! So, we obtain expression
> $$
> I + S +  \frac{S^2}{2} = \begin{bmatrix}
> 	1 & 1 & \frac{1}{2} \\ 
> 	0 & 1 & 1 \\
> 	0 & 0 & 1
> 	\end{bmatrix}
> $$
> And compute our exponential as
> $$
> e^J = (e^4 I) 
> \begin{bmatrix}
> 	1 & 1 & \frac{1}{2} \\ 
> 	0 & 1 & 1 \\
> 	0 & 0 & 1
> 	\end{bmatrix} = 
> 	\begin{bmatrix}
> 	e^4 & e^4 & \frac{e^4}{2} \\ 
> 	0 & e^4 & e^4 \\
> 	0 & 0 & e^4
> 	\end{bmatrix}
> $$ 

### Solving for the Jordan Form
Given an eigenvalue $\lambda$, the number of Jordan blocks for $\lambda$ is equal to $dim(ker(A - \lambda I))$, the number of linearly independent eigenvectors corresponding to $\lambda$. 
> Each Jordan block will have one eigenvector of $\lambda$, with the rest being generalized eigenvectors.

A **generalized eigenvector** of $A \in M_n (\mathbb{C})$ with eigenvalue $\lambda$ is a non-zero vector $v$ such that
$$
(A - \lambda I)^k v = 0 \qquad k \ge 1
$$
> For $k = 1$, $v$ is an eigenvector.

Now suppose we have a Jordan Block $A$ such that
$$
A = \begin{bmatrix}
	\lambda & 1 & 0 & \cdots & 0 \\
	0 & \lambda & 1 & \cdots & 0 \\
	0 & 0 & \lambda & \cdots & 0 \\
	\vdots & \vdots & \vdots & \ddots & \vdots \\
	0 & 0 & 0 & \cdots & \lambda
	\end{bmatrix}
$$
Suppose we solve for the eigenvectors of $A$. We see that 
$$
\begin{align*}
	&ker(A - \lambda I) = ker(S) = span\{ e_1 \} \\
	&ker((A - \lambda I)^2) = ker(S^2) = span\{ e_1, e_2 \} \\
	&ker((A - \lambda I)^3) = ker(S^3) = span\{ e_1, e_2, e_3 \} \\
	&\vdots \\
	\end{align*}
$$
where $S$ is a shift map. So, for all $\lambda$, we guarantee that we will be able to find enough generalized eigenvectors to create a Jordan block for $\lambda$.

> [!Example]- Example: Determining Jordan Blocks
> Let $P_A(z) = (z - i)^3 (z - 3)^4 (z - 5)^6$. To diagonalize the matrix, we must have 13 linearly independent eigenvectors, which may not be true.
> 
> We find the number of Jordan blocks corresponding to each $\lambda$ by finding
> $$
> \begin{align*}
> 	&dim(ker(A - iI)) \le 3 \\
> 	&dim(ker(A - 3I)) \le 4 \\ 
> 	&dim(ker(A - 5I)) \le 5 
> 	\end{align*}
> $$
> Where $A$ is diagonalizable only if equality is obtained for all kernels.
> > For eigenvalues which are not repeated as a root, we guarantee they must have some linearly independent eigenvector (by definition).
> 
> For example, if $dim(ker(A - i I)) = 2$, there must be 2 Jordan blocks for $\lambda = i$, which must be
> $$
> \begin{bmatrix}
> 	i & 1 \\ 0 & i
> 	\end{bmatrix} \qquad 
> 	\begin{bmatrix}
> 	i
> 	\end{bmatrix}
> $$
> with one eigenvector per block (and the other vectors being generalized eigenvectors).

> [!Example]- Example: Solving for The Jordan Canonical Form
> $$
> A = \begin{bmatrix} 
> 	0 & 1 & 0 \\
> 	1 & 0 & -1 \\
> 	0 & 1 & 0
> 	\end{bmatrix}
> $$
> Taking standard basis vectors $e_1, e_2, e_3$, we see that
> $$
> \begin{align*}
> 	&e_1 \to_A e_2 \to_A e_1 + e_3 \to_A 0 \\
> 	&e_2 \to_A e_1 + e_3 \to_A 0 \\
> 	&e_3 \to_A -e_2 \to_A -e_1 - e_3 \to_A 0
> 	\end{align*}
> $$
> Because after 3 transformations, all basis vectors go to 0, $A^3 = 0$. Because of this, we know by the [[Linear Algebra#Cayley-Hamilton Theorem | Cayley Hamilton Theorem]] that the characteristic polynomial is $\lambda^3 = 0$ ($\lambda$ must satisfy A^3), so $A$ only has eigenvalue $\lambda = 0$.
> Moreover, we see that $Null(A) = e_1 + e_3$, as these basis vectors mapped to 0. This is only one vector, so we expect only one Jordan block for $A$ with eigenvalue $\lambda = 0$.
> 
> Thus, we expect 
> $$
> J = \begin{bmatrix} 
> 	0 & 1 & 0 \\ 
> 	0 & 0 & 1 \\ 
> 	0 & 0 & 0
> 	\end{bmatrix}
> $$
> We now find the generalized eigenvectors that form $P$. We start with $A$'s eigenvector $e_1 + e_3$. To choose the generalized eigenvectors, we take progressive $Null(A - \lambda I)^k$ for increasing $k$, whose dimension should increase (as shown above). Then, we choose vectors in each Nullspace which are not in the previous, to guarantee a linearly independent combination.
> $$
> \begin{align*}
> 	&Null(A - 0I) = e_1 + e_3 \\
> 	&Null((A - 0I)^2) = e_2 \\
> 	&Null((A - 0I)^3) = e_1  
> 	\end{align*}
> $$
> Giving us 
> $$
> P = \begin{bmatrix} 
> 	1 & 0 & 1 \\ 
> 	0 & 1 & 0 \\ 
> 	1 & 0 & 0
> 	\end{bmatrix}
> $$
