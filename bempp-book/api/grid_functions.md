Grid Functions
==============

In Bempp, data on a given grid is represented as a grid function object.
A grid function consists of a set of basis function coefficients and a corresponding [function space](function_spaces.md).


## Initialising with a Python callable
Grid functions can be created from Python callables.

```python
@bempp.api.complex_callable
def fun(x, normal, domain_index, result):
    result[0] = np.exp(1j * x[0])
```

The first argument `x` is the coordinates of an evaluation point.
The second argument `normal` is the normal direction at the evaluation point.
The third one is the `domain_index`: this corresponds to the physical id in Gmsh and can be used to assign different boundary data to different parts of the grid.
The last argument `result` is the variable that stores the value of the callable.
It is a Numpy array with as many components as the basis functions of the underlying space have.

A Python callable that you want to use to build a grid function should always have these four inputs.
An optional fifth input may be used to pass parameters into the function.

In order for Bempp to assemble a grid function with coefficients of the correct data type,
these callables must be decorated with either `@bempp.api.real_callable` or
`@bempp.api.real_callable`.

The projection of this callable into a Bempp space can be created with:
```python
grid_fun = bempp.api.GridFunction(space, fun=fun)
```

### Disabling just-in-time compilation
By default, Bempp with use Numba just-in-time compilation when creating grid functions from callables.
In some cases, this compilation is not possible and should be disabled. This can be
done by passing `jit=False` into the decorator:

```python
@bempp.api.complex_callable(jit=False)
def fun(x, normal, domain_index, result):
    result[0] = np.exp(1j * x[0])

grid_fun = bempp.api.GridFunction(space, fun=fun)
```

The construction of this grid function will be slower as it is not sped up by Numba.

## Initialising with coefficients or projections
Instead of a callable, we can initialise a grid function from a vector of
coefficients or a vector of projections.
This can be done as follows.

```python
c = np.array([...])  # These are the coefficients
grid_fun = GridFunction(space, coefficients=c)

p = np.array([...])  # These are the projections
grid_fun = GridFunction(space, projections=p, dual_space=dual)
```

The argument `dual_space` gives the space with which the projection coefficients were computed.
The parameter is optional and if it is not given then `space == dual_space` is assumed.

## Coefficients and projections
The functions in a discrete function space are represented as a linear combination of some basis
functions. The coefficients of a grid function are the scalars which each basis function
is multiplied by in this combination. The coefficients of a grid function can be obtained using:

```python
grid_fun.coefficients
```

The projections of a grid function are calculated by applying a discrete mass matrix to the
coefficients. The mass matrix will be between the grid function's space and a dual space
provided to the `projections` call. These can be obtained using:

```python
grid_fun.projections(dual_space)
```

In some situations, for example when the space and the dual are RWG and SNC spaces, the mass matrix
for projections may be numerically singular. In these cases, the coefficients of a grid function
that has been initialised using projections cannot be accurately calculated. Bempp, however, can
still use these grid functions by only querying the projections.

## Plotting and exporting grid functions
To export a grid function, we can use the `export` command:

```python
bempp.api.export('grid_function.msh', grid_function=grid_fun)
```

This commands export the object `grid_fun` as Gmsh file with the
name `grid_function.msh`.

In order to plot a grid function, we can simply use the command:

```python
grid_fun.plot()
```

By default, this will plot using Gmsh (or plotly if you are inside a Jupyter notebook).
The following command can be used to change the plotting backend.

```python
bempp.api.PLOT_BACKEND = "gmsh"
bempp.api.PLOT_BACKEND = "paraview"
```

This requires Gmsh or Paraview to be available in the system path.
