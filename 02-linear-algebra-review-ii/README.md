---
output: pdf_document
---
Linear Algebra Review II
=======================

- Nate Olson
- June 29, 2016

## Matricies and Linear Regression
What we are working towards....

$$ 
Y_i = \beta_0 + \beta_1 x_i + \varepsilon_i, i=1,\dots,N 
$$

as: 


$$
\,
\begin{pmatrix}
Y_1\\
Y_2\\
\vdots\\
Y_N
\end{pmatrix} = 
\begin{pmatrix}
1&x_1\\
1&x_2\\
\vdots\\
1&x_N
\end{pmatrix}
\begin{pmatrix}
\beta_0\\
\beta_1
\end{pmatrix} +
\begin{pmatrix}
\varepsilon_1\\
\varepsilon_2\\
\vdots\\
\varepsilon_N
\end{pmatrix}
$$

or simply: 

$$
\mathbf{Y}=\mathbf{X}\boldsymbol{\beta}+\boldsymbol{\varepsilon}
$$


## 1.3 Vector Equations

### Definitions  

* vector - a list of numbers
* column vector - one column matrix  
* zero vector - all values in a vector are zero  
* scalar - real numbers that have magnitude but no direction [wikipedia](https://en.wikipedia.org/wiki/Scalar_(mathematics))  
* span - subset of a vector 

### Parallelogram Rule for Addition
![http://i.stack.imgur.com/O6Ved.png](http://i.stack.imgur.com/O6Ved.png)

### Algebratic Properties of ${\rm I\!R}^n$
$\mathbf{u}$, $\mathbf{v}$, and $\mathbf{w}$ are vectors, where $c$ and $d$ are scalars  

1. $\mathbf{u} + \mathbf{v} = \mathbf{v} + \mathbf{u}$  
1. $(\mathbf{u} + \mathbf{v}) + \mathbf{w} = \mathbf{u} + (\mathbf{v} + \mathbf{w})$  
1. $\mathbf{u} + 0 = 0 + \mathbf{u} = \mathbf{u}$  
1. $\mathbf{u} + (-\mathbf{u}) = 0$, where $(-1)\mathbf{u} = -\mathbf{u}$  
1. $c(\mathbf{u} + \mathbf{v}) = c\mathbf{u} + c\mathbf{v}$  
1. $(c + d)\mathbf{u} = c\mathbf{u} + d\mathbf{u}$  
1. $c(d\mathbf{u}) = (cd)(\mathbf{u})$  
1. $1\mathbf{u} = \mathbf{u}$  



## 1.4 The Matrix Equation $A\mathbf{x} = \mathbf{b}$
$A$ is a $m\times n$ matrix, with columns $\mathbf{a}_1$, ..., $\mathbf{a}_n$, and if $\mathbf{x}$ is in ${\rm I\!R}^n$,  

$$
A\mathbf{x} = 
\begin{bmatrix}
      \mathbf{a}_1 & \mathbf{a}_2 & \dots & \mathbf{a}_n
\end{bmatrix} 
\begin{bmatrix}
x_1\\ 
x_2\\ 
\vdots \\
x_n\\ 
\end{bmatrix} = 
x_1\mathbf{a}_1 + x_2\mathbf{a}_2 + \dots + x_n\mathbf{a}_n$$
 
### Theorem 3
$\mathbf{A}$ is a $m\times n$ matrix with columns $\mathbf{a}_1, \dots, \mathbf{a}_n$,   $\mathbf{b}$ is in ${\rm I\!R}^m$  

The solutions of $x$ (and solution set for the augmented matrix) are all the same.  

- $\mathbf{A}x=\mathbf{b}$  
- $x_1\mathbf{a}_1 + x_2\mathbf{a}_2 + \dots + x_n\mathbf{a}_n = \mathbf{b}$   
- $\begin{bmatrix} \mathbf{a}_1 & \mathbf{a}_2 & \dots & \mathbf{a}_n & \mathbf{b}\end{bmatrix}$  

### Existence of Solutions
Only solution if and only if $\mathbf{b}$ is a linear combination of the columns of $A$

### Theorem 4
$\mathbf{A}$ is a $m \times n$ matrix. The following are all true or false.  

1. for all real $\mathbf{b}$, $\mathbf{A}x=\mathbf{b}$ has a solution  
1. for all real $\mathbf{b}$, $\mathbf{b}$ is a linear combination of columns in $\mathbf{A}$
1. column of $\mathbf{A}$ span ${\rm I\!R}^m$ - I think this means the columns are real as well  
1. $\mathbf{A}$ has a pivot position in every row.

### Computation of $A\mathbf{x}$  

Introduction of the identity matrix concept - the identity matrix is key to finding inverse of a matrix

![https://tfetimes.com/c-identity-matrix/](http://rosettacode.org/mw/images/math/f/e/1/fe1a9857fd0a471baec6c538220e1bc9.png)

### Theorem 5
Assuming the following,  

- $\mathbf{A}$ is a $m\times n$ matrix
- $\mathbf{u}$ and $\mathbf{v}$ are real vectors
- $c$ is a scalar

Then  

- $\mathbf{A}(\mathbf{u} + \mathbf{v}) = \mathbf{A}\mathbf{u} + \mathbf{A}\mathbf{v}$  
- $\mathbf{A}(c\mathbf{u}) = c(\mathbf{A}\mathbf{u})$  
