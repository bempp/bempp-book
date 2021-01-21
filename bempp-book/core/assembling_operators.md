# Assembling Operators
The functionality in `bempp.core` is almost exclusively for operator assembly and the multiplication
of discrete operators and vectors, as these is the most computationally-heavy components of BEM.

Bempp uses just-in-time compiled [OpenCL](#assembling-operators-using-opencl) or
[Numba](#assembling-operators-using-numba)
kernels to quickly assemble the dense matrices that arise from discretising BEM operators.

For larger problems, however, the use of dense matrices is expensive, both in terms of computation
time and storage space. For such problems, Bempp can use the [fast multipole method](#assembling-operators-using-fmm)
to speed up matrix assembly and the computation of matrix-vector products. This is done via
interfaces to the external [ExaFMM](https://github.com/exafmm/exafmm-t) library.

## Assembling Operators using Numba
On some systems (for example recents versions of MacOS), OpenCL is not available or has some features
unavailable. If this is the case, Bempp can use [Numba](https://numba.pydata.org/)
to just-in-time compile operator assembly routines.

Bempp's Numba kernels are defined in the file [`bempp/core/numba_kernels.py`](https://github.com/bempp/bempp-cl/blob/master/bempp/core/numba_kernels.py).
Bempp can use Numba
to just-in-time compile operator assembly routines.

## Assembling Operators using OpenCL
OpenCL is a C-based compute language designed to allow a single script to be parallelised on
a wide range of CPU and GPU devices. Bempp uses [PyOpenCL](https://documen.tician.de/pyopencl/)
to just-in-time compile its OpenCL kernels when they are needed.

Bempp's OpenCL kernels are stored in the folder [`bempp/core/sources/kernels`](https://github.com/bempp/bempp-cl/tree/master/bempp/core/sources/kernels).

## Assembling Operators using FMM
For larger problems, dense assembly using OpenCL or Numba become very expensive, both in terms of
computation time and memory consumption. In such cases, Bempp can use the fast multipole method (FMM)
to speed up its calculations and reduce memory usage.

Internally, Bempp uses the [ExaFMM](https://github.com/exafmm/exatmm-t) library to carry out its FMM computations.
