Linear Algebra Review III
=======================

- Candice Schumann
- July 6, 2016

## 1.5 Solution Sets of Linear Systems

A homogeneous equation always has one solution, the zero vector.

![homogeneous equation](img/homogeneous.png)

The homogeneous equation has a nontrivial solution if and only if the equation has at least one free variable.

![geometric example](img/geometric_homogeneous)

#### Parametric Vector Form

This form explicitly describes the plane as the set spanned by vectors **u** and **v**. It emphasizes that the parameters vary over all real numbers.

![parametric vector form](img/parametric.png)

#### Solutions of Nonhomogeneous Systems

When a nonhomogeneous linear system has many solutions, the general solution can be written in parametric vector form as one vector plus an arbitrary linear combination of vectors that satisfy the corresponding homogeneous system.

The solution to *A***x**=**b** can be written as

![solution to Ax=b](img/solution1.png)

The solution to *A***x**=**0** can be written as

![Solution to Ax=0](img/solution2.png)

![Geometric example](img/geometric_parallel)

#### Theorem 6

Suppose the equation ![Nonhomogeneous](img/nonhomogeneous.png) is consistent for some given **b**, and let **p** be a solution. Then the solution set of ![Nonhomogeneous](img/nonhomogeneous.png) is the set of all vectors of the form ![Solution to nonhoogeneous](img/nonhomo_soltion.png), where ![v_h](img/v_h.png) is any solution of the homogenous equation ![homogeneous](img/homogeneous.png).

