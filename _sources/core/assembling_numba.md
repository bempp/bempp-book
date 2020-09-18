Assembling Operators using Numba
================================

On some systems (for example recents versions of MacOS), OpenCL is not available or has some features
unavailable. If this is the case, Bempp can use [Numba]()
to just-in-time compile operator assembly routines.

Bempp's Numba kernels are defined in the file [`bempp/core/numba_kernels.py`]().
