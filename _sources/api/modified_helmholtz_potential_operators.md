Potential Operators for the modified Helmholtz Equation
=======================================================

For the modified Helmholtz equation, there are two potential operators that are used, as given in the table
below.

-------------------- | ----------
Operator             | Definition
-------------------- | ----------
Single layer         | (\mathcal{V}\mu)(\mathbf{x}) := \int_{\Gamma} G_\omega(\mathbf{x},\mathbf{y}) \mu(\mathbf{y})\,\mathrm{d}\mathbf{y}$
Double layer         | $(\mathcal{K}v)(\mathbf{x}) := \int_{\Gamma} \frac{\partial G_\omega(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{y}}} v(\mathbf{y})\,\mathrm{d}\mathbf{y}$
-------------------- | ----------


In each case, $G_\omega(\mathbf{x},\mathbf{y})$ is the Green's function for the modified Helmholtz equation
with frequency $\omega$.

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
from bempp.api.operators.potential import modified_helmholtz
single = modified_helmholtz.single_layer(domain, points, omega)
double = modified_helmholtz.double_layer(domain, points, omega)
```

These can be applied to a grid function with:
```python
single.evaluate(solution)
double.evaluate(solution)
```

As with [boundary operators](modified_helmholtz_boundary_operators.md), `assembler` and `device_interface`
keyword arguments can be used to control the assembly type used for potential operators.
