Linear Algebra Review I
=======================

- Keith Hughitt
- June 22, 2016

## 1.1 Linear Equations in Linear Algebra

### Linear equations

#### Overview

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

#### Equations for a line

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

#### Linear in the parameters

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

### Systems of Linear equations

#### Some definitions

- **system of linear equations** (aka **linear system**): collection of one or
  more linear equations using the same variables.
- **solution**: List of numbers that makes each equation evaluate to a true
  statement when substituted for the variables in a linear system.
- **solution set**: The set of all possible solutions for a linear system.
- **equivalence**: Two linear systems are said to be equivalent if they share
  the same solution set.

#### Geometric interpretation

For two variables, the solution set represents the intersection (if it occurs)
of two lines:

![](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/Linear_Function_Graph.svg/600px-Linear_Function_Graph.svg.png)
(source: [Wikipedia](https://en.wikipedia.org/wiki/Linear_equation#/media/File:Linear_Function_Graph.svg))

A point (x1,x2) is a solution (satisfies both equations) iff it lies on both lines.

For three variables, the solution set represents the intersection of planes in
three dimensional space, e.g. for two equations:

![](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d6/Intersecting_Planes_2.svg/480px-Intersecting_Planes_2.svg.png)
(source: [Wikipedia](https://en.wikipedia.org/wiki/File:Intersecting_Planes_2.svg))

#### Possible solutions

A system of linear equations has either:

1. No solutions (e.g. two linear that don't intersect)
2. One solution (e.g. lines intersecting at a single point)
3. Infinitely many solutions (e.g. two equations describing the same line)

This makes sense because we are talking about equations of _lines_. Unlike
parabolas, etc., a line can't intersect another line multiple times, unless
they are the same.

### Matrix notation

A linear system can be represented using a single matrix:

- **coefficient matrix**: values represent variable coefficients
- **augmented matrix**: same thing but with the RHS constant part of the linear
  equations.

Example (Wikipedia):

System of linear equations:

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/6ec576274d4b6ff0127ce52790ad9f71c4c2e2bc)

Augmented matrix for that system:

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/6d99c79eb45b325d779be9693c613d9aec07b6d4)

Dimension (rows x columns):

- _m_ x _n_ (Lay)
- _n_ x _p_ (Commonly used in machine learning)

### Solving a linear system

To solve a linear set of equations, we use **elementary row operations** to
iteratively replace our system of equations with a simpler _equivalent_ system.

#### Elementary row operations

1. **Replacement** - Replace one row by the sum of itself with a multiple of
   another row.
2. **Interchange** - Swap two rows.
3. **Scaling** - Replace a row my the product of itself with a non-zero
   constant.

- Two matrices are said to be **row equivalent** if you can switch between them
using only elementary row operations.
- If two augmented matrices are row equivalent, the the two systems have the
  same solution set.

Example:

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/5f6367f306a7947555dd25f9b3b29a5903efdabb)

(Source: [Wikpedia](https://en.wikipedia.org/wiki/System_of_linear_equations); Thank you Wikipedia for saving me from so much typing!)

#### Existence and Uniqueness

A couple important questions to consider about a set of equations:

- Does a system of equations have at least one solution (is is **consistent**?)
- If a solution exists, is it unique?

## References

1. [Linear Algebra and its applications (Lay 3e)](http://www.laylinalgebra.com/)
2. [Linear Equation - Wikipedia](https://en.wikipedia.org/wiki/Linear_equation)
3. [Linear Regression - Wikipedia](https://en.wikipedia.org/wiki/Linear_regression)
4. [What Is the Difference between Linear and Nonlinear Equations in Regression Analysis?](http://blog.minitab.com/blog/adventures-in-statistics/what-is-the-difference-between-linear-and-nonlinear-equations-in-regression-analysis)
