-   [Overview](#overview)
-   [Week 3: Generalizations](#week-3-generalizations)
    -   [Linear regression for a function space](#linear-regression-for-a-function-space)
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

So far, we have been considering linear regression in Euclidean space (ℝ^n). It turns out, however, that many of the same approaches readily apply to other more general vector spaces.

One such example is a [Hilbert Space](https://en.wikipedia.org/wiki/Hilbert_space).

-   A Hilbert Space is a vector space generalization of the Euclidean space which has an associted *inner product* that allows lengths and angles to be measured.
-   Used in functional analysis, quantum mechanics, Fourier analysis, etc.

Linear regression for a function space
--------------------------------------

The course gives an example of extending linear regression to a space of square integrable functions.

-   Let *y* be in the space of functions from \[0, 1\]→*ℝ* with finite squared integral.
-   "In mathematics, a square-integrable function, also called a quadratically integrable function, is a real- or complex-valued measurable function for which the integral of the square of the absolute value is finite." (Wikipedia)
-   Define the inner product as:

⟨*f*, *g*⟩=∫<sub>0</sub><sup>1</sup>*f*(*t*)*g*(*t*)*d**t*

-   In this case, we want to find the best approximation to y in x.
-   The solution for $\\hat{\\beta}$ is the same as for linear regression with real numbers:

$$
\\hat{\\beta} = \\over{\\langle y,x \\rangle}{\\langle x,x \\rangle}
$$

-   Textbook/video demonstrate the above and also extend the example to include an intercept, and define functional variance and correlation.

-   Functional Example:

Suppose you have functions a quadratic function *y*(*t*) that you want to approximate with a linear function:

*y*(*t*)=*t* + 2*t*<sup>2</sup>*x*(*t*)=*t*

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

References
==========

1.  Advanced Linear Models by Brian Caffo (Coursera)
2.  <https://en.wikipedia.org/wiki/Hilbert_space>
3.  <https://en.wikipedia.org/wiki/Square-integrable_function>
