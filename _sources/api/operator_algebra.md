Operator Algebra
================

In many boundary element method applications, a discretisation of the product of two operators
is required.

Let $\mathsf{A}$ and $\mathsf{B}$ be two operators with discretisations $A_h$ and $B_h$.
A discretisation of the product $\mathsf{A}\mathsf{B}$ is given by $A_hM^{-1}B_h$,
where $M$ is the mass matrix between the range and dual of the operator $\mathsf{B}$.

In Bempp, the discrete product of two operators can be formed using:
```python
op1 = bempp.api.operators.boundary...
op2 = bempp.api.operators.boundary...
product = op1 * op2
```
If `product.weak_form()` is called, Bempp will internally use its knowledge of the range space
of `op2` to correctly from the discretisation of this product.

Calling the `strong_form` of an operator $\mathsf{B}$ will return the product
$M^{-1}B_h$. Calling `product.weak_form()` is equivalent to calculating
`op1.weak_form() * op2.strong_form()`. Using the strong form of operators can in general
be useful, as the discretisation obtained corresponds to a mass matrix preconditioned
version of the relevant formulation.
