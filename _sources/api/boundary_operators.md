# Boundary Operators

Boundary integral formulations of problems are commonly written using boundary integral operators.
In this section of the Bempp Handbook, we look at how these operators can be defined and
assembled using Bempp.

Full documentation of Bempp boundary operators can be found on [Read the Docs](https://bempp-cl.readthedocs.io/en/latest/docs/bempp/api/operators/index.html).

## Domains, ranges, and duals
When creating an operator in Bempp, three spaces are provided: the domain, the range, and the
dual to the range (given as inputs in that order). The domain and dual spaces are used to
calculate the weak form of the operator. The range is used by the
[operator algebra](#operator-algebra) to correctly assemble product of operators.

## Sparse Boundary Operators

Discretising the identity operator leads to a matrix $M=(m_{ij})$, defined by

$$
m_{ij}=\int_\Gamma\phi_j\cdot\overline{\psi_i},
$$

where $\phi_j$ and $\psi_i$ are the basis functions of the domain and dual spaces respectively.
As this integral will only be non-zero when the basis functions overlap, the resulting
matrix will be sparse.

The identity operator can be created in Bempp using:
```python
ident = bempp.api.operators.boundary.sparse(domain, range_, dual)
```

A `SparseDiscreteBoundaryOperator` can be obtained using:
```python
mat = ident.weak_form()
```
This matrix is commonly called the mass matrix between the domain and dual spaces.

If desiried, a SciPy CSR matrix can be obtained from this discrete boundary operator with:
```python
mat.A
```

## Boundary Operators for Laplace's Equation

For Laplace's equation, there are four boundary operators that are used, as given in the table
below.

Operator             | Symbol        | Matrix entries
-------------------- | ------------- | --------------
Single layer         | $\mathsf{V}$  | $m_{ij}=\int_{\Gamma}\int_{\Gamma}G(\mathbf{x},\mathbf{y})\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$
Double layer         | $\mathsf{K}$  | $m_{ij}=\int_{\Gamma}\int_{\Gamma}\frac{\partial G(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{y}}}\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$
Adjoint double layer | $\mathsf{K}'$ | $m_{ij}=\int_{\Gamma}\int_{\Gamma}\frac{\partial G(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{x}}}\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$
Hypersingular        | $\mathsf{W}$  | $m_{ij}=-\int_{\Gamma}\int_{\Gamma}\frac{\partial^2 G(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{y}}\partial\mathbf{\nu}_{\mathbf{x}}}\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$

In each case,  $\phi_j$ and $\psi_i$ are the basis functions of the domain and dual spaces (respectively),
and $G(\mathbf{x},\mathbf{y})$ is the Green's function for Laplace's equation.
The Green's function will have a singularity when $\mathbf{x}=\mathbf{y}$, so internally Bempp will
use appropriate singular quadrature rules to handle this.

These operators can be initialised in Bempp using:
```python
from bempp.api.operators.boundary import laplace
single = laplace.single_layer(domain, range_, dual)
double = laplace.double_layer(domain, range_, dual)
adjoint_d = laplace.adjoint_double_layer(domain, range_, dual)
hypersingular = laplace.hypersingular(domain, range_, dual)
```
The spaces passed into each operator should be appropriately chosen
[scalar function spaces](function_spaces.md#scalar-function-spaces).

A keyword argument `assembler` may be passed into each constructor to change the assembler
used to assemble the operator. For example, the single layer operator will be discretised using
the fast multipole method (FMM) if it is initialised with:
```python
single = laplace.single_layer(domain, range_, dual, assembler="fmm")
```

When using dense assembly, the keyword argument `device_interface` can be used to switch
between assembly using OpenCL and Numba:
```python
single = laplace.single_layer(
    domain, range_, dual, wavenumber, assembler="dense",
    device_interface="numba"
    )
single = laplace.single_layer(
    domain, range_, dual, wavenumber, assembler="dense",
    device_interface="opencl"
    )
```

Options for controlling which device OpenCL will use can be found in the
[Assembling Operators](../core/assembling_operators.md#assembling-on-different-devices)
section of the documentation of the core.

The matrix discretisation of an operator can be obtained using, for example:

```python
single.weak_form()
```

The strong form discretisation of an operator can be obtained using:
```python
single.strong_form()
```
The interpretation of the strong form is discussed in the [operator algebra](boundar_operators.md#operator-algebra)
section.

## Boundary Operators for the Helmholtz Equation

For the Helmholtz equation, there are four boundary operators that are used, as given in the table
below.

Operator             | Symbol        | Matrix entries
-------------------- | ------------- | --------------
Single layer         | $\mathsf{V}$  | $m_{ij}=\int_{\Gamma}\int_{\Gamma}G_k(\mathbf{x},\mathbf{y})\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$
Double layer         | $\mathsf{K}$  | $m_{ij}=\int_{\Gamma}\int_{\Gamma}\frac{\partial G_k(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{y}}}\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$
Adjoint double layer | $\mathsf{K}'$ | $m_{ij}=\int_{\Gamma}\int_{\Gamma}\frac{\partial G_k(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{x}}}\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$
Hypersingular        | $\mathsf{W}$  | $m_{ij}=-\int_{\Gamma}\int_{\Gamma}\frac{\partial^2 G_k(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{y}}\partial\mathbf{\nu}_{\mathbf{x}}}\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$

In each case,  $\phi_j$ and $\psi_i$ are the basis functions of the domain and dual spaces (respectively),
and $G_k(\mathbf{x},\mathbf{y})$ is the Green's function for the Helmholtz equation with
wavenumber $k$.
The Green's function will have a singularity when $\mathbf{x}=\mathbf{y}$, so internally Bempp will
use appropriate singular quadrature rules to handle this.

These operators can be initialised in Bempp using:
```python
from bempp.api.operators.boundary import helmholtz
single = helmholtz.single_layer(domain, range_, dual, wavenumber)
double = helmholtz.double_layer(domain, range_, dual, wavenumber)
adjoint_d = helmholtz.adjoint_double_layer(domain, range_, dual, wavenumber)
hypersingular = helmholtz.hypersingular(domain, range_, dual, wavenumber)
```
The spaces passed into each operator should be appropriately chosen
[scalar function spaces](function_spaces.md#scalar-function-spaces).

A keyword argument `assembler` may be passed into each constructor to change the assembler
used to assemble the operator. For example, the single layer operator will be discretised using
the fast multipole method (FMM) if it is initialised with:
```python
single = helmholtz.single_layer(
    domain, range_, dual, wavenumber, assembler="fmm")
```

When using dense assembly, the keyword argument `device_interface` can be used to switch
between assembly using OpenCL and Numba:
```python
single = helmholtz.single_layer(
    domain, range_, dual, wavenumber, assembler="dense",
    device_interface="numba"
    )
single = helmholtz.single_layer(
    domain, range_, dual, wavenumber, assembler="dense",
    device_interface="opencl"
    )
```

The matrix discretisation of an operator can be obtained using, for example:

```python
single.weak_form()
```

The strong form discretisation of an operator can be obtained using:
```python
single.strong_form()
```
The interpretation of the strong form is discussed in the [operator algebra](#operator-algebra)
section.

## Boundary Operators for the Modified Helmholtz Equation 

For the modified Helmholtz equation, there are four boundary operators that are used, as given in the table
below.

Operator             | Symbol        | Matrix entries
-------------------- | ------------- | --------------
Single layer         | $\mathsf{V}$  | $m_{ij}=\int_{\Gamma}\int_{\Gamma}G_\omega(\mathbf{x},\mathbf{y})\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$
Double layer         | $\mathsf{K}$  | $m_{ij}=\int_{\Gamma}\int_{\Gamma}\frac{\partial G_\omega(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{y}}}\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$
Adjoint double layer | $\mathsf{K}'$ | $m_{ij}=\int_{\Gamma}\int_{\Gamma}\frac{\partial G_\omega(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{x}}}\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$
Hypersingular        | $\mathsf{W}$  | $m_{ij}=-\int_{\Gamma}\int_{\Gamma}\frac{\partial^2 G_\omega(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{y}}\partial\mathbf{\nu}_{\mathbf{x}}}\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$

In each case,  $\phi_j$ and $\psi_i$ are the basis functions of the domain and dual spaces (respectively),
and $G_\omega(\mathbf{x},\mathbf{y})$ is the Green's function for the modified Helmholtz equation with
frequency $\omega$.
The Green's function will have a singularity when $\mathbf{x}=\mathbf{y}$, so internally Bempp will
use appropriate singular quadrature rules to handle this.

These operators can be initialised in Bempp using:
```python
from bempp.api.operators.boundary import modified_helmholtz
single = modified_helmholtz.single_layer(domain, range_, dual, omega)
double = modified_helmholtz.double_layer(domain, range_, dual, omega)
adjoint_d = modified_helmholtz.adjoint_double_layer(domain, range_, dual, omega)
hypersingular = modified_helmholtz.hypersingular(domain, range_, dual, omega)
```
The spaces passed into each operator should be appropriately chosen
[scalar function spaces](function_spaces.md#scalar-function-spaces).

A keyword argument `assembler` may be passed into each constructor to change the assembler
used to assemble the operator. For example, the single layer operator will be discretised using
the fast multipole method (FMM) if it is initialised with:
```python
single = modified_helmholtz.single_layer(
    domain, range_, dual, omega, assembler="fmm")
```

When using dense assembly, the keyword argument `device_interface` can be used to switch
between assembly using OpenCL and Numba:
```python
single = modified_helmholtz.single_layer(
    domain, range_, dual, wavenumber, assembler="dense",
    device_interface="numba"
    )
single = modified_helmholtz.single_layer(
    domain, range_, dual, wavenumber, assembler="dense",
    device_interface="opencl"
    )
```

The matrix discretisation of an operator can be obtained using, for example:

```python
single.weak_form()
```

The strong form discretisation of an operator can be obtained using:
```python
single.strong_form()
```
The interpretation of the strong form is discussed in the [operator algebra](#operator-algebra)
section.

## Boundary Operators for Maxwell's Equations

For Maxwell's equations, there are two boundary operators that are used, as given in the table
below.

Operator             | Symbol       | Matrix entries
-------------------- | ------------ | --------------
Electric field       | $\mathsf{E}$ | $m_{ij}=-\mathrm{i}k\int_\Gamma\int_\Gamma G_k(\mathbf{x},\mathbf{y})\mathbf{\phi}_j(\mathbf{y})\cdot\mathbf{\psi}_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}-\frac{1}{\mathrm{i}k}\int_\Gamma\int_\Gamma G_k(\mathrm{x},\mathrm{y})\nabla_\Gamma\mathbf{\phi}_j(\mathbf{y})\nabla_\Gamma\mathbf{\psi}_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x})$
Magnetic field       | $\mathsf{H}$ | $m_{ij}=-\int_\Gamma\int_\Gamma\nabla_\mathbf{x}G_k(\mathbf{x},\mathbf{y})\cdot(\mathbf{\psi}_j(\mathbf{y})\times\mathbf{\psi}_i(\mathbf{x}))\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x})$


In each case,  $\phi_j$ and $\psi_i$ are the basis functions of the domain and dual spaces (respectively),
and $G_k(\mathbf{x},\mathbf{y})$ is the Green's function for the Helmholtz equation with
wavenumber $k$.
The Green's function will have a singularity when $\mathbf{x}=\mathbf{y}$, so internally Bempp will
use appropriate singular quadrature rules to handle this.

These operators can be initialised in Bempp using:
```python
from bempp.api.operators.boundary import maxwell
electric = maxwell.electric_field(domain, range_, dual, wavenumber)
magnetic = maxwell.magnetic_field(domain, range_, dual, wavenumber)
```
The spaces passed into each operator should be appropriately chosen
[vector function spaces](function_spaces.md#vector-function-spaces): the domain and range spaces
should both be Hdiv spaces, while the dual space should be a Hcurl space.

A keyword argument `assembler` may be passed into each constructor to change the assembler
used to assemble the operator. For example, the electric field operator will be discretised using
the fast multipole method (FMM) if it is initialised with:
```python
electric = maxwell.electric_field(
    domain, range_, dual, wavenumber, assembler="fmm")
```

When using dense assembly, the keyword argument `device_interface` can be used to switch
between assembly using OpenCL and Numba:
```python
electric = maxwell.electric_field(
    domain, range_, dual, wavenumber, assembler="dense",
    device_interface="numba"
    )
electric = maxwell.electric_field(
    domain, range_, dual, wavenumber, assembler="dense",
    device_interface="opencl"
    )
```

The matrix discretisation of an operator can be obtained using, for example:

```python
electric.weak_form()
```

The strong form discretisation of an operator can be obtained using:
```python
electric.strong_form()
```
The interpretation of the strong form is discussed in the [operator algebra](#operator-algebra)
section. For Maxwell's equations, care must be taken to use space for the range and dual spaces
that form a stable dual pairing (see the [vector function spaces](function_spaces.md#vector-function-spaces)
section) in order to be able to correctly obtain the strong form of an operator.

## Operator Algebra

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
