Assembling Operators using OpenCL
=================================

OpenCL is a C-based compute language designed to allow a single script to be parallelised on
a wide range of CPU and GPU devices. Bempp uses [PyOpenCL]()
to just-in-time compile its OpenCL kernels when they are needed.

Bempp's OpenCL kernels are stored in the folder [`bempp/core/sources/kernels`]().
