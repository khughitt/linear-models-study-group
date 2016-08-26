-   [Determinants](#determinants)
    -   [Some geometric motivation](#some-geometric-motivation)
    -   [Other useful theorems we missed in chapter 3...](#other-useful-theorems-we-missed-in-chapter-3...)
-   [The Characteristic Equation](#the-characteristic-equation)
-   [Spectral analysis of covariance matrices](#spectral-analysis-of-covariance-matrices)
-   [References](#references)

<h1>
Linear Algebra Review XI
</h1>
-   Keith Hughitt
-   Sept 02, 2016

Determinants
============

### Some geometric motivation

A 2 × 2 matrix, *A*, can be viewed as a **linear map** which transforms the **standard basis vectors** (unit vectors pointing in the direction of the coordinate exes, in this case *e*<sub>*x*</sub> = (1, 0) and *e*<sub>*y*</sub> = (0, 1)) to the rows (or columns) of *A*.

The image of the basis vectors form a parallelogram representing the transformation applied to the unit square:

![](img/800px-Area_parallellogram_as_determinant.svg.png)

(source: [Wikipedia](https://en.wikipedia.org/wiki/Determinant#/media/File:Area_parallellogram_as_determinant.svg))

> The parallelogram defined by the rows of the above matrix is the one with vertices at (0, 0), (a, b), (a + c, b + d), and (c, d), as shown in the accompanying diagram. -Wikipedia

And:

**The absolute value of ad − bc is the area of the parallelogram, and thus represents the scale factor by which areas are transformed by A.** -Wikipedia

....This is the definition of the determinant (*Δ*) of a 2 × 2 matrix:

![](img/determinant.png)

The same idea can be extended into higher dimensions, for example, the absolute value of the determinant of a 3 × 3 matrix is the volume of the **parallelepiped** bound by coordinates related to values from the original matrix.

Here, the parallelepiped represents the transformed **unit cube**.

Another useful way of thinking of the determinant geometrically:

> You can derive the algebraic properties from this geometrical interpretation. For example, if two of the columns are linearly dependent, your box is missing a dimension and so it's been flattened to have zero volume. \[2\]

### Other useful theorems we missed in chapter 3...

-   **Theorem 2** If *A* is a triangular matrix, then det *A* is the product of the entries on the main diagonal of *A*.
    -   This is easy to see for 2 × 2 example: second product includes something below the diagonal so it goes to zero, leaving only the product coming from the diagonal.
-   **Theorem 3**: Determinant for one square matrix can be determined by following simple rules relating to row operations used to get from that matrix to a new one (see p192 for details).
-   Relation to invertibility of a matrix:
    1.  When *A* is invertible: det *A* = ( − 1)<sup>*r*</sup> × (product of pivots in*U*)
    2.  When *A* is *not* invertible, det *A* = 0
-   **Theorem 4** A square matrix *A* is invertible iff det *A* ≠ 0
    -   The columns of *A* are linearly dependent ⟹*d**e**t**A* = 0
        -   ...remember the geometric interpretation of this idea above.
    -   The rows of *A* are linearly dependent ⟹*d**e**t**A* = 0
        -   Rows of *A* = columns of *A*<sup>*T*</sup>.
        -   When *A*<sup>*T*</sup> is singular, so is *A*.
-   **Theorem 5** If *A* is an *n* × *n* matrix, then det*A*<sup>*T*</sup> = det*A*.
-   **Theorem 6** If *A* and *B* are *n* × *n* matrices, then det *A**B* = (det *A*)(det *B*).
-   Note: this is *not* true for sums of determinants!

Skipping 3.3 on Cramer's Rule, etc. (too much typing and not really needed below..)

The Characteristic Equation
===========================

For a given square matrix, *A*, recall that eigenvalues for the matrix are defined as:

$$
Ax = \\lamba x
$$

We can then rearrange this to:

$$
(A - \\lamba I)x = 0
$$

to find the eigenvalues associated with a given matrix. All values for *λ* that lead to a nontrival solution for the above equation are the eigenvalues for the matrix.

Next, recall that for a matrix to be invertible, equation *A**x* = 0 must have *only* the trivial solution (IVT).

Therefore, another way to think about the above problem is to look for all *λ* such that $A - \\lambdaI$ is *not* invertible.

From Lay 3.2, theorem 4 states:

> A square matrix A is invertible iff det A != 0

Which leads us to the following way of determining the eigenvalues for *A*:

*d**e**t*(*A* − *λ**I*)=0

Spectral analysis of covariance matrices
========================================

First, we will create a vector with three columns, one of which is a multiple of another.

``` r
set.seed(1)

dat <- matrix(rnorm(40), ncol=2)
dat <- cbind(1.0 * dat[,1], dat)

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

In the output, the `$vectors` components is a *p* × *p* matrix whose *columns* contain the eigen vectors of the input matrix, normalized to unit length (see `?eigen`).

Notice that the first two *rows* in the result matrix are the same, but pointing in opposite directions. What do the rows mean in this context?..

What happens if we add another column that is a multiple of the first one?

``` r
dat2 <- cbind(2 * dat[,1], dat)
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
