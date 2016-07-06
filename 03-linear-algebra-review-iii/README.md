Linear Algebra Review III
=======================

- Candice Schumann
- July 6, 2016

## 1.5 Solution Sets of Linear Systems

A homogeneous equation always has one solution, the zero vector.

![homogeneous equation](img/homogeneous.png)

The homogeneous equation has a nontrivial solution if and only if the equation has at least one free variable.

![geometric example](img/geometric_homogeneous.png)

#### Parametric Vector Form

This form explicitly describes the plane as the set spanned by vectors **u** and **v**. It emphasizes that the parameters vary over all real numbers.

![parametric vector form](img/parametric.png)

#### Solutions of Nonhomogeneous Systems

When a nonhomogeneous linear system has many solutions, the general solution can be written in parametric vector form as one vector plus an arbitrary linear combination of vectors that satisfy the corresponding homogeneous system.

The solution to *A***x**=**b** can be written as

![solution to Ax=b](img/solution1.png)

The solution to *A***x**=**0** can be written as

![Solution to Ax=0](img/solution2.png)

![Geometric example](img/geometric_parallel.png)

#### Theorem 6

Suppose the equation ![Nonhomogeneous](img/nonhomogeneous.png) is consistent for some given **b**, and let **p** be a solution. Then the solution set of ![Nonhomogeneous](img/nonhomogeneous.png) is the set of all vectors of the form ![Solution to nonhoogeneous](img/nonhomo_solution.png), where ![v_h](img/v_h.png) is any solution of the homogenous equation ![homogeneous](img/homogeneous.png).

## 1.7 Linear Independence

#### Definition of Linear Independence

An indexed set of vectors ![{v_1,...,v_p}](img/vectors.png) in ![R^n](img/reals.png) is said to be linearly independent if the vector equation 
![x_1v_1+x_2v_2+...+x_pv_p=0](img/independent.png)
has only the trivial solution. The set ![{v_1,...,v_p}](img/vectors.png) is said to be linearly dependent if there exists weights ![c_1,...,c_p](img/weights.png), not all zero, such that
![c_1v_1+c_2v_2+...+c_pv_p=0](img/dependent.png)


Therefore by section 1.5, the vectors are dependent if the equation ![Ax=0](img/homogeneous.png) has at least one free variable. If there are no free variables then the vectors are independent.

#### Special cases

If a set only contains one vector then the set is independent if that vector is not the zero vector.

A set of two vectors is linearly dependent if at least one of the vectors is a multiple of another. The set is linearly independent if and only if neither of the vectors is a multiple of the other.

#### Linearly dependent sets

An indexed set ![S={v_1,...v_p}](img/indexed_set.png) of two or more vectors is linearly dependent if and only if at least one of the vectors in ![S](img/s.png) is a linear combination of the others. In fact, if ![S](img/s.png) is linearly dependent and ![v_1<>0](img/v1_neq_0.png), then some ![v_j](img/v_j.png) (with ![j>1](img/j.png)) is a linear combination of the preceding vectors, ![v_1,...,v_j-1](img/preceding_vectors.png).

![visual of independence](http://www.mathsisfun.com/algebra/images/system-linear-types.gif)

#### Theorem 8

If a set contains more vectors than there are entries in each vector, then the set is linearly dependent. That is, any set ![{v_1,...,v_p}](img/vectors.png) in ![R^n](img/reals.png) is linearly dependent if ![p>n](img/p_n.png).

#### Theorem 9

If a set ![S={v_1,...v_p}](img/indexed_set.png) in ![R^n](img/reals.png) contain the zero vector, then the set is linearly dependent.
