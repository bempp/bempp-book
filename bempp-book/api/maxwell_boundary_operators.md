Boundary Operators for Maxwell's Equations
==========================================

For Maxwell's equations, there are two boundary operators that are used, as given in the table
below.

-------------------- | ------------ | --------------
Operator             | Symbol       | Matrix entries
-------------------- | ------------ | --------------
Electric field       | $\mathsf{E}$ | $m_{ij}=-\mathrm{i}k\int_\Gamma\int_\Gamma G_k(\mathbf{x},\mathbf{y})\mathbf{\phi}_j(\mathbf{y})\cdot\mathbf{\psi}_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x}-\frac{1}{\mathrm{i}k}\int_\Gamma\int_\Gamma G_k(\mathrm{x},\mathrm{y})\nabla_\Gamma\mathbf{\phi}_j(\mathbf{y})\nabla_\Gamma\mathbf{\psi}_i(\mathbf{x})\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x})$
Magnetic field       | $\mathsf{H}$ | $m\_{ij}=-\int_\Gamma\int_\Gamma\nabla_\mathbf{x}G_k(\mathbf{x},\mathbf{y})\cdot(\mathbf{\psi}_j(\mathbf{y})\times\mathbf{\psi}_i(\mathbf{x}))\,\mathrm{d}\mathbf{y}\,\mathrm{d}\mathbf{x})$
-------------------- | ------------ | --------------


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
[vector function spaces](vector_function_spaces.md): the domain and range spaces
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
The interpretation of the strong form is discussed in the [operator algebra](operator_algebra.md)
section. For Maxwell's equations, care must be taken to use space for the range and dual spaces
that form a stable dual pairing (see the [vector function spaces](vector_function_spaces.md)
section) in order to be able to correctly obtain the strong form of an operator.
