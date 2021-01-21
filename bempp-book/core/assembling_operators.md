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

Full documentation of the functionality of Bempp grids can be found on
[Read the Docs](https://bempp-cl.readthedocs.io/en/latest/docs/bempp/core/).

## Assembly options
The type of assembly used by Bempp can be controlled by passing a `device_interface` keyword
argument into an operator. The possible values that can be passed in are `"opencl"`,
`"numba"`. FMM can be used by passing `assembler="fmm"` into an operator. Examples of how this can
be done are given in the [boundary operators](../api/boundary_operators.md) section of the API
Overview.

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

### Assembling on different devices
OpenCL can be used to assemble operators on a wide range of GPU and CPU devices. You can view
your available devices by running:

```python
from bempp.core import opencl_kernels
opencl_kernels.show_available_platforms_and_devices()
```

Each available device will be displayed alongside their platform and device indices. These
indices can be used to set the default device. For example, the following snippet will set the
default device to be the 0th device on platform 1:

```python
opencl_kernels.set_default_device(1, 0)
```

The default device can be viewed by running:
```python
print(opencl_kernels.default_device())
```

## Assembling Operators using FMM
For larger problems, dense assembly using OpenCL or Numba become very expensive, both in terms of
computation time and memory consumption. In such cases, Bempp can use the fast multipole method (FMM)
to speed up its calculations and reduce memory usage.

Internally, Bempp uses the [ExaFMM](https://github.com/exafmm/exatmm-t) library to carry out its FMM computations.
