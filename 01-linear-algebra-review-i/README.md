Linear Algebra Review
---------------------

## Linear equations

### Overview

Most of what we will encounter during our review of linear algebra will be
simple linear equations:

> A linear equation is an algebraic equation in which each term is either a
> constant or the product of a constant and (the first power of) a single
> variable. -Wikipedia

So things like a line in two-dimensional space:

![a line](img/line.png)

or a plane in three-dimensional space:

![a plane](img/plane.png)

In higher dimensions, this generalizes to a n-1 dimensional hyperplane in
n-dimensional space.

### Equations for a line

Two-dimensional linear equations are commonly represented in different forms:

1. General form

$Ax + By = C$

or

$Ax + By - c = 0$

2. Slope-intercept form

$y = mx + b$

3. Point-slope form

$y - y1 = m(x - x1)$

where (x1, y1) is any point on the line.


### Linear in the parameters

While our review of linear algebra will primarily focus on the simple types of
linear equations described above. For these equations, each term in the
equation consists of a constant multiplied by a variable.

In other contexts such as linear regression, the variable part of each term may
be transformed, even in a nonlinear way, e.g.:

<!-- 
y = \beta_0 + \beta_1 X_1 + \beta_2 X_2^2 + \beta_3 X_1 X_2
-->
![linear in the parameters](img/linear_in_the_parameters_example.png)

A example of this is [polynomial regression](https://en.wikipedia.org/wiki/Polynomial_regression):

> ...The mean of the response variable is a linear combination of the parameters 
> (regression coefficients) and the predictor variables. Note that this
> assumption is much less restrictive than it may at first seem. Because the
> predictor variables are treated as fixed values (see above), linearity is
> really only a restriction on the parameters. The predictor variables themselves
> can be arbitrarily transformed, and in fact multiple copies of the same
> underlying predictor variable can be added, each one transformed differently.
> This trick is used, for example, in polynomial regression, which uses linear 
> regression to fit the response variable as an arbitrary polynomial function 
> (up to a given rank) of a predictor variable.
> -Wikipedia

References
----------

1. [Linear Equation - Wikipedia](https://en.wikipedia.org/wiki/Linear_equation)
2. [Linear Regression - Wikipedia](https://en.wikipedia.org/wiki/Linear_regression)
3. [What Is the Difference between Linear and Nonlinear Equations in Regression Analysis?](http://blog.minitab.com/blog/adventures-in-statistics/what-is-the-difference-between-linear-and-nonlinear-equations-in-regression-analysis)
