-   [Determinants](#determinants)
    -   [Some geometric motivation](#some-geometric-motivation)
    -   [Other useful theorems we missed in chapter 3...](#other-useful-theorems-we-missed-in-chapter-3...)
-   [The Characteristic Equation](#the-characteristic-equation)
-   [Another tangent: spectral analysis of covariance matrices](#another-tangent-spectral-analysis-of-covariance-matrices)
    -   [3 variables (2 correlated)](#variables-2-correlated)
    -   [4 variables (3 correlated)](#variables-3-correlated)
-   [References](#references)

<h1>
Linear Algebra Review XI
</h1>
-   Keith Hughitt
-   Sept 02, 2016

Determinants
============

### Some geometric motivation

#### 2x2 matrices

A ![2 \\times 2](http://chart.apis.google.com/chart?cht=tx&chl=2%20%5Ctimes%202 "2 \times 2") matrix, ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"), can be viewed as a **linear map** which transforms the **standard basis vectors** (unit vectors pointing in the direction of the coordinate exes, in this case ![e\_x = (1,0)](http://chart.apis.google.com/chart?cht=tx&chl=e_x%20%3D%20%281%2C0%29 "e_x = (1,0)") and ![e\_y = (0, 1)](http://chart.apis.google.com/chart?cht=tx&chl=e_y%20%3D%20%280%2C%201%29 "e_y = (0, 1)")) to the rows (or columns) of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A").

The image of the basis vectors form a parallelogram representing the transformation applied to the unit square:

![](img/800px-Area_parallellogram_as_determinant.svg.png)

(source: [Wikipedia](https://en.wikipedia.org/wiki/Determinant#/media/File:Area_parallellogram_as_determinant.svg))

> The parallelogram defined by the rows of the above matrix is the one with vertices at (0, 0), (a, b), (a + c, b + d), and (c, d), as shown in the accompanying diagram. -Wikipedia

And:

**The absolute value of ad − bc is the area of the parallelogram, and thus represents the scale factor by which areas are transformed by A.** -Wikipedia

....This is the definition of the determinant (![\\Delta](http://chart.apis.google.com/chart?cht=tx&chl=%5CDelta "\Delta")) of a ![2 \\times 2](http://chart.apis.google.com/chart?cht=tx&chl=2%20%5Ctimes%202 "2 \times 2") matrix:

![](img/determinant.png)

#### 3x3 matrices

The same idea can be extended into higher dimensions, for example, the absolute value of the determinant of a ![3 \\times 3](http://chart.apis.google.com/chart?cht=tx&chl=3%20%5Ctimes%203 "3 \times 3") matrix is the volume of the **parallelepiped** bound by coordinates related to values from the original matrix.

![](img/950px-Determinant_parallelepiped.svg.png)

(source: [Wikipedia](https://en.wikipedia.org/wiki/Determinant#/media/File:Determinant_parallelepiped.svg))

Here, the parallelepiped represents the transformed **unit cube**.

#### Related geometric interpretation

Another useful way of thinking of the determinant geometrically:

> You can derive the algebraic properties from this geometrical interpretation. For example, if two of the columns are linearly dependent, your box is missing a dimension and so it's been flattened to have zero volume. \[2\]

#### Determinants of correlation matrices

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

<img src="img/cor_mat2rix_determinant_a-1.png" width="1080" />

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

<span style="color:red; font-weight: 700;">QUESTION:</span> *Why are the values of the eigenvectors so similar for the two examples?..*

The same basic trends hold true when applied to covariance matrices as well (correlated variables lead to closer values in the covariance matrix), however the exact values of the coordinates and the determinant change.

### Other useful theorems we missed in chapter 3...

-   **Theorem 2** If ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is a triangular matrix, then det ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is the product of the entries on the main diagonal of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A").
    -   This is easy to see for ![2 \\times 2](http://chart.apis.google.com/chart?cht=tx&chl=2%20%5Ctimes%202 "2 \times 2") example: second product includes something below the diagonal so it goes to zero, leaving only the product coming from the diagonal.
-   **Theorem 3**: Determinant for one square matrix can be determined by following simple rules relating to row operations used to get from that matrix to a new one (see p192 for details).
-   Relation to invertibility of a matrix:
    1.  When ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is invertible: det ![A = (-1)^r \\times (\\text{product of pivots in} U)](http://chart.apis.google.com/chart?cht=tx&chl=A%20%3D%20%28-1%29%5Er%20%5Ctimes%20%28%5Ctext%7Bproduct%20of%20pivots%20in%7D%20U%29 "A = (-1)^r \times (\text{product of pivots in} U)")
    2.  When ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is *not* invertible, det ![A = 0](http://chart.apis.google.com/chart?cht=tx&chl=A%20%3D%200 "A = 0")
-   **Theorem 4** A square matrix ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is invertible iff det ![A \\neq 0](http://chart.apis.google.com/chart?cht=tx&chl=A%20%5Cneq%200 "A \neq 0")
    -   The columns of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") are linearly dependent ![\\implies det A = 0](http://chart.apis.google.com/chart?cht=tx&chl=%5Cimplies%20det%20A%20%3D%200 "\implies det A = 0")
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

> A square matrix A is invertible iff det A != 0

Which leads us to the following way of determining the eigenvalues for ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"):

*d**e**t*(*A* − *λ**I*)=0

This is called the **The Characteristic Equation** of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"). Any scalar ![\\lambda](http://chart.apis.google.com/chart?cht=tx&chl=%5Clambda "\lambda") is an eigenvalue of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") if and only if it satisfies the above equation.

When we have a triangular matrix, we can just take the product each of the diagonal values - ![\\lambda](http://chart.apis.google.com/chart?cht=tx&chl=%5Clambda "\lambda"), and set it equal to zero.

After expansion, this leaves us with a simple polynomial equation in a single variable!

-   If ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is an ![n \\times n](http://chart.apis.google.com/chart?cht=tx&chl=n%20%5Ctimes%20n "n \times n") matrix, then det ( ![A - \\lambda I](http://chart.apis.google.com/chart?cht=tx&chl=A%20-%20%5Clambda%20I "A - \lambda I") )is a polynomial of degree ![n](http://chart.apis.google.com/chart?cht=tx&chl=n "n") called the <b>characteristic polynomial</b> of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A").
-   To find the eigenvalues for ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"), we simply find the roots of its characteristic polynomial equation!

Another tangent: spectral analysis of covariance matrices
=========================================================

To get a better feel for what the eigenvalues and eigenvectors of covariance matrices look like, let's look at a couple examples using fake data.

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

1.  <https://en.wikipedia.org/wiki/Determinant>

2.  <http://math.stackexchange.com/questions/668/whats-an-intuitive-way-to-think-about-the-determinant>
