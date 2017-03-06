-   [Overview](#overview)
-   [Lay 6.5](#lay-6.5)
    -   [6.5 Least-squares problems](#least-squares-problems)
-   [Dobson & Barnett Chapter 6: Normal Linear Models](#dobson-barnett-chapter-6-normal-linear-models)
-   [References](#references)

<h1>
Advanced Linear Models III
</h1>
-   Keith Hughitt
-   March 06, 2017

Overview
========

This week will be a brief digression from the current series of notes which follow the Advanced Linear Models Coursera course.

Instead, this week I will review the basic of linear models as they are introduced from a couple different sources:

1.  A linear algebra textbook (Lay)
2.  A GLM textbook (Dobson & Barnett)

Interestingly, in the Lay formulation of the least-squares solution, we are able to arrive at the familiar expression for the solution using only the tools of basic linear algebra (i.e. no differentiation.)

Lay 6.5
=======

6.5 Least-squares problems
--------------------------

### Overview

-   When a sytem represented by ![Ax = b](https://latex.codecogs.com/png.latex?Ax%20%3D%20b "Ax = b") has no solution, it is *inconsistent*
-   In this case, the best you can do is find an ![x](https://latex.codecogs.com/png.latex?x "x") that makes ![Ax](https://latex.codecogs.com/png.latex?Ax "Ax") as close to ![b](https://latex.codecogs.com/png.latex?b "b") as possible.
-   The **general least-squares problem** is to find an ![x](https://latex.codecogs.com/png.latex?x "x") that makes ![||b - Ax||](https://latex.codecogs.com/png.latex?%7C%7Cb%20-%20Ax%7C%7C "||b - Ax||") as small as possible.
-   *No matter what x we select, the vector Ax will necessarily be in the column space, ColA*.
-   So the solution, ![x](https://latex.codecogs.com/png.latex?x "x") is the vector which makes ![Ax](https://latex.codecogs.com/png.latex?Ax "Ax") the closest point in Col![A](https://latex.codecogs.com/png.latex?A "A") to ![b](https://latex.codecogs.com/png.latex?b "b").

### Solution of the General Least-Squares Problem

**Best Approximation Theorem** (Lay 6.3)

Let ![W](https://latex.codecogs.com/png.latex?W "W") be a subspace of ![ℝ^n](https://latex.codecogs.com/png.latex?%E2%84%9D%5En "ℝ^n"), ![y](https://latex.codecogs.com/png.latex?y "y") any vector in ![ℝ^n](https://latex.codecogs.com/png.latex?%E2%84%9D%5En "ℝ^n"), and ![\\hat{y}](https://latex.codecogs.com/png.latex?%5Chat%7By%7D "\hat{y}") the orthogonal projection of ![y](https://latex.codecogs.com/png.latex?y "y") onto ![W](https://latex.codecogs.com/png.latex?W "W"). Then ![\\hat{y}](https://latex.codecogs.com/png.latex?%5Chat%7By%7D "\hat{y}") is the closest point in ![W](https://latex.codecogs.com/png.latex?W "W") to ![y](https://latex.codecogs.com/png.latex?y "y") in the sense that:

![
||y - \\hat{y}|| &lt; ||y - v||
](https://latex.codecogs.com/png.latex?%0A%7C%7Cy%20-%20%5Chat%7By%7D%7C%7C%20%3C%20%7C%7Cy%20-%20v%7C%7C%0A "
||y - \hat{y}|| < ||y - v||
")

for all ![v](https://latex.codecogs.com/png.latex?v "v") in ![W](https://latex.codecogs.com/png.latex?W "W") from ![\\hat{y}](https://latex.codecogs.com/png.latex?%5Chat%7By%7D "\hat{y}").

We can use this theorem to find the closest point in Col![A](https://latex.codecogs.com/png.latex?A "A") to ![b](https://latex.codecogs.com/png.latex?b "b").

Let:

![
\\hat{b} = \\text{proj}\_{ColA} b
](https://latex.codecogs.com/png.latex?%0A%5Chat%7Bb%7D%20%3D%20%5Ctext%7Bproj%7D_%7BColA%7D%20b%0A "
\hat{b} = \text{proj}_{ColA} b
")

Recall, from Lay 6.2, an **orthogonal projection** is defined as:

![
\\hat{y}{  = \\text{proj}\_L y = \\frac{y \\cdot u}{u \\cdot u} u
](https://latex.codecogs.com/png.latex?%0A%5Chat%7By%7D%7B%20%20%3D%20%5Ctext%7Bproj%7D_L%20y%20%3D%20%5Cfrac%7By%20%5Ccdot%20u%7D%7Bu%20%5Ccdot%20u%7D%20u%0A "
\hat{y}{  = \text{proj}_L y = \frac{y \cdot u}{u \cdot u} u
")

Because ![\\hat{b}](https://latex.codecogs.com/png.latex?%5Chat%7Bb%7D "\hat{b}") is in the column space of ![A](https://latex.codecogs.com/png.latex?A "A"), we know that ![Ax = \\hat{b}](https://latex.codecogs.com/png.latex?Ax%20%3D%20%5Chat%7Bb%7D "Ax = \hat{b}") is consistent and there is an ![\\hat{x}](https://latex.codecogs.com/png.latex?%5Chat%7Bx%7D "\hat{x}") in ![ℝ^n](https://latex.codecogs.com/png.latex?%E2%84%9D%5En "ℝ^n") such that:

![
A\\hat{x} = \\hat{b}
](https://latex.codecogs.com/png.latex?%0AA%5Chat%7Bx%7D%20%3D%20%5Chat%7Bb%7D%0A "
A\hat{x} = \hat{b}
")

Since ![\\hat{b}](https://latex.codecogs.com/png.latex?%5Chat%7Bb%7D "\hat{b}") is the closest point in ColA to ![b](https://latex.codecogs.com/png.latex?b "b"), the vector ![\\hat{x}](https://latex.codecogs.com/png.latex?%5Chat%7Bx%7D "\hat{x}") is a least-squares solution of ![Ax = b](https://latex.codecogs.com/png.latex?Ax%20%3D%20b "Ax = b").

### Finding ![\\hat{x}](https://latex.codecogs.com/png.latex?%5Chat%7Bx%7D "\hat{x}")

Going back to the definition of orthogonal projections, we have:

**Orthogonal Decomposition Theorem** (Lay 6.3)

Let ![W](https://latex.codecogs.com/png.latex?W "W") be a subspace of ![ℝ^n](https://latex.codecogs.com/png.latex?%E2%84%9D%5En "ℝ^n"). Then each ![y](https://latex.codecogs.com/png.latex?y "y") in ![ℝ^n](https://latex.codecogs.com/png.latex?%E2%84%9D%5En "ℝ^n") can be written uniquely in the form:

![
y = \\hat{y} + z
](https://latex.codecogs.com/png.latex?%0Ay%20%3D%20%5Chat%7By%7D%20%2B%20z%0A "
y = \hat{y} + z
")

Where ![\\hat{y}](https://latex.codecogs.com/png.latex?%5Chat%7By%7D "\hat{y}") is in ![W](https://latex.codecogs.com/png.latex?W "W") and ![z](https://latex.codecogs.com/png.latex?z "z") in in ![W^\\perp](https://latex.codecogs.com/png.latex?W%5E%5Cperp "W^\perp"). In fact, if ![\\{u\_1,...,u\_p\\}](https://latex.codecogs.com/png.latex?%5C%7Bu_1%2C...%2Cu_p%5C%7D "\{u_1,...,u_p\}") is any orthogonal basis of ![W](https://latex.codecogs.com/png.latex?W "W"), then:

![
\\hat{y} = \\frac{y \\cdot u\_1}{u\_1 \\cdot u\_1} u\_1 + ... + \\frac{y \\cdot u\_p}{u\_p \\cdot u\_p} u\_p
](https://latex.codecogs.com/png.latex?%0A%5Chat%7By%7D%20%3D%20%5Cfrac%7By%20%5Ccdot%20u_1%7D%7Bu_1%20%5Ccdot%20u_1%7D%20u_1%20%2B%20...%20%2B%20%5Cfrac%7By%20%5Ccdot%20u_p%7D%7Bu_p%20%5Ccdot%20u_p%7D%20u_p%0A "
\hat{y} = \frac{y \cdot u_1}{u_1 \cdot u_1} u_1 + ... + \frac{y \cdot u_p}{u_p \cdot u_p} u_p
")

and ![z = y - \\hat{y}](https://latex.codecogs.com/png.latex?z%20%3D%20y%20-%20%5Chat%7By%7D "z = y - \hat{y}")

-   The vector ![\\hat{y}](https://latex.codecogs.com/png.latex?%5Chat%7By%7D "\hat{y}") is called the **orthogonal projection of y onto W**, and often is written as ![\\text{proj}\_W y](https://latex.codecogs.com/png.latex?%5Ctext%7Bproj%7D_W%20y "\text{proj}_W y").
-   *See Lay 6.2 on orthogonal sets and bases*

![Lay 6.5, figure 2](img/lay65fig2.png)

By ODT, the projection ![\\hat{b}](https://latex.codecogs.com/png.latex?%5Chat%7Bb%7D "\hat{b}") has the property that ![b - \\hat{b}](https://latex.codecogs.com/png.latex?b%20-%20%5Chat%7Bb%7D "b - \hat{b}") is orthogonal to ![ColA](https://latex.codecogs.com/png.latex?ColA "ColA"), so ![b - A\\hat{x}](https://latex.codecogs.com/png.latex?b%20-%20A%5Chat%7Bx%7D "b - A\hat{x}") is orthogonal to each column of A.

If ![a\_j](https://latex.codecogs.com/png.latex?a_j "a_j") is any column of A, then ![a\_j \\cdot (b-A\\hat{x}) = 0](https://latex.codecogs.com/png.latex?a_j%20%5Ccdot%20%28b-A%5Chat%7Bx%7D%29%20%3D%200 "a_j \cdot (b-A\hat{x}) = 0"), and ![a\_j^T(b - A\\hat{x}) = 0](https://latex.codecogs.com/png.latex?a_j%5ET%28b%20-%20A%5Chat%7Bx%7D%29%20%3D%200 "a_j^T(b - A\hat{x}) = 0"). Since each ![a\_j^T](https://latex.codecogs.com/png.latex?a_j%5ET "a_j^T") is a row of ![A^T](https://latex.codecogs.com/png.latex?A%5ET "A^T"):

![
A^T(b - A\\hat{x}) = 0
](https://latex.codecogs.com/png.latex?%0AA%5ET%28b%20-%20A%5Chat%7Bx%7D%29%20%3D%200%0A "
A^T(b - A\hat{x}) = 0
")

Thus:

![
A^Tb - A^TA\\hat{x} = 0
](https://latex.codecogs.com/png.latex?%0AA%5ETb%20-%20A%5ETA%5Chat%7Bx%7D%20%3D%200%0A "
A^Tb - A^TA\hat{x} = 0
")

![
A^TA\\hat{x} = A^Tb
](https://latex.codecogs.com/png.latex?%0AA%5ETA%5Chat%7Bx%7D%20%3D%20A%5ETb%0A "
A^TA\hat{x} = A^Tb
")

So the least-squares solution of ![Ax = b](https://latex.codecogs.com/png.latex?Ax%20%3D%20b "Ax = b") satisfies the equation:

![
A^TAx = A^Tb
](https://latex.codecogs.com/png.latex?%0AA%5ETAx%20%3D%20A%5ETb%0A "
A^TAx = A^Tb
")

.

(Work through example 1...)

**Theorem 14**

The matrix ![A^TA](https://latex.codecogs.com/png.latex?A%5ETA "A^TA") is invertible *if and only if* the columns of ![A](https://latex.codecogs.com/png.latex?A "A") are linearly independent. In this case, the equation ![Ax = b](https://latex.codecogs.com/png.latex?Ax%20%3D%20b "Ax = b") has only one least-squares solution, ![\\hat{x}](https://latex.codecogs.com/png.latex?%5Chat%7Bx%7D "\hat{x}"), and it is given by:

![
\\hat{x} = (A^TA)^{-1}A^Tb
](https://latex.codecogs.com/png.latex?%0A%5Chat%7Bx%7D%20%3D%20%28A%5ETA%29%5E%7B-1%7DA%5ETb%0A "
\hat{x} = (A^TA)^{-1}A^Tb
")

Dobson & Barnett Chapter 6: Normal Linear Models
================================================

In this text, models of the form:

![
\\text{E}(Y\_i) = \\mu\_i = \\textbf{x}\_i^T \\beta; Y\_i \\sim \\text{N}(\\mu\_i, \\sigma^2)
](https://latex.codecogs.com/png.latex?%0A%5Ctext%7BE%7D%28Y_i%29%20%3D%20%5Cmu_i%20%3D%20%5Ctextbf%7Bx%7D_i%5ET%20%5Cbeta%3B%20Y_i%20%5Csim%20%5Ctext%7BN%7D%28%5Cmu_i%2C%20%5Csigma%5E2%29%0A "
\text{E}(Y_i) = \mu_i = \textbf{x}_i^T \beta; Y_i \sim \text{N}(\mu_i, \sigma^2)
")

Where:

-   ![Y\_1,...,Y\_N](https://latex.codecogs.com/png.latex?Y_1%2C...%2CY_N "Y_1,...,Y_N") are independent random variables
-   The link function is the identity function, ![g(\\mu\_i) = \\mu\_i](https://latex.codecogs.com/png.latex?g%28%5Cmu_i%29%20%3D%20%5Cmu_i "g(\mu_i) = \mu_i")

This model is often written as:

![
\\textbf{y} = \\textbf{X} \\beta + \\textbf{e}
](https://latex.codecogs.com/png.latex?%0A%5Ctextbf%7By%7D%20%3D%20%5Ctextbf%7BX%7D%20%5Cbeta%20%2B%20%5Ctextbf%7Be%7D%0A "
\textbf{y} = \textbf{X} \beta + \textbf{e}
")

Where the ![e\_i](https://latex.codecogs.com/png.latex?e_i "e_i")'s are IID random variables with ![e\_i \\sim \\textbf{N}(0, \\sigma^2)](https://latex.codecogs.com/png.latex?e_i%20%5Csim%20%5Ctextbf%7BN%7D%280%2C%20%5Csigma%5E2%29 "e_i \sim \textbf{N}(0, \sigma^2)")

Models of this form are called **general linear models** and include:

-   multiple linear regression
-   ANOVA
-   ANCOVA

(Text goes on to show that for these models, maximum likelihood estimators and least squares estimators are the same..)

References
==========

1.  Lay Chapters 6.5
2.  Dobson, A. J., & Barnett, A. (2008). An introduction to generalized linear models. CRC press. (Chapter 6)
