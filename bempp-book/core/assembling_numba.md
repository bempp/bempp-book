Assembling Operators using Numba
================================

On some systems (for example recents versions of MacOS), OpenCL is not available or has some features
unavailable. If this is the case, Bempp can use [Numba](https://numba.pydata.org/)
to just-in-time compile operator assembly routines.

Bempp's Numba kernels are defined in the file [`bempp/core/numba_kernels.py`](https://github.com/bempp/bempp-cl/blob/master/bempp/core/numba_kernels.py).
