Linear Algebra Review VI
=======================

- Nate Olson
- July 28, 2016

# Overview
Covering sections 2.2 and 2.3, which focus on inverse matricies

# Section 2.2
Definition of the inverse matrix $\mathbf{A}^{-1}$ when $\mathbf{A}$.
$\mathbf{A}\mathbf{A}^{-1}=I$  
$\mathbf{A}^{-1}\mathbf{A}=I$  

Where $I$ is the identity matrix.  

_singular matrix_ non-invertible matrix  
_nonsingular matrix_ invertible matrix  

## Theorem 4
Formula for calculating the inverse of a $2 \times 2$ matrix.  

Let $\mathbf{A}=\begin{bmatrix} a & b\\ c & d \end{bmatrix}$.

If $ad-bc \neq 0$, then $\mathbf{A}$ is invertible and  

$$\mathbf{A}^{-1}=\frac{1}{ad-bc}
\begin{bmatrix}
d & -b\\ 
-c & a
\end{bmatrix}$$  

If $ab-bc=0$, then $\mathbf{A}$ is not invertible.  

$ad-bc$ is the _determinant_, chapter 3 focuses on determinants.  

## Theorem 5
If $A$ is an invertible $n \times n$ matrix, then for each $\mathbf{b}$ in ${\rm I\!R}^n$, the equation $A\mathbf{x}=\mathbf{b}$ has the unique solution $\mathbf{x}=A^{-1}\mathbf{b}$

## Theorem 6
Three parts  

1. If $A$ is an invertible matrix, then $A^{-1}$ is invertible and $(A^{-1})^{-1}=A$  
1. If $A$ and $B$ are $n \times n$ invertible matrices then so is $AB$, and the inverse of $AB$ is the product of the inverse of $A$ and $B$ in the reverse order. That is, $(AB)^{-1}=B^{-1}A^{-1}$  
1. If $A$ is an inversible matrix, then so is $A^T$, and the inverse of $A^T$ is the transpose of $A^{-1}$. That is $(A^T)^{-1}=(A^{-1})^T$  

__Elementary matrix__ ($E$) - obtianed by performing a single elementary row operation on an identity matrix.

Three kinds of elementary matricies, thoes that are products of the three elementary row operations replacement, interchange, and scaling (p. 7). 

$EA$ is the product of an elementary matrix and matrix $A$. 

## Theorem 7
An $n \times n$ matrix $A$ is invertible if and only if $A$ is row equibalent to $I_n$, and in this case, any sequence of elementary row operations that reduces $A$ to $I_n$ also transforms $I_n$ into $A^{-1}$.  

## Algorithm for finding $A^{-1}$  
Row reduce the augmented matrix $\begin{bmatrix} A & I \end{bmatrix}$. IF $A$ is row equivalent to $I$, then $\begin{bmatrix} A & I \end{bmatrix}$ is row equivalent to $\begin{bmatrix} I & A^{-1} \end{bmatrix}$. Otherwise, $A$ is not invertible.

# Section 2.3 
## Theorem 8

__The Invertible Matrix Theorem__  
Let $A$ be a square $n \times n$ matrix. Then the following statements are equivalent, all statements are _TRUE_ or all are _FALSE_.  

a. $A$ is an invertible matrix.  
b. $A$ is row equivalent to the $n \times n$ identity matrix.  
c. $A$ has $n$ pivot positions.  
d. The equation $A\mathbf{x}=0$ has only the trivial solution.  
e. The columns of $A$ form a linearly independent set.   
f. The linear transformation $x \mapsto A\mathbf{x}$.  
g. The equation $A\mathbf{x}=\mathbf{b}$ has at least one solution for each $\mathbf{b}$ in ${\rm I\!R}^n$.  
h. The columns of $A$ span ${\rm I\!R}^n$.
i. The linear transformation $\mathbf{x} \mapsto A\mathbf{x}$ maps ${\rm I\!R}^n$ onto ${\rm I\!R}^n$.  
j. There is an $n \times n$ matrix $C$ such that $CA=I$.  
k. There is an $n \times n$ matrix $D$ such that $AD=I$.  
l. $A^T$ is an invertible matrix.  

Continued thoughout the book, p. 179 (parts m - r), 312 (s & t), 479 (u - x)  

### Proof
See figure 1 page 129 for relationships between individual parts used in proof.

* Circular relationship between a, j, d, c, and b  
      - $a \mapsto j$ - by definition of an invertible matrix as $C=A^{-1}$  
      - $j \mapsto d$ - from exercise 23 section 2.1  
            + $CA=I$ and $Ax=0$ only has a singular solution.  
            + $CAx=C0=0$ therefore $I_nx=0$ and $x=0$, $Ax=0$ has not free variables and therefore only has the trivial solution. 
            Trivial solution is $x=0$, $Ax=0$ has a nontrivial solution if there is a nonzero vector $x$ that satisfies the equation.  
      - $d \mapsto c$ - there are no free variables therefore $A$ has $n$ pivot columns.  
      - $c \mapsto b$ - for a square $n \times n$ matrix with $n$ pivot positions the pivot positions must lie on the diagonal and therefore $I_n$ is the reduced echelon form of $A$.  
      - $b \mapsto a$ - by theorem 7 (see above).
* Circular relationship between a,k, and g  
      - $a \mapsto k$ - same as $a \mapsto j$  
      - $k \mapsto g$ - exercise 24 section 2.1
      - $g \mapsto a$ - exercise 24 section 2.2  
* Equivalence g, h, and i (applies for all matrices)  
      - Theorem 4 (section 1.4) and theorem 12 (a) section 1.9  
* Equivalence d, e, and f (applies for all matrices)  
      - Section 1.7 and Theorem 12 (b) section 1.9  
* Parts g and d link h, i and e, f to the rest of IMT  
* $a \Leftrightarrow a$ Theorem 6 (c) section 2.2.
            
      

## Theorem 9
Let $T: {\rm I\!R}^n \mapsto {\rm I\!R}^n$ be a linear transformation and let $A$ be the standard matrix for $T$. Then $T$ is invertible if and only if $A$ is an invertible matrix. In that case, the linear transfromation $S$ given by $S(\mathbf{x})=A^{-1}\mathbf{x}$ is the unqiue function satisfying (1) and (2).
 
(1) $S(T)(\mathbf{x})=\mathbf{x}$ for all $\mathbf{x}$ in ${\rm I\!R}^n$
(2) $T(S)(\mathbf{x})=\mathbf{x}$ for all $\mathbf{x}$ in ${\rm I\!R}^n$
