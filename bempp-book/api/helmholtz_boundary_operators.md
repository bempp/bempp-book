Boundary Operators for the Helmholtz Equation
=============================================


For the Helmholtz equation, there are four boundary operators that are used, as given in the table
below.

-------------------- | ------------- | --------------
Operator             | Symbol        | Matrix entries
-------------------- | ------------- | --------------
Single layer         | $\mathsf{V}$  | $m_{ij}=\int_{\Gamma}\int_{\Gamma}G_k(\mathbf{x},\mathbf{y})\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$
Double layer         | $\mathsf{K}$  | $m_{ij}=\int_{\Gamma}\int_{\Gamma}\frac{\partial G_k(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{y}}}\phi\_j(\mathbf{y})\psi\_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$
Adjoint double layer | $\mathsf{K}'$ | $m\_{ij}=\int_{\Gamma}\int_{\Gamma}\frac{\partial G_k(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{x}}}\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$
Hypersingular        | $\mathsf{W}$  | $m\_{ij}=-\int_{\Gamma}\int_{\Gamma}\frac{\partial^2 G_k(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{y}}\partial\mathbf{\nu}_{\mathbf{x}}}\phi_j(\mathbf{y})\psi_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}$
-------------------- | ------------- | --------------

In each case,  $\phi\_j$ and $\psi\_i$ are the basis functions of the domain and dual spaces (respectively),
and $G\_k(\mathbf{x},\mathbf{y})$ is the Green's function for the Helmholtz equation with
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
[scalar function spaces](scalar_function_spaces.md).

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
The interpretation of the strong form is discussed in the [operator algebra](operator_algebra.md)
section.
