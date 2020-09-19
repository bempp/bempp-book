Potential Operators for Laplace's Equation
==========================================

For Laplace's equation, there are two potential operators that are used, as given in the table
below.

Operator             | Definition
-------------------- | ----------
Single layer         | $(\mathcal{V}\mu)(\mathbf{x}) := \int_{\Gamma} G(\mathbf{x},\mathbf{y}) \mu(\mathbf{y})\,\mathrm{d}\mathbf{y}$
Double layer         | $(\mathcal{K}v)(\mathbf{x}) := \int_{\Gamma} \frac{\partial G(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{y}}} v(\mathbf{y})\,\mathrm{d}\mathbf{y}$

In each case, $G(\mathbf{x},\mathbf{y})$ is the Green's function for Laplace's equation.

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
from bempp.api.operators.potential import laplace
single = laplace.single_layer(domain, points)
double = laplace.double_layer(domain, points)
```

These can be applied to a grid function with:
```python
single.evaluate(solution)
double.evaluate(solution)
```

As with [boundary operators](laplace_boundary_operators.md), `assembler` and `device_interface`
keyword arguments can be used to control the assembly type used for potential operators.
