-   [Overview](#overview)
-   [Week 3: Generalizations](#week-3-generalizations)
    -   [Linear regression for a function space](#linear-regression-for-a-function-space)
-   [Week 4: Projections](#week-4-projections)
    -   [Projection matrix](#projection-matrix)
    -   [Residuals](#residuals)
-   [References](#references)

<h1>
Advanced Linear Models III
</h1>
-   Keith Hughitt
-   April 18, 2017

Overview
========

Covering a couple of left-over sections from weeks 3-4:

-   Week 3 Generalizations (textbook section 4.4: *Extension to other spaces*)
-   Week 4 Projections (textbook section 5.4: *Projections*)

Week 3: Generalizations
=======================

So far, we have been considering linear regression in Euclidean space (![ℝ^n](https://latex.codecogs.com/png.latex?%E2%84%9D%5En "ℝ^n")). It turns out, however, that many of the same approaches readily apply to other more general vector spaces.

One such example is a [Hilbert Space](https://en.wikipedia.org/wiki/Hilbert_space).

-   A Hilbert Space is a vector space generalization of the Euclidean space which has an associted *inner product* that allows lengths and angles to be measured.
-   Used in functional analysis, quantum mechanics, Fourier analysis, etc.

Linear regression for a function space
--------------------------------------

The course gives an example of extending linear regression to a space of square integrable functions.

-   Let *y* be in the space of functions from ![\[0,1\] \\rightarrow ℝ](https://latex.codecogs.com/png.latex?%5B0%2C1%5D%20%5Crightarrow%20%E2%84%9D "[0,1] \rightarrow ℝ") with finite squared integral.
-   "In mathematics, a square-integrable function, also called a quadratically integrable function, is a real- or complex-valued measurable function for which the integral of the square of the absolute value is finite." (Wikipedia)
-   Define the inner product as:

![
\\langle f,g \\rangle = \\int\_0^1 f(t)g(t) \\mathrm{d}t
](https://latex.codecogs.com/png.latex?%0A%5Clangle%20f%2Cg%20%5Crangle%20%3D%20%5Cint_0%5E1%20f%28t%29g%28t%29%20%5Cmathrm%7Bd%7Dt%0A "
\langle f,g \rangle = \int_0^1 f(t)g(t) \mathrm{d}t
")

-   In this case, we want to find the best approximation to y in x.
-   The solution for ![\\hat{\\beta}](https://latex.codecogs.com/png.latex?%5Chat%7B%5Cbeta%7D "\hat{\beta}") is the same as for linear regression with real numbers:

![
\\hat{\\beta} = \\frac{\\langle y,x \\rangle}{\\langle x,x \\rangle}
](https://latex.codecogs.com/png.latex?%0A%5Chat%7B%5Cbeta%7D%20%3D%20%5Cfrac%7B%5Clangle%20y%2Cx%20%5Crangle%7D%7B%5Clangle%20x%2Cx%20%5Crangle%7D%0A "
\hat{\beta} = \frac{\langle y,x \rangle}{\langle x,x \rangle}
")

-   Textbook/video demonstrate the above and also extend the example to include an intercept, and define functional variance and correlation.

-   Functional Example:

Suppose you have functions a quadratic function ![y(t)](https://latex.codecogs.com/png.latex?y%28t%29 "y(t)") that you want to approximate with a linear function:

![
y(t) = t + 2t^2
\\newline
x(t) = t
](https://latex.codecogs.com/png.latex?%0Ay%28t%29%20%3D%20t%20%2B%202t%5E2%0A%5Cnewline%0Ax%28t%29%20%3D%20t%0A "
y(t) = t + 2t^2
\newline
x(t) = t
")

Using the integral-based definition of the inner-product least-squares solution above (integral of y(t) over the integral of x(t)), you arrive at a slope for the best-fit line of 2.5.

``` r
t <- seq(0, 1, by=1/1000)
y <- t + 2*t^2
x <- t

lm(y ~ x - 1)
```

    ## 
    ## Call:
    ## lm(formula = y ~ x - 1)
    ## 
    ## Coefficients:
    ##     x  
    ## 2.501

\*Note: what's the "-1" in the model equation above for?

Week 4: Projections
===================

Projection matrix
-----------------

Thinking of least squares in terms of projections.

Suppose you have:

![
y in ℝ^3
\\newline
x = 3x2 matrix
](https://latex.codecogs.com/png.latex?%0Ay%20in%20%E2%84%9D%5E3%0A%5Cnewline%0Ax%20%3D%203x2%20matrix%0A "
y in ℝ^3
\newline
x = 3x2 matrix
")

Want to minimize:

![
|| y - x\\beta ||^2
](https://latex.codecogs.com/png.latex?%0A%7C%7C%20y%20-%20x%5Cbeta%20%7C%7C%5E2%0A "
|| y - x\beta ||^2
")

-   y is a vector in ![ℝ^3](https://latex.codecogs.com/png.latex?%E2%84%9D%5E3 "ℝ^3")
-   the solution space for ![\\beta](https://latex.codecogs.com/png.latex?%5Cbeta "\beta") (![\\gamma](https://latex.codecogs.com/png.latex?%5Cgamma "\gamma")) in the notes is a 2-dimensional subspace in ![ℝ^3](https://latex.codecogs.com/png.latex?%E2%84%9D%5E3 "ℝ^3")
-   The solution to the above (![\\hat{y}](https://latex.codecogs.com/png.latex?%5Chat%7By%7D "\hat{y}")) is the point in ![\\gamma](https://latex.codecogs.com/png.latex?%5Cgamma "\gamma") that is the minimum distance from ![y](https://latex.codecogs.com/png.latex?y "y")

An interesting result of this:

-   Adding a redundant column to ![x](https://latex.codecogs.com/png.latex?x "x") (example used: ![x\_1 + x\_2](https://latex.codecogs.com/png.latex?x_1%20%2B%20x_2 "x_1 + x_2")), doesn't change the solution space:
    -   Even with this new column, the rank of the matrix is the same, and,
    -   the space spanned (all possible linear columns of ![x\_1 \\text{and} x\_2](https://latex.codecogs.com/png.latex?x_1%20%5Ctext%7Band%7D%20x_2 "x_1 \text{and} x_2")) and the solution ![\\hat{y}](https://latex.codecogs.com/png.latex?%5Chat%7By%7D "\hat{y}") are the same.
-   This also means that we don't need an invertible matrix to find a solution
-   We just need the space defined by the linearly indepedent *subset* of the columns of ![X](https://latex.codecogs.com/png.latex?X "X").
-   Also, different design matrices (video uses examples of matrices with all 1's and 0's organized in different ways, ~5:45) also span the same ![\\gamma](https://latex.codecogs.com/png.latex?%5Cgamma "\gamma").

Next, recall:

![
\\hat{\\beta} = (x^Tx)^{-1}x^Ty
](https://latex.codecogs.com/png.latex?%0A%5Chat%7B%5Cbeta%7D%20%3D%20%28x%5ETx%29%5E%7B-1%7Dx%5ETy%0A "
\hat{\beta} = (x^Tx)^{-1}x^Ty
")

That is the projection of ![y](https://latex.codecogs.com/png.latex?y "y") on to the space defined by the linear combinations of the columns of ![x](https://latex.codecogs.com/png.latex?x "x").

The solution, ![\\hat{\\beta}](https://latex.codecogs.com/png.latex?%5Chat%7B%5Cbeta%7D "\hat{\beta}") is the particular vector in ![ℝ^2](https://latex.codecogs.com/png.latex?%E2%84%9D%5E2 "ℝ^2") that converts projects ![x](https://latex.codecogs.com/png.latex?x "x") onto ![\\gamma](https://latex.codecogs.com/png.latex?%5Cgamma "\gamma").

So the *projection* is:

![
\\hat{\\beta} = H\_xy = x(x^Tx)^{-1}x^Ty
](https://latex.codecogs.com/png.latex?%0A%5Chat%7B%5Cbeta%7D%20%3D%20H_xy%20%3D%20x%28x%5ETx%29%5E%7B-1%7Dx%5ETy%0A "
\hat{\beta} = H_xy = x(x^Tx)^{-1}x^Ty
")

The matrix ![H\_x](https://latex.codecogs.com/png.latex?H_x "H_x") (the "projection matrix" or "hat matrix") is the linear operator that projects a vector in ![ℝ^n](https://latex.codecogs.com/png.latex?%E2%84%9D%5En "ℝ^n") onto the 2-dimensional space spanned by the columns of ![X](https://latex.codecogs.com/png.latex?X "X").

Residuals
---------

Residuals:

![
e = y - \\hat{y} = y - x(x^Tx)^{-1}x^Ty
\\newline
  = (I - H\_x)y
](https://latex.codecogs.com/png.latex?%0Ae%20%3D%20y%20-%20%5Chat%7By%7D%20%3D%20y%20-%20x%28x%5ETx%29%5E%7B-1%7Dx%5ETy%0A%5Cnewline%0A%20%20%3D%20%28I%20-%20H_x%29y%0A "
e = y - \hat{y} = y - x(x^Tx)^{-1}x^Ty
\newline
  = (I - H_x)y
")

-   ![e](https://latex.codecogs.com/png.latex?e "e") is orthogonal to any point in ![\\gamma](https://latex.codecogs.com/png.latex?%5Cgamma "\gamma")
-   ![e](https://latex.codecogs.com/png.latex?e "e") is orthogonal to any column of ![X](https://latex.codecogs.com/png.latex?X "X")
-   The sum of the residuals equals 0.

References
==========

1.  Advanced Linear Models by Brian Caffo (Coursera)
2.  <https://en.wikipedia.org/wiki/Hilbert_space>
3.  <https://en.wikipedia.org/wiki/Square-integrable_function>
