-   [Determinants](#determinants)
    -   [Some geometric motivation](#some-geometric-motivation)
    -   [Other useful theorems we missed in chapter 3...](#other-useful-theorems-we-missed-in-chapter-3...)
-   [The Characteristic Equation](#the-characteristic-equation)
    -   [Overview](#overview)
    -   [Characteristic polynomials](#characteristic-polynomials)
    -   [Similarity](#similarity)
-   [Diagonalization](#diagonalization)
    -   [Overview](#overview-1)
    -   [The Diagonalization Theorem](#the-diagonalization-theorem)
-   [Tangent: spectral analysis of covariance matrices](#tangent-spectral-analysis-of-covariance-matrices)
    -   [Matrices with correlated features](#matrices-with-correlated-features)
-   [References](#references)

<h1>
Linear Algebra Review XI
</h1>
-   Keith Hughitt
-   Sept 02, 2016

Determinants
============

Some geometric motivation
-------------------------

### 2x2 matrices

A ![2 \\times 2](http://chart.apis.google.com/chart?cht=tx&chl=2%20%5Ctimes%202 "2 \times 2") matrix, ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"), can be viewed as a **linear map** which transforms the **standard basis vectors** (unit vectors pointing in the direction of the coordinate exes, in this case ![e\_x = (1,0)](http://chart.apis.google.com/chart?cht=tx&chl=e_x%20%3D%20%281%2C0%29 "e_x = (1,0)") and ![e\_y = (0, 1)](http://chart.apis.google.com/chart?cht=tx&chl=e_y%20%3D%20%280%2C%201%29 "e_y = (0, 1)")) to the rows (or columns) of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A").

The image of the basis vectors form a parallelogram representing the transformation applied to the unit square:

![](img/800px-Area_parallellogram_as_determinant.svg.png)

(source: [Wikipedia](https://en.wikipedia.org/wiki/Determinant#/media/File:Area_parallellogram_as_determinant.svg))

> The parallelogram defined by the rows of the above matrix is the one with vertices at (0, 0), (a, b), (a + c, b + d), and (c, d), as shown in the accompanying diagram. -Wikipedia

And:

**The absolute value of ad − bc is the area of the parallelogram, and thus represents the scale factor by which areas are transformed by A.** -Wikipedia

....This is the definition of the determinant (![\\Delta](http://chart.apis.google.com/chart?cht=tx&chl=%5CDelta "\Delta")) of a ![2 \\times 2](http://chart.apis.google.com/chart?cht=tx&chl=2%20%5Ctimes%202 "2 \times 2") matrix:

![](img/determinant.png)

### 3x3 matrices

The same idea can be extended into higher dimensions, for example, the absolute value of the determinant of a ![3 \\times 3](http://chart.apis.google.com/chart?cht=tx&chl=3%20%5Ctimes%203 "3 \times 3") matrix is the volume of the **parallelepiped** bound by coordinates related to values from the original matrix.

![](img/950px-Determinant_parallelepiped.svg.png)

(source: [Wikipedia](https://en.wikipedia.org/wiki/Determinant#/media/File:Determinant_parallelepiped.svg))

Here, the parallelepiped represents the transformed **unit cube**.

### Related geometric interpretation

Another useful way of thinking of the determinant geometrically:

> You can derive the algebraic properties from this geometrical interpretation. For example, if two of the columns are linearly dependent, your box is missing a dimension and so it's been flattened to have zero volume. \[2\]

### Determinants of correlation matrices

For example, suppose we are looking at *correlation matrices* for two variables.

In the first scenario, suppose the variables are highly correlated. In this case, the parallelogram corresponding to the matrix would be thin, and therefor, have a small area:

``` r
set.seed(1)

x <- 1:5
y <- x + rnorm(5)
mat <- cbind(x, y)

cor_mat1 <- cor(mat)
cor_mat1
```

    ##          x        y
    ## x 1.000000 0.934176
    ## y 0.934176 1.000000

``` r
# components of mat
a1 <- cor_mat1[1,1]
b1 <- cor_mat1[2,1]
c1 <- cor_mat1[1,2]
d1 <- cor_mat1[2,2]

plot(c(0, 2), c(0, 2), type = "n")
polygon(c(0, a1, a1 + c1, c1), c(0, b1, b1 + d1, d1), col='#369bed')
```

<img src="img/cor_matrix_determinant_a-1.png" width="1080" />

``` r
det(cor_mat1)
```

    ## [1] 0.1273151

``` r
eigen(cor_mat1)
```

    ## $values
    ## [1] 1.93417604 0.06582396
    ## 
    ## $vectors
    ##           [,1]       [,2]
    ## [1,] 0.7071068 -0.7071068
    ## [2,] 0.7071068  0.7071068

Next, suppose we have to completely uncorrelated variables; here, the parallelogram would be much closer to the unit square and its area would close to 1:

``` r
x <- rnorm(100)
y <- rnorm(100)
mat <- cbind(x, y)

cor_mat2 <- cor(mat)
cor_mat2
```

    ##             x           y
    ## x  1.00000000 -0.02049706
    ## y -0.02049706  1.00000000

``` r
# components of mat
a2 <- cor_mat2[1,1]
b2 <- cor_mat2[2,1]
c2 <- cor_mat2[1,2]
d2 <- cor_mat2[2,2]

plot(c(0, 2), c(0, 2), type = "n")
polygon(c(0, a2, a2 + c2, c2), c(0, b2, b2 + d2, d2), col='#369bed')
```

<img src="img/cor_matrix_determinant_b-1.png" width="1080" />

``` r
det(cor_mat2)
```

    ## [1] 0.9995799

``` r
eigen(cor_mat2)
```

    ## $values
    ## [1] 1.0204971 0.9795029
    ## 
    ## $vectors
    ##            [,1]       [,2]
    ## [1,] -0.7071068 -0.7071068
    ## [2,]  0.7071068 -0.7071068

<span style="color:red;">**QUESTION**:</span> *Why are the values of the eigenvectors so similar for the two examples?..*

The same basic trends hold true when applied to covariance matrices as well (correlated variables lead to closer values in the covariance matrix), however the exact values of the coordinates and the determinant change.

Other useful theorems we missed in chapter 3...
-----------------------------------------------

-   **Theorem 2** If ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is a triangular matrix, then det ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is the product of the entries on the main diagonal of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A").
    -   This is easy to see for ![2 \\times 2](http://chart.apis.google.com/chart?cht=tx&chl=2%20%5Ctimes%202 "2 \times 2") example: second product includes something below the diagonal so it goes to zero, leaving only the product coming from the diagonal.
-   **Theorem 3**: Determinant for one square matrix can be determined by following simple rules relating to row operations used to get from that matrix to a new one (see p192 for details).
-   Relation to invertibility of a matrix:
    1.  When ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is invertible: det ![A = (-1)^r \\times (\\text{product of pivots in } U)](http://chart.apis.google.com/chart?cht=tx&chl=A%20%3D%20%28-1%29%5Er%20%5Ctimes%20%28%5Ctext%7Bproduct%20of%20pivots%20in%20%7D%20U%29 "A = (-1)^r \times (\text{product of pivots in } U)")
    2.  When ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is *not* invertible, det ![A = 0](http://chart.apis.google.com/chart?cht=tx&chl=A%20%3D%200 "A = 0")
-   **Theorem 4** A square matrix ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is invertible if and only if det ![A \\neq 0](http://chart.apis.google.com/chart?cht=tx&chl=A%20%5Cneq%200 "A \neq 0")
    -   The columns of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") are linearly dependent ![\\Rightarrow det A = 0](http://chart.apis.google.com/chart?cht=tx&chl=%5CRightarrow%20det%20A%20%3D%200 "\Rightarrow det A = 0")
        -   ...remember the geometric interpretation of this idea above.
    -   The rows of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") are linearly dependent ![\\implies det A = 0](http://chart.apis.google.com/chart?cht=tx&chl=%5Cimplies%20det%20A%20%3D%200 "\implies det A = 0")
        -   Rows of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") = columns of ![A^T](http://chart.apis.google.com/chart?cht=tx&chl=A%5ET "A^T").
        -   When ![A^T](http://chart.apis.google.com/chart?cht=tx&chl=A%5ET "A^T") is singular, so is ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A").
-   **Theorem 5** If ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is an ![n \\times n](http://chart.apis.google.com/chart?cht=tx&chl=n%20%5Ctimes%20n "n \times n") matrix, then ![\\text{det} A^T = \\text{det} A](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctext%7Bdet%7D%20A%5ET%20%3D%20%5Ctext%7Bdet%7D%20A "\text{det} A^T = \text{det} A").
-   **Theorem 6** If ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") and ![B](http://chart.apis.google.com/chart?cht=tx&chl=B "B") are ![n \\times n](http://chart.apis.google.com/chart?cht=tx&chl=n%20%5Ctimes%20n "n \times n") matrices, then det ![A B](http://chart.apis.google.com/chart?cht=tx&chl=A%20B "A B") = (det ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"))(det ![B](http://chart.apis.google.com/chart?cht=tx&chl=B "B")).
-   Note: this is *not* true for sums of determinants!

Skipping 3.3 on Cramer's Rule, etc. (too much typing and not really needed below..)

The Characteristic Equation
===========================

Overview
--------

**Main idea:**

Information about the <i>eigenvalues</i> of a square matrix are encoded in a special equation called the <b>characteristic equation</b> of the matrix.

For a given square matrix, ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"), recall that eigenvalues for the matrix are defined as:

*A**x* = *λ**x*

We can then rearrange this to:

(*A* − *λ**I*)*x* = 0

to find the eigenvalues associated with a given matrix. All values for ![\\lambda](http://chart.apis.google.com/chart?cht=tx&chl=%5Clambda "\lambda") that lead to a nontrival solution for the above equation are the eigenvalues for the matrix.

Next, recall that for a matrix to be invertible, equation ![Ax = 0](http://chart.apis.google.com/chart?cht=tx&chl=Ax%20%3D%200 "Ax = 0") must have *only* the trivial solution (IVT).

Therefore, another way to think about the above problem is to look for all ![\\lambda](http://chart.apis.google.com/chart?cht=tx&chl=%5Clambda "\lambda") such that ![A - \\lambda I](http://chart.apis.google.com/chart?cht=tx&chl=A%20-%20%5Clambda%20I "A - \lambda I") is *not* invertible.

From Lay 3.2, theorem 4 states:

> A square matrix A is invertible if and only if det A != 0

Which leads us to the following way of determining the eigenvalues for ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"):

*d**e**t*(*A* − *λ**I*)=0

This is called the **The Characteristic Equation** of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"). Any scalar ![\\lambda](http://chart.apis.google.com/chart?cht=tx&chl=%5Clambda "\lambda") is an eigenvalue of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") if and only if it satisfies the above equation.

When we have a triangular matrix, we can just take the product each of the diagonal values - ![\\lambda](http://chart.apis.google.com/chart?cht=tx&chl=%5Clambda "\lambda"), and set it equal to zero.

After expansion, this leaves us with a simple polynomial equation in a single variable!

Characteristic polynomials
--------------------------

-   If ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is an ![n \\times n](http://chart.apis.google.com/chart?cht=tx&chl=n%20%5Ctimes%20n "n \times n") matrix, then det ( ![A - \\lambda I](http://chart.apis.google.com/chart?cht=tx&chl=A%20-%20%5Clambda%20I "A - \lambda I") )is a polynomial of degree ![n](http://chart.apis.google.com/chart?cht=tx&chl=n "n") called the <b>characteristic polynomial</b> of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A").
-   To find the eigenvalues for ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"), we simply find the roots of its characteristic polynomial equation!

Similarity
----------

Another key idea from 5.2 which leads us into the chapter on matrix diagonalization is *similarity*.

-   If ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") and ![B](http://chart.apis.google.com/chart?cht=tx&chl=B "B") are ![n \\times n](http://chart.apis.google.com/chart?cht=tx&chl=n%20%5Ctimes%20n "n \times n") matrices, then ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") *is similar to* ![B](http://chart.apis.google.com/chart?cht=tx&chl=B "B") if there is an invertible matrix ![P](http://chart.apis.google.com/chart?cht=tx&chl=P "P") such that ![A = PBP^-1](http://chart.apis.google.com/chart?cht=tx&chl=A%20%3D%20PBP%5E-1 "A = PBP^-1").
-   ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") *is similar to* ![B](http://chart.apis.google.com/chart?cht=tx&chl=B "B") implies ![B](http://chart.apis.google.com/chart?cht=tx&chl=B "B") *is similar to* ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A")
-   Changing ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") into ![PBP^-1](http://chart.apis.google.com/chart?cht=tx&chl=PBP%5E-1 "PBP^-1") is called a **similarity transformation**

If ![n \\times n](http://chart.apis.google.com/chart?cht=tx&chl=n%20%5Ctimes%20n "n \times n") matrices ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") and ![B](http://chart.apis.google.com/chart?cht=tx&chl=B "B") are similar, then they have the same characteristic polynomial and hence the same eigenvalues (with the same multiplicities).

-note: *similarity* ![\\neq](http://chart.apis.google.com/chart?cht=tx&chl=%5Cneq "\neq") *row equivalence*.

Diagonalization
===============

Overview
--------

**Main idea:**

The eigenvalue-eigenvector information contained within a matrix ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") can be displayed in a usefu factorization of the form ![A = PDP^-1](http://chart.apis.google.com/chart?cht=tx&chl=A%20%3D%20PDP%5E-1 "A = PDP^-1"), where:

-   P -&gt; eigenvectors
-   D -&gt; eigenvalues

-   ![D](http://chart.apis.google.com/chart?cht=tx&chl=D "D") stands for *diagonal*
-   Useful for computing ![A^k](http://chart.apis.google.com/chart?cht=tx&chl=A%5Ek "A^k") for large values of ![k](http://chart.apis.google.com/chart?cht=tx&chl=k "k")
-   Aka "Eigendecomposition" or "spectral decomposition"
-   [SVD](https://en.wikipedia.org/wiki/Singular_value_decomposition) extends this idea to rectangular matrices.

The Diagonalization Theorem
---------------------------

-   A square matrix ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is said to be **diagonalizable** if ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is similar to a diagonal matrix, i.e. if ![A = PDP^-1](http://chart.apis.google.com/chart?cht=tx&chl=A%20%3D%20PDP%5E-1 "A = PDP^-1") for some invertible matrix ![P](http://chart.apis.google.com/chart?cht=tx&chl=P "P") and some diagonal matrix ![D](http://chart.apis.google.com/chart?cht=tx&chl=D "D").

**Theorem 5**

> An ![n \\times n](http://chart.apis.google.com/chart?cht=tx&chl=n%20%5Ctimes%20n "n \times n") matrix ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is diagonalizable if and only if ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") has ![n](http://chart.apis.google.com/chart?cht=tx&chl=n "n") linearly indepdendent eigenvectors. In fact, ![A = PDP^-1](http://chart.apis.google.com/chart?cht=tx&chl=A%20%3D%20PDP%5E-1 "A = PDP^-1"), with ![D](http://chart.apis.google.com/chart?cht=tx&chl=D "D") a diagonal matrix, if and only if the columns of ![P](http://chart.apis.google.com/chart?cht=tx&chl=P "P") are ![n](http://chart.apis.google.com/chart?cht=tx&chl=n "n") linearly independent eigenvectors of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"). In this case, the diagonal entries of ![D](http://chart.apis.google.com/chart?cht=tx&chl=D "D") are eigenvalues of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") that correspond, respectively, to the eigenvectors in ![P](http://chart.apis.google.com/chart?cht=tx&chl=P "P"). (Lay 5.3)

In other words...

-**![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is diagonalizable if and only if there are enough eigenvectors to form a basis of ![ℝ^n](http://chart.apis.google.com/chart?cht=tx&chl=%E2%84%9D%5En "ℝ^n"). - We call such a basis an **eigenvector basis\*\*.

Tangent: spectral analysis of covariance matrices
=================================================

To get a better feel for what the eigenvalues and eigenvectors of covariance matrices look like, let's look at a couple examples using fake data.

Matrices with correlated features
---------------------------------

### 3 variables (2 correlated)

First, we will create a vector with three columns, one of which is a multiple of another.

``` r
set.seed(1)

dat <- matrix(rnorm(40), ncol=2)
dat <- cbind(1.0 * dat[,1], dat)

# visualization relationship between the columns
cor(dat)
```

    ##            [,1]       [,2]       [,3]
    ## [1,]  1.0000000  1.0000000 -0.2175249
    ## [2,]  1.0000000  1.0000000 -0.2175249
    ## [3,] -0.2175249 -0.2175249  1.0000000

``` r
pairs(dat, upper.panel=NULL)
```

<img src="img/eigenvector_example-1.png" width="1080" />

Next, we will take compute the *square* covariance matrix corresponding to our original *rectangular* data matrix.

Because of the linear dependence in the columns of `dat`, there are only two non-zero eigenvalues.

``` r
# get the (square) covariance matrix for our data
covmat <- cov(dat)

# compute the eigenvectors / eigenvalues of the covariance matrix
eigen(covmat, symmetric=TRUE)
```

    ## $values
    ## [1]  1.729812e+00  6.975298e-01 -2.220446e-16
    ## 
    ## $vectors
    ##            [,1]      [,2]          [,3]
    ## [1,] -0.6856324 0.1729401  7.071068e-01
    ## [2,] -0.6856324 0.1729401 -7.071068e-01
    ## [3,]  0.2445742 0.9696306  6.383782e-16

In the output, the `$vectors` components is a ![p \\times p](http://chart.apis.google.com/chart?cht=tx&chl=p%20%5Ctimes%20p "p \times p") matrix whose *columns* contain the eigen vectors of the input matrix, normalized to unit length (see `?eigen`).

Notice that the first two *rows* in the result matrix are the same, but pointing in opposite directions. What do the rows mean in this context?..

### 4 variables (3 correlated)

What happens if we add another column that is a multiple of the first one?

``` r
dat2 <- cbind(2 * dat[,1], dat)
cor(dat2)
```

    ##            [,1]       [,2]       [,3]       [,4]
    ## [1,]  1.0000000  1.0000000  1.0000000 -0.2175249
    ## [2,]  1.0000000  1.0000000  1.0000000 -0.2175249
    ## [3,]  1.0000000  1.0000000  1.0000000 -0.2175249
    ## [4,] -0.2175249 -0.2175249 -0.2175249  1.0000000

``` r
eigen(cov(dat2), symmetric=TRUE)
```

    ## $values
    ## [1]  5.046133e+00  7.173388e-01  5.642840e-16 -2.493860e-16
    ## 
    ## $vectors
    ##             [,1]        [,2]          [,3]          [,4]
    ## [1,]  0.81253173 -0.08036699  4.807996e-01  3.196327e-01
    ## [2,]  0.40626587 -0.04018350 -8.722681e-01  2.692241e-01
    ## [3,]  0.40626587 -0.04018350 -8.933102e-02 -9.084896e-01
    ## [4,] -0.09842906 -0.99514407 -1.942890e-16 -2.463307e-16

p.s. Nice quote from Lay in the opening of chapter 3:

> In Cauchy's day, when life was simple and matrices were small...

References
==========

1.  *Lay* chapter 5.2 - 5.3
2.  <https://en.wikipedia.org/wiki/Determinant>
3.  <http://math.stackexchange.com/questions/668/whats-an-intuitive-way-to-think-about-the-determinant>
