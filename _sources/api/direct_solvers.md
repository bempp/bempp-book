Direct Solvers
==============

Direct solvers compute the solution of a linear system by (usually indirectly) computing the
inverse of the matrix.

SciPy's direct LU solver is wrapped in the function `bempp.api.linalg.lu`. This can be used with:
```python
solution = bempp.api.linalg.lu(operator, grid_fun)
```

Direct solvers should only be used if the operator has been assembled in dense mode.
