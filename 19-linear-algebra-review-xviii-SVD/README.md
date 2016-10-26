-   [Steps to performing SVD](#steps-to-performing-svd)
-   [SVD in R](#svd-in-r)

<h1>
Linear Algebra Review XVIII SVD
</h1>
-   Nate Olson
-   October 25, 2016

**Singular value decomposition** - matrix factorization that can be applied to rectangular matricies.

**Singlular Value Decomposition**

*A* = *U**Σ**V*<sup>*T*</sup>

-   ![\\textbf{A}](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7BA%7D "\textbf{A}") is a ![m \\times n](http://chart.apis.google.com/chart?cht=tx&chl=m%20%5Ctimes%20n "m \times n") matrix with rank ![r](http://chart.apis.google.com/chart?cht=tx&chl=r "r")
-   **![\\Sigma](http://chart.apis.google.com/chart?cht=tx&chl=%5CSigma "\Sigma")** is a ![m \\times n](http://chart.apis.google.com/chart?cht=tx&chl=m%20%5Ctimes%20n "m \times n") matrix that includes a diagonal matrix of size ![r \\times r](http://chart.apis.google.com/chart?cht=tx&chl=r%20%5Ctimes%20r "r \times r"), where ![r](http://chart.apis.google.com/chart?cht=tx&chl=r "r") is the rank of the factorized matrix.
-   the diagonal values in the matrix are the singular values in decreasing order
-   ![\\textbf{U}](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7BU%7D "\textbf{U}")\_\_ - left singular values
-   ![\\textbf{V}](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7BV%7D "\textbf{V}") - right singular values

### Steps to performing SVD

1.  Find an orthogonal diagonalization of **![A^{T}A](http://chart.apis.google.com/chart?cht=tx&chl=A%5E%7BT%7DA "A^{T}A")** - eigenvalues of ![A^TA](http://chart.apis.google.com/chart?cht=tx&chl=A%5ETA "A^TA") and corresponding orthonormal eigenvectors.
2.  Set up **![V](http://chart.apis.google.com/chart?cht=tx&chl=V "V")** and **![\\Sigma](http://chart.apis.google.com/chart?cht=tx&chl=%5CSigma "\Sigma")** based on the ordered eigenvalues
3.  Construct **![U](http://chart.apis.google.com/chart?cht=tx&chl=U "U")** - composed of the normalized vectors from **![Av\_i](http://chart.apis.google.com/chart?cht=tx&chl=Av_i "Av_i")**

Good youtube video on SVD <https://youtu.be/P5mlg91as1c>

### SVD in R

Matrix from example 3 in book

``` r
(a <- matrix(c(4,11,14,8,7,-2),ncol=3, byrow = TRUE))
```

    ##      [,1] [,2] [,3]
    ## [1,]    4   11   14
    ## [2,]    8    7   -2

R has a command for calculating SVD <http://ugrad.stat.ubc.ca/R/library/base/html/svd.html>

``` r
svd(a,nv = 3)
```

    ## $d
    ## [1] 18.973666  9.486833
    ## 
    ## $u
    ##            [,1]       [,2]
    ## [1,] -0.9486833 -0.3162278
    ## [2,] -0.3162278  0.9486833
    ## 
    ## $v
    ##            [,1]       [,2]       [,3]
    ## [1,] -0.3333333  0.6666667 -0.6666667
    ## [2,] -0.6666667  0.3333333  0.6666667
    ## [3,] -0.6666667 -0.6666667 -0.3333333

#### Stepwise

1.  Find an orthogonal diagonalization of **![A^{T}A](http://chart.apis.google.com/chart?cht=tx&chl=A%5E%7BT%7DA "A^{T}A")** - eigenvalues of ![A^TA](http://chart.apis.google.com/chart?cht=tx&chl=A%5ETA "A^TA") and corresponding orthonormal eigenvectors.

``` r
(a_eigen <- eigen(t(a) %*% a))
```

    ## $values
    ## [1] 3.600000e+02 9.000000e+01 7.105427e-15
    ## 
    ## $vectors
    ##            [,1]       [,2]       [,3]
    ## [1,] -0.3333333  0.6666667  0.6666667
    ## [2,] -0.6666667  0.3333333 -0.6666667
    ## [3,] -0.6666667 -0.6666667  0.3333333

1.  Set up **![V](http://chart.apis.google.com/chart?cht=tx&chl=V "V")** and **![\\Sigma](http://chart.apis.google.com/chart?cht=tx&chl=%5CSigma "\Sigma")** based on the ordered eigenvalues

``` r
(sigma <- diag(sqrt(a_eigen$values)))
```

    ##          [,1]     [,2]        [,3]
    ## [1,] 18.97367 0.000000 0.00000e+00
    ## [2,]  0.00000 9.486833 0.00000e+00
    ## [3,]  0.00000 0.000000 8.42937e-08

``` r
(V <- a_eigen$vectors)
```

    ##            [,1]       [,2]       [,3]
    ## [1,] -0.3333333  0.6666667  0.6666667
    ## [2,] -0.6666667  0.3333333 -0.6666667
    ## [3,] -0.6666667 -0.6666667  0.3333333

1.  Construct **![U](http://chart.apis.google.com/chart?cht=tx&chl=U "U")** - composed of the normalized vectors from **![\\frac{1}{\\sigma\_i} Av\_i](http://chart.apis.google.com/chart?cht=tx&chl=%5Cfrac%7B1%7D%7B%5Csigma_i%7D%20Av_i "\frac{1}{\sigma_i} Av_i")**

``` r
e1 <- V[,1] %>% as.matrix()
e2 <- V[,2] %>% as.matrix()

u1 <- a %*% e1 * 1/sigma[1,1]
u2 <- a %*% e2 * 1/sigma[2,2]

(U <- cbind(u1,u2))
```

    ##            [,1]       [,2]
    ## [1,] -0.9486833 -0.3162278
    ## [2,] -0.3162278  0.9486833
