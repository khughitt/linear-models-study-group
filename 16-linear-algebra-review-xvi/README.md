-   [Section 7.1 Diagonalization of Symmetric Matrices](#section-7.1-diagonalization-of-symmetric-matrices)

<h1>
Linear Algebra Review XVI
</h1>
-   Nate Olson
-   Sept 26, 2016

Section 7.1 Diagonalization of Symmetric Matrices
-------------------------------------------------

### Definition of a Symmetric Matrix

-   ![A^T=A](http://chart.apis.google.com/chart?cht=tx&chl=A%5ET%3DA "A^T=A")
-   Square by definition
-   diagonal entries arbitrary, other entries occur in pairs - opposite side of diagonal

![](img/symmetric_matrix.svg) (source: [Wikipedia](https://wikimedia.org/api/rest_v1/media/math/render/svg/2b2d89d68e9a534aceef44b199cdcb8ef310f0dc)

**Diagonalization:** ![A=PDP^{-1}](http://chart.apis.google.com/chart?cht=tx&chl=A%3DPDP%5E%7B-1%7D "A=PDP^{-1}"), where ![D](http://chart.apis.google.com/chart?cht=tx&chl=D "D") is the diagonal

**Theorem 1**

If ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is symmetric, then any two eigenvectors from different eigenspaces are orthogonal.

PROOF??

**Orthognally Diagonalizable:** orthogonal matrix ![P](http://chart.apis.google.com/chart?cht=tx&chl=P "P") with diagonal matrix ![D](http://chart.apis.google.com/chart?cht=tx&chl=D "D"), ![A=PDP^T=PDP^{-1}](http://chart.apis.google.com/chart?cht=tx&chl=A%3DPDP%5ET%3DPDP%5E%7B-1%7D "A=PDP^T=PDP^{-1}")

**Theorem 2**

An ![n \\times n](http://chart.apis.google.com/chart?cht=tx&chl=n%20%5Ctimes%20n "n \times n") matrix ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is orthogonally diagonalizable if and only if ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is a symmetric matrix$

### The Spectral Theorem

*spectrum* - set of matrix eigenvalues

**QUESTION** Does this term only apply to sets of eigenvalues for symmetric matrices

**Theorem 3** **The Spectral Theorem for Symmetric Matrices**

An ![n \\times n](http://chart.apis.google.com/chart?cht=tx&chl=n%20%5Ctimes%20n "n \times n") symmetric matrix ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") has the following properties:

-   ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") has ![n](http://chart.apis.google.com/chart?cht=tx&chl=n "n") real eigenvalues, counting multiplicities.
-   The dimension of the eigenspace for each eigenvalue ![\\lambda](http://chart.apis.google.com/chart?cht=tx&chl=%5Clambda "\lambda") equals the multiplicity of ![\\lambda](http://chart.apis.google.com/chart?cht=tx&chl=%5Clambda "\lambda") as a root of the characteristic equation.
-   Eigenspaces are mutually orthogonal, in the sense that eigenvectors corresponding to differnt eigenvalues are orthogonal.
-   ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is orthogonally diagonalizable.

**spectral decomposition**(A): ![A= \\lambda\_1u\_1u\_1^T+\\lambda\_2u\_2u\_2^T+\\dots+\\lambda\_nu\_nu\_n^T](http://chart.apis.google.com/chart?cht=tx&chl=A%3D%20%5Clambda_1u_1u_1%5ET%2B%5Clambda_2u_2u_2%5ET%2B%5Cdots%2B%5Clambda_nu_nu_n%5ET "A= \lambda_1u_1u_1^T+\lambda_2u_2u_2^T+\dots+\lambda_nu_nu_n^T")
