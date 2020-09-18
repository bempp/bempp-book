Assembling Operators using FMM
==============================

For larger problems, dense assembly using OpenCL or Numba become very expensive, both in terms of
computation time and memory consumption. In such cases, Bempp can use the fast multipole method (FMM)
to speed up its calculations and reduce memory usage.

Internally, Bempp uses the [ExaFMM]() library to carry out its FMM computations.
