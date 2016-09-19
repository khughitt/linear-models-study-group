-   [Least-squares Problems](#least-squares-problems)
    -   [Overview](#overview)
-   [References](#references)

<h1>
Linear Algebra Review XIV
</h1>
-   Keith Hughitt
-   Sept 19, 2016

Least-squares Problems
======================

Overview
--------

So far, much of the linear algebra discussion has been focused on matrices which could be used to represent *consistent* systems of linear equations, i.e. ones which have solutions.

In these cases, there exists one or more values for ![x](http://chart.apis.google.com/chart?cht=tx&chl=x "x") such that ![Ax = b](http://chart.apis.google.com/chart?cht=tx&chl=Ax%20%3D%20b "Ax = b").

Here, we discuss how to deal with systems for which there is *no valid solutions* to the matrix equation ![Ax = b](http://chart.apis.google.com/chart?cht=tx&chl=Ax%20%3D%20b "Ax = b"). Instead, we will seek to find an ![x](http://chart.apis.google.com/chart?cht=tx&chl=x "x") that is "close" to a solution, in fact, one that is as close as we can get.

In this scenario, ![Ax](http://chart.apis.google.com/chart?cht=tx&chl=Ax "Ax") can be thought of as an *approximation* to ![b](http://chart.apis.google.com/chart?cht=tx&chl=b "b").

### General least-squares problem

The **General least-squares problem** is to find an ![x](http://chart.apis.google.com/chart?cht=tx&chl=x "x") that makes ![||b - Ax||](http://chart.apis.google.com/chart?cht=tx&chl=%7C%7Cb%20-%20Ax%7C%7C "||b - Ax||") as small as possible. \[1\]

Recall that the **norm** of a vector, ![||v||](http://chart.apis.google.com/chart?cht=tx&chl=%7C%7Cv%7C%7C "||v||") is defined as:

![](../12-linear-algebra-review-xii/img/norm.png)

The "squares" in "least-squares" refers to the square root of the sum of squares above.

#### Definition

*From Lay 6.5:*

If ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") is ![m \\times n](http://chart.apis.google.com/chart?cht=tx&chl=m%20%5Ctimes%20n "m \times n") and ![\\textbf{b}](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7Bb%7D "\textbf{b}") is in ![ℝ^m](http://chart.apis.google.com/chart?cht=tx&chl=%E2%84%9D%5Em "ℝ^m"), a **least-squares solution** of ![Ax = \\textbf{b}](http://chart.apis.google.com/chart?cht=tx&chl=Ax%20%3D%20%5Ctextbf%7Bb%7D "Ax = \textbf{b}") is ![\\hat{x}](http://chart.apis.google.com/chart?cht=tx&chl=%5Chat%7Bx%7D "\hat{x}") in ![ℝ^n](http://chart.apis.google.com/chart?cht=tx&chl=%E2%84%9D%5En "ℝ^n") such that:

$$
||\\textbf{b} - A\\hat{x}|| \\leq || \\textbf{b} - Ax||
$$

for all ![\\textbf{x}](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7Bx%7D "\textbf{x}") in ![ℝ^n](http://chart.apis.google.com/chart?cht=tx&chl=%E2%84%9D%5En "ℝ^n").

In the context of a data matrix:

-   ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") = observed data values
-   ![\\textbf{x}](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7Bx%7D "\textbf{x}") = coefficient weights
-   ![\\textbf{b}](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7Bb%7D "\textbf{b}") = response / depdendent variable

And ![A\\textbf{x}](http://chart.apis.google.com/chart?cht=tx&chl=A%5Ctextbf%7Bx%7D "A\textbf{x}") gives us our estimate of the response variables for each row.

**Relation to Col A** (6.5, fig 1)

-   All possible ![A\\textbf{x}](http://chart.apis.google.com/chart?cht=tx&chl=A%5Ctextbf%7Bx%7D "A\textbf{x}")'s will be in the column space of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A")
-   Therefor we aim to find an ![\\textbf{x}](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7Bx%7D "\textbf{x}") such that ![A\\textbf{x}](http://chart.apis.google.com/chart?cht=tx&chl=A%5Ctextbf%7Bx%7D "A\textbf{x}") is the closest point in Col A to ![\\textbf{b}](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7Bb%7D "\textbf{b}").

### Solutions of the general least-squares problem

#### Background

Using the *Best Approximate Theorem* from 6.3 (which basically says that the closest point in a subspace ![W](http://chart.apis.google.com/chart?cht=tx&chl=W "W") to a given point in ![ℝ^n](http://chart.apis.google.com/chart?cht=tx&chl=%E2%84%9D%5En "ℝ^n") is the projection from that point to ![W](http://chart.apis.google.com/chart?cht=tx&chl=W "W")), we have:

$$
\\hat{b} = \\text{proj}\_{\\text{Col}A} \\textbf{b}
$$

![](img/640px-OLS_geometric_interpretation.svg.png) (source: [Wikipedia](https://en.wikipedia.org/wiki/Ordinary_least_squares#/media/File:OLS_geometric_interpretation.svg))

-   ![A\\textbf{x} = \\textbf{b}](http://chart.apis.google.com/chart?cht=tx&chl=A%5Ctextbf%7Bx%7D%20%3D%20%5Ctextbf%7Bb%7D "A\textbf{x} = \textbf{b}") is consistent
-   Therefore, there is an ![\\hat{x}](http://chart.apis.google.com/chart?cht=tx&chl=%5Chat%7Bx%7D "\hat{x}") in ![ℝ^n](http://chart.apis.google.com/chart?cht=tx&chl=%E2%84%9D%5En "ℝ^n") such that ![A\\hat{x} = \\hat{b}](http://chart.apis.google.com/chart?cht=tx&chl=A%5Chat%7Bx%7D%20%3D%20%5Chat%7Bb%7D "A\hat{x} = \hat{b}")
-   The vector ![\\hat{x}](http://chart.apis.google.com/chart?cht=tx&chl=%5Chat%7Bx%7D "\hat{x}") is the least-squares solution to ![A\\textbf{x} = \\textbf{b}](http://chart.apis.google.com/chart?cht=tx&chl=A%5Ctextbf%7Bx%7D%20%3D%20%5Ctextbf%7Bb%7D "A\textbf{x} = \textbf{b}")!

In other words:

**The least-squares solution is the projection of ![\\textbf{b}](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7Bb%7D "\textbf{b}") onto Col A.**

**Note**: If there are free variables, then there will be many solutions to this equation!

#### A simpler formulation

-   Suppose ![\\hat{x}](http://chart.apis.google.com/chart?cht=tx&chl=%5Chat%7Bx%7D "\hat{x}") satisfies ![A\\hat{x} = \\hat{b}](http://chart.apis.google.com/chart?cht=tx&chl=A%5Chat%7Bx%7D%20%3D%20%5Chat%7Bb%7D "A\hat{x} = \hat{b}")
-   Then by the Orthogonal Decomposition Theorem (section 6.3), we know that ![\\textbf{b} - \\hat{b} \\perp \\text{Col} A](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7Bb%7D%20-%20%5Chat%7Bb%7D%20%5Cperp%20%5Ctext%7BCol%7D%20A "\textbf{b} - \hat{b} \perp \text{Col} A")
    -   Therefore, ![\\textbf{b} - A \\hat{x}](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7Bb%7D%20-%20A%20%5Chat%7Bx%7D "\textbf{b} - A \hat{x}") is orthogonal to Col ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") (which also means it is orthogonal to each column in ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"))
    -   ODT: Each ![y](http://chart.apis.google.com/chart?cht=tx&chl=y "y") in ![ℝ^n](http://chart.apis.google.com/chart?cht=tx&chl=%E2%84%9D%5En "ℝ^n") can be written uniquely as a sum of two vectors:
        1.  linear combination of some set of vectors in a subspace of ![ℝ^n](http://chart.apis.google.com/chart?cht=tx&chl=%E2%84%9D%5En "ℝ^n") (![W](http://chart.apis.google.com/chart?cht=tx&chl=W "W")), and,
        2.  linear combination of some set of vectors orthogonal to ![W](http://chart.apis.google.com/chart?cht=tx&chl=W "W").
    -   Note: Compare figures 6.3 fig2 & 6.5 fig2...
-   Next, since the dot product of two orthogonal vectors equals zero, for any column ![a\_j](http://chart.apis.google.com/chart?cht=tx&chl=a_j "a_j") in ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"), we have ![a\_j \\cdot (\\textbf{b} - A \\hat{x}) = 0](http://chart.apis.google.com/chart?cht=tx&chl=a_j%20%5Ccdot%20%28%5Ctextbf%7Bb%7D%20-%20A%20%5Chat%7Bx%7D%29%20%3D%200 "a_j \cdot (\textbf{b} - A \hat{x}) = 0"), and
-   **DISCUSS** ![a\_j^T \\cdot (\\textbf{b} - A \\hat{x}) = 0](http://chart.apis.google.com/chart?cht=tx&chl=a_j%5ET%20%5Ccdot%20%28%5Ctextbf%7Bb%7D%20-%20A%20%5Chat%7Bx%7D%29%20%3D%200 "a_j^T \cdot (\textbf{b} - A \hat{x}) = 0")
-   Since each ![a\_j^T](http://chart.apis.google.com/chart?cht=tx&chl=a_j%5ET "a_j^T") is a row in ![A^T](http://chart.apis.google.com/chart?cht=tx&chl=A%5ET "A^T"),

$$
A^T(\\textbf{b} - A\\hat{x}) = 0
$$

which leads to:

$$
A^T\\textbf{b} - A^TA\\hat{x} = 0
A^TA\\hat{x} = A^T\\textbf{b}
$$

So each least-squares solution thus satisfies:

*A*<sup>*T*</sup>*A***x** = *A*<sup>*T*</sup>**b**

This equation represents a system of equations called the **normal equations** for ![Ax = b](http://chart.apis.google.com/chart?cht=tx&chl=Ax%20%3D%20b "Ax = b"), and solutions to this are often written as ![\\hat{x}](http://chart.apis.google.com/chart?cht=tx&chl=%5Chat%7Bx%7D "\hat{x}").

**Theorem 13**

The set of least-squares solution of ![Ax = b](http://chart.apis.google.com/chart?cht=tx&chl=Ax%20%3D%20b "Ax = b") coincides with the nonempty set of solutions of the normal equations ![A^TA\\textbf{x} = A^T\\textbf{b}](http://chart.apis.google.com/chart?cht=tx&chl=A%5ETA%5Ctextbf%7Bx%7D%20%3D%20A%5ET%5Ctextbf%7Bb%7D "A^TA\textbf{x} = A^T\textbf{b}").

-   Example 1 goes over a simple example of finding ![\\hat{x}](http://chart.apis.google.com/chart?cht=tx&chl=%5Chat%7Bx%7D "\hat{x}")...
-   Steps:
    -   find ![A^TA](http://chart.apis.google.com/chart?cht=tx&chl=A%5ETA "A^TA")
    -   find ![A^T \\textbf{b}](http://chart.apis.google.com/chart?cht=tx&chl=A%5ET%20%5Ctextbf%7Bb%7D "A^T \textbf{b}")
    -   substitute parts back into *normal equations* formula above.
    -   To find ![x](http://chart.apis.google.com/chart?cht=tx&chl=x "x"), can use row reduction, however, in this example they use matrix inversion instead:
        -   **Section 2.2 Thm 4** (formula for finding ![A^{-1}](http://chart.apis.google.com/chart?cht=tx&chl=A%5E%7B-1%7D "A^{-1}") for 2x2 matrices using the determinant of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A"))
        -   **Section 2.2 Thm 5** (for invertible matrices, ![\\textbf{x} = A^{-1}\\textbf{b}](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7Bx%7D%20%3D%20A%5E%7B-1%7D%5Ctextbf%7Bb%7D "\textbf{x} = A^{-1}\textbf{b}"))

**NOTE**: ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") need not be invertible! Example 2 provides a problem where this is not the case.

The final formulation of the general least-squares problem is the one that we are probably most familiar with, having worked with linear models previously:

**Theorem 14**

The matrix ![A^TA](http://chart.apis.google.com/chart?cht=tx&chl=A%5ETA "A^TA") is invertible *if and only if* the columns of ![A](http://chart.apis.google.com/chart?cht=tx&chl=A "A") are linearly independent. In this case, the equation ![Ax = b](http://chart.apis.google.com/chart?cht=tx&chl=Ax%20%3D%20b "Ax = b") has only *one* least-squares solution ![\\hat{x}](http://chart.apis.google.com/chart?cht=tx&chl=%5Chat%7Bx%7D "\hat{x}"), and it is given by:

$$
\\hat{x} = (A^TA)^{-1}A^T \\textbf{b}
$$

The distance from ![\\textbf{b}](http://chart.apis.google.com/chart?cht=tx&chl=%5Ctextbf%7Bb%7D "\textbf{b}") to ![A\\hat{x}](http://chart.apis.google.com/chart?cht=tx&chl=A%5Chat%7Bx%7D "A\hat{x}") is called the **least-squares error**.

References
==========

1.  *Lay* chapter 6.5-6.6
2.  <https://en.wikipedia.org/wiki/Ordinary_least_squares>
