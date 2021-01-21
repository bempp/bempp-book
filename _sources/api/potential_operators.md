# Potential Operators

Once the solution of a boundary integral formulation has been approximated, potential
operators can be used to compute point evaluations of the solution inside the domain.

Full documentation of Bempp potential operators can be found on [Read the Docs](https://bempp-cl.readthedocs.io/en/latest/docs/bempp/api/operators/potential/index.html).

## Potential Operators for Laplace's Equation

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

As with [boundary operators](boundary_operators.md#boundary-operators-for-laplaces-equation), `assembler` and `device_interface`
keyword arguments can be used to control the assembly type used for potential operators.

## Potential Operators for the Helmholtz Equation

For the Helmholtz equation, there are two potential operators that are used, as given in the table
below.

Operator             | Definition
-------------------- | ----------
Single layer         | $(\mathcal{V}\mu)(\mathbf{x}) := \int_{\Gamma} G_k(\mathbf{x},\mathbf{y}) \mu(\mathbf{y})\,\mathrm{d}\mathbf{y}$
Double layer         | $(\mathcal{K}v)(\mathbf{x}) := \int_{\Gamma} \frac{\partial G_k(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{y}}} v(\mathbf{y})\,\mathrm{d}\mathbf{y}$

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
from bempp.api.operators.potential import helmholtz
single = helmholtz.single_layer(domain, points, wavenumber)
double = helmholtz.double_layer(domain, points, wavenumber)
```

These can be applied to a grid function with:
```python
single.evaluate(solution)
double.evaluate(solution)
```

As with [boundary operators](boundary_operators.md#boundary-operators-for-the-helmholtz-equation), `assembler` and `device_interface`
keyword arguments can be used to control the assembly type used for potential operators.

## Potential Operators for the modified Helmholtz Equation

For the modified Helmholtz equation, there are two potential operators that are used, as given in the table
below.

Operator             | Definition
-------------------- | ----------
Single layer         | $(\mathcal{V}\mu)(\mathbf{x}) := \int_{\Gamma} G_\omega(\mathbf{x},\mathbf{y}) \mu(\mathbf{y})\,\mathrm{d}\mathbf{y}$
Double layer         | $(\mathcal{K}v)(\mathbf{x}) := \int_{\Gamma} \frac{\partial G_\omega(\mathbf{x},\mathbf{y})}{\partial\mathbf{\nu}_{\mathbf{y}}} v(\mathbf{y})\,\mathrm{d}\mathbf{y}$

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

As with [boundary operators](boundary_operators.md#boundary-operators-for-the-modified-helmholtz-equation), `assembler` and `device_interface`
keyword arguments can be used to control the assembly type used for potential operators.

## Potential Operators for Maxwell's Equations

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

As with [boundary operators](boundary_operators.md#boundary-operators-for-maxwells-equations), `assembler` and `device_interface`
keyword arguments can be used to control the assembly type used for potential operators.
