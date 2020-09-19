Potential Operators for Maxwell's Equations
===========================================

For Maxwell's equations, there are two potential operators that are used, as given in the table
below.

Operator       | Definition
-------------- | ----------
Electric field | $(\mathcal{E}(\mathbf{p}))(\mathbf{x})=\mathrm{i} k\int_\Gamma\mathbf{p}(\mathbf{y})G_k(\mathbf{x},\mathbf{y})\,\mathrm{d}\mathbf{y}-\frac1{\mathrm{i} k}\nabla_{\mathbf{x}}\int_\Gamma\nabla_{\Gamma}\cdot\mathbf{p}(\mathbf{y})G_k(\mathbf{x},\mathbf{y})\,\mathrm{d}\mathbf{y}$
Magnetic field | $(\mathcal{H}(\mathbf{p})(\mathbf{x})=\nabla_\mathbf{x}\times\int_\Gamma\mathbf{p}(\mathbf{y})G(\mathbf{x},\mathbf{y})\,\mathrm{d}\mathbf{y}$

In each case, $G_k(\mathbf{x},\mathbf{y})$ is the Green's function for the Helmholtz equation
with wavenumber $k$.

To assemble potential operators in Bempp, the desired evaluation points must first be defined.
For example, the following snippet creates a grid of 2500 points in the $x$$y$-plane with
$x$ and $y$ between -3 and 3.

```python
plot_grid = np.mgrid[-3:3:50j, -3:3:50j]
points = np.vstack((plot_grid[0].ravel(),
                    plot_grid[1].ravel(),
                    np.zeros(plot_grid[0].size)))
```

Potential operators can thenbe initialised in Bempp using:
```python
from bempp.api.operators.potential import maxwell
electric = maxwell.electric_feild(domain, points, wavenumber)
magnetic = maxwell.magnetic_feild(domain, points, wavenumber)
```

These can be applied to a grid function with:
```python
electric.evaluate(solution)
magnetic.evaluate(solution)
```

As with [boundary operators](maxwell_boundary_operators.md), `assembler` and `device_interface`
keyword arguments can be used to control the assembly type used for potential operators.

