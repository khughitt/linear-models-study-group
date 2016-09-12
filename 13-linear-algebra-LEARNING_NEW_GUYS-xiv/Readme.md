<h1>
Linear Algebra Review IX
</h1>
-   Jonathan Goodson
-   September 12, 2016

## 6.2 Orthogonal Sets</sup> 

### Orthogonal sets

A set of vectors are an **orthogonal set** if each pair of distint vectors in the set is orthogonal. **u**<sub>i</sub>•**u**<sub>y</sub>=0 whenever *i*≠*j*.

Theorem 4:

If *S* = {**u**<sub>1</sub>m ..., **u**<sub>p</sub>} is an orthogonal set of nonzero vectors in ℝ<sup>n</sup>, then *S* is linearly independent and hence is a basis for the subspace spanned by *S*.

An **orthogonal basis** for a subspace *W* of ℝ<sup>n</sup> is a basis for *W* that is also an orthogonal set.

Theorem 5:

Let {**u**<sub>1</sub>m ..., **u**<sub>p</sub>} be an orthogonal basis for a subspace *W* of ℝ<sup>n</sup>. For each **y** in *W*, the weights in the linear combination

	**y** = *c*<sub>1</sub>**u**<sub>1</sub> + ... + *c*<sub>p</sub>**u**<sub>p</sub>
	
are given by

	*c*<sub>j</sub> = **y**•**u**<sub>j</sub> / **u**<sub>j</sub>•**u**<sub>j</sub>
	where *j* = 1, ..., *p*
	
This allows one to easily calculate the weights for an arbitrary vector in the subspace spanned by the orthogonal set as a linear combination of the orthogonal vectors without having to solve the complete system of equations.

### An Orthogonal Projection

An orthogonal projection involves decomposing a vector **y** into two orthogonal vectors, one of which is a multiple of **y**.

	**y** = **ŷ** + **z**
	
	where **ŷ** = α**u** and **z** is orthogonal to **u**
	
The vector **ŷ** is the **orthogonal projection of y onto u** and the vector **z** is the **component of y orthogonal to u**.

Sometimes **ŷ** is represented by proj<sub>L</sub>**y** and called the **orthogonal projection of y onto** *L*, where *L* is the line spanned by **y**.

**ŷ** is the point on *L* that is *closest* to **y**. 

![Orthogonal Projection](orth_proj.png)

![Least-squares representation](least_squares_proj.png)

### Orthonormal sets

An **orthonormal set** is an orthogonal set where all vectors are of unit length. If *W* is the subspace spanned by this set, this the set is an **orthonormal basis** for the subspace *W*.

An **orthogonal set** can be made into an **orthonormal set** by *normalizing* the vector lengths, and the set remains orthogonal.

Theorem 6:

An *m* x *n* matrix *U* has orthonormal columns if and only if *U*<sup>T</sup>*U* = *I*.

This is proved by doing the matrix multiplication and utilizing the definition of an orthogonal set.

Theorem 7:

Let *U* be an *m* x *n* matrix with orthonormal columns, and let *x* and *y* be in ℝ<sup>n</sup>. Then

	a. ||*U***x**|| = ||**x**||
	b. (*U***x**)•(*U***y**) = **x**•**y**
	c. (*U***x**)•(*U***y**) = 0 if and only if **x**•**y** = 0