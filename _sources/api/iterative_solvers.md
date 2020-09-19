Iterative Solvers
=================

Iterative solvers solve a linear system iteratively: steps are repeated to achieve better
approximations of the solution. For well-condtioned matrices, iterative solvers can achieve
fast convergence, so very good approximations of the solution can be achieved in just a few
iterations.

SciPy's CG and GMRes iterative solvers are wrapped in the `bempp.api.linalg` submodule. These
can be used with:

```python
solution, info = bempp.api.linalg.cg(operator, grid_fun)
solution, info = bempp.api.linalg.gmres(opreator, grid_fun)
```

These solvers take a number of optional arguments:

Argument                 | Description                                                                                 | Default
------------------------ | ------------------------------------------------------------------------------------------- | ----------
`tol`                    | The tolerance the solver should aim for                                                     | `1e-5`
`maxiter`                | The maximum number of iterations                                                            | No maximum
`use_strong_form`        | If `True`, the strong form of the operator will be used. If `False`, the weak form is used. | `False`
`return_residuals`       | If `True` the residuals will be returned as well as the solution and info                   | `False`
`return_iteration_count` | If `True` the iteration count will be returned as well as the solution and info             | `False`

By default, Bempp will use the weak form discretisation of the operator and the coefficients
of the grid function when using an iterative solver.
If `use_strong_form` is set to `True`, Bempp will use the strong form discretisation of the operator
and the projections of the grid function onto the range of the operator. This is equivalent
to applying a mass matrix preconditioner to the problem and often leads to a lower iteration count.
