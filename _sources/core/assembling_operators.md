---
title: Assembling Operators
layout: handbook
children:
  - core/assembling_opencl.md
  - core/assembling_numba.md
  - core/assembling_fmm.md
---
The functionality in `bempp.core` is almost exclusively for operator assembly and the multiplication
of discrete operators and vectors, as these is the most computationally-heavy components of BEM.

Bempp uses just-in-time compiled [OpenCL](assembling_opencl.md) or [Numba](assembling_numba.md)
kernels to quickly assemble the dense matrices that arise from discretising BEM operators.

For larger problems, however, the use of dense matrices is expensive, both in terms of computation
time and storage space. For such problems, Bempp can use the [fast multipole method](assembling_fmm.md)
to speed up matrix assembly and the computation of matrix-vector products. This is done via
interfaces to the external [ExaFMM](https://github.com/exafmm/exafmm-t) library.
