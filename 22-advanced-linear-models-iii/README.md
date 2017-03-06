-   [Overview](#overview)
-   [Lay 6.5 - 6.6](#lay-6.5---6.6)
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

Lay 6.5 - 6.6
=============

6.5 Least-squares problems
--------------------------

### Overview

-   When a sytem represented by ![Ax = b](https://latex.codecogs.com/png.latex?Ax%20%3D%20b "Ax = b") has no solution, it is *inconsistent*
-   In this case, the best you can do is find an ![x](https://latex.codecogs.com/png.latex?x "x") that makes ![Ax](https://latex.codecogs.com/png.latex?Ax "Ax") as close to ![b](https://latex.codecogs.com/png.latex?b "b") as possible.
-   The **general least-squares problem** is to find an ![x](https://latex.codecogs.com/png.latex?x "x") that makes ![||b - Ax||](https://latex.codecogs.com/png.latex?%7C%7Cb%20-%20Ax%7C%7C "||b - Ax||") as small as possible.
-   *No matter what x we select, the vector Ax will necessarily be in the column space, ColA*.
-   So the solution, ![x](https://latex.codecogs.com/png.latex?x "x") is the vector which makes ![Ax](https://latex.codecogs.com/png.latex?Ax "Ax") the closest point in Col![A](https://latex.codecogs.com/png.latex?A "A") to ![b](https://latex.codecogs.com/png.latex?b "b").

### Solution of the General Least-Squares Problem

**Best Approximation Theorem**

Let ![W](https://latex.codecogs.com/png.latex?W "W") be a subspace of ![ℝ^n](https://latex.codecogs.com/png.latex?%E2%84%9D%5En "ℝ^n"), ![y](https://latex.codecogs.com/png.latex?y "y") any vector in ![ℝ^n](https://latex.codecogs.com/png.latex?%E2%84%9D%5En "ℝ^n"), and ![\\hat{y}](https://latex.codecogs.com/png.latex?%5Chat%7By%7D "\hat{y}") the orthogonal projection of ![y](https://latex.codecogs.com/png.latex?y "y") onto ![W](https://latex.codecogs.com/png.latex?W "W"). Then ![\\hat{y}](https://latex.codecogs.com/png.latex?%5Chat%7By%7D "\hat{y}") is the closest point in ![W](https://latex.codecogs.com/png.latex?W "W") to ![y](https://latex.codecogs.com/png.latex?y "y") in the sense that:

![
||y - \\hat{y}|| &lt; ||y - v||
](https://latex.codecogs.com/png.latex?%0A%7C%7Cy%20-%20%5Chat%7By%7D%7C%7C%20%3C%20%7C%7Cy%20-%20v%7C%7C%0A "
||y - \hat{y}|| < ||y - v||
")

for all ![v](https://latex.codecogs.com/png.latex?v "v") in ![W](https://latex.codecogs.com/png.latex?W "W") from ![\\hat{y}](https://latex.codecogs.com/png.latex?%5Chat%7By%7D "\hat{y}").

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

1.  Lay Chapters 6.5 - 6.6
2.  Dobson, A. J., & Barnett, A. (2008). An introduction to generalized linear models. CRC press. (Chapter 6)
