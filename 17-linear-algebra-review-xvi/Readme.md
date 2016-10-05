<h1>
Linear Algebra Review IX
</h1>
-   Jonathan Goodson
-   October 5, 2016

## 7.2 Quadratic Forms</sup> 

Quadratic forms are *functions* defined in ℝ<sup>n</sup> at single vector values in ℝ<sup>n</sup>, by the equation:

	**Q** = *x*<sup>**T**</sup>**A***x*
	
Where **A** is a *symmetric* matrix, referred to as the *matrix of the quadratic form*.

Reminder, symmetric matrices are those where **A**=**A**<sup>T</sup>

See 7.2 Examples 1 and 2

This quadratic form is easy to calculate. Entries along the diagonal of the matrix result in squared terms. Entries
off of the diagonal result in terms such as **ax**<sub>1</sub>**x**<sub>2</sub> or cross-product terms. These
can be inconvenient for some purposes. They can be avoided with a *change of variable*.

### Changes of variables

One can imagine substituting a different variable, *y* for *x* with a compensating change in the matrix 
in the quadratic form which will result in the same function **Q**. If one choses the variable *y* carefully,
the compensating matrix may be a diagonal matrix.

First, we can more carefully define our change of variable (P of course must be invertible):

	*x* =  **P***y*    and    *y* = **P**<sup>-1</sup>*x*
	
Next, simply sub *y* in for *x* and simplify.

	*x*<sup>T</sup>**A***x* = (**Py***y*)<sup>T</sup>**A**(**P***y*) = *y*<sup>T</sup>**P**<sup>T</sup>**AP***y* = *y*<sup>T</sup>(**P**<sup>T</sup>**AP**)*y*
	
Putting to use theorem 2 from last week, since **A** is symmetric, there must be
a **P** such that **P**<sup>T</sup>**AP** is diagonal. (By computing the eigenvalues and using
the proper eigenvectors to construct **P** which will diagonalize **A** resulting in a 
diagonal matrix **D** consisting of the eigenvalues of **A**) This results in a quadratic form 
with no cross products and coefficients determined by the eigenvalues of **A** in the order used to
construct **PP**.

For details, see working of 7.2 Example 4

This is summarized by *The Principal Axes Theorem*:

	Let **A** be an **n** x **n** symmetric matrix. Then there is an orthogonal change of variable, *x* = **P***y*, that transforms the quadratic form *x*<sup>T</sup>**A***x* into a quadratic form *y*<sup>T</sup>**D***y* with no cross-product term.
	
### A Geometric View of Principal Axes

See textbook, this does a great job and I don't want to reproduce all the images here...

The general gist is the quadratic form can easily be seen to represent the traditional parametric form
of an equation, and if set to a constant value, results (for forms in ℝ<sup>2</sup>) in an equation for either a:
ellipse, hyperbola, intersection lines, a point, or has no real solutions.

These will all be centered on the origin, but if the matrix of the quadratic form is not diagonal, the resulting 
geometric form will be rotated due to the presence of the cross-product term. The process of changing the variables
and diagonalizing the matrix results in a second set of axes in which the form is not rotated. This has parallels with
our other interpretations of eigenvalues and eigenvectors as projecting a geometric interpretation onto different axes.

### Classifying Quadratic Forms

Quadratic forms come in one of a few classes that can be useful for characterization. These classes are based 
on the behavior of the form across all vectors in the defined space. If a form is always positive for non-zero vectors
it is defined as *positive definite*, while if a form is always negative for non-zero vectors it is *negative definite*.
Forms which result in both negative and positive values are *indefinite*.

There is a corresponding theorem which equates these classes with characteristics of the eigenvalues of the matrix of the 
quadratic form:

Quadratic Forms and Eigenvalues
Let **A** be an **n** x **n** symmetric matrix. Then a quadratic form *x*<sup>T</sup>**A***x* is:
a. positive definite if and only if the eigenvalues of *A* are all positive,
b. negative definite if and only if the eigenvalues of **A** are all negative, or 
c. indefinite if and only if **A** has both positive and negative eigenvalues.