Assembling Operators using OpenCL
=================================

OpenCL is a C-based compute language designed to allow a single script to be parallelised on
a wide range of CPU and GPU devices. Bempp uses [PyOpenCL](https://documen.tician.de/pyopencl/)
to just-in-time compile its OpenCL kernels when they are needed.

Bempp's OpenCL kernels are stored in the folder [`bempp/core/sources/kernels`](https://github.com/bempp/bempp-cl/tree/master/bempp/core/sources/kernels).
