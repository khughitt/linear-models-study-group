Linear Algebra Review I
=======================

- Keith Hughitt
- June 22, 2016

## Linear equations

### Overview

> A **linear equation** in the variables x1,...,xn is an equation that can be
> written in the form:

![linear equation](img/linear_eqn.png)

> where b and the **coefficients** a1,...,1n are real or complex numbers,
> usually known in advance.

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

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/7c13e5e90c7908cacad9eaf243508935906621fe)

or

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/9f49e4113c4334c1b196d30f59e52ebf690aea71)

2. Slope-intercept form

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/753facd3de6ab64fa1cefd9a176437ed977e2979)

3. Point-slope form

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/6b2be8b9932f9656b8f3dca57cb4832653d10331)

where (x1, y1) is any point on the line.

4. Parametric form

Simultaneous equations:

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/d19f316585d11d422d808b377b17d7f627570e2e)

and

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/3c2b75dc06a35310bf2a8512b0d120a1d53765af)

(See [Wikipedia](https://en.wikipedia.org/wiki/Linear_equation#Forms_for_two-dimensional_linear_equations)
for a more exhaustive list of the ways lines can be represented.)

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

> A model is linear when each term is either a constant or the product of a
> parameter and a predictor variable. A linear equation is constructed by
> adding the results for each term. (Minitab blog [4])

- This allows for the introduction of curviture into the regression fit.
- Thus, a _linear_ model can be used to fit a _nonlinear_ relationship.

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

## Systems of Linear equations

### Some definitions

- **system of linear equations** (aka **linear system**): collection of one or
  more linear equations using the same variables.
- **solution**: List of numbers that makes each equation evaluate to a true
  statement when substituted for the variables in a linear system.
- **solution set**: The set of all possible solutions for a linear system.
- **equivalence**: Two linear systems are said to be equivalent if they share
  the same solution set.

### Geometric interpretation

For two variables, the solution set represents the intersection (if it occurs)
of two lines:

![](https://en.wikipedia.org/wiki/Linear_equation#/media/File:Linear_Function_Graph.svg)
(source: [Wikipedia](https://en.wikipedia.org/wiki/Linear_equation#/media/File:Linear_Function_Graph.svg))

## Matrix notation

## References

1. [Linear Algebra and its applications (Lay 3e)](http://www.laylinalgebra.com/)
2. [Linear Equation - Wikipedia](https://en.wikipedia.org/wiki/Linear_equation)
3. [Linear Regression - Wikipedia](https://en.wikipedia.org/wiki/Linear_regression)
4. [What Is the Difference between Linear and Nonlinear Equations in Regression Analysis?](http://blog.minitab.com/blog/adventures-in-statistics/what-is-the-difference-between-linear-and-nonlinear-equations-in-regression-analysis)
