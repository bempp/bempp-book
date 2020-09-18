# Defining a function space


The function `function_space` is used to initialise spaces. To define
a space of piecewise constant functions we use the command:

```python
space = bempp.api.function_space(grid, "DP", 0)
```

The parameter `DP` is short for Discontinuous Polynomial. The number 0 is
the degree of the polynomial space. To define a space of continuous, piecewise
linear functions use:

```python
space = bempp.api.function_space(grid, "P", 1)
```

Bempp-cl only supports function spaces up to degree 1. This is an important
difference to earlier versions that also supported higher order spaces.

The number of degrees of freedom (DOFs) in a space can be found using:

```python
space.global_dof_count
```

For solving Laplace or Helmholtz problems, [scalar function spaces](scalar_function_spaces.md)
should be used.
For solving Maxwell's equations, [vector function spaces](./vector_function_spaces.md)
should be used.
