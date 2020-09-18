Function Spaces
===============

To use the boundary element method, we start with a variational boundary integral
equation, for example: Find $u\in H^{1/2}(\Gamma)$ such that for all $v\in H^{1/2}(\Gamma)$,

$$
\left\langle\mathsf{V}u,v\right\rangle = \left\langle f,v\right\rangle.
$$

An approximation of the solution of this problem is then found by discretising the problem
and searching for a solution in a subspace $\mathcal{V}_h\subset H^{1/2}(\Gamma)$.

In this section of the Bempp Handbook, we look at the definitions of
[continuous function spaces such as $H^{1/2}(\Gamma)$](sobolev_spaces.md)
that are used in the boundary integral equations, and we look at how
[discrete subspaces](discrete_function_spaces.md) of these are usually defined.
