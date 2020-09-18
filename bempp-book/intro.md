Introduction
============

The boundary element method (BEM) is a numerical method for approximating the solution of partial differential equations (PDEs).
The method finds the approximation by discretising a boundary integral equation that can be derived from the PDE.

Bempp is an open-source boundary element method library that can be used to assemble all the standard integral kernels for
Laplace, Helmholtz, modified Helmholtz, and Maxwell problems. The library has a user-friendly Python interface that allows the
user to use BEM to solve a variety of problems, including problems in electrostatics, acoustics and electromagnetics.

Bempp began life as BEM++, and was a Python library with a fast C++ computational core. The ++ slowly changed to a pp as
functionality gradually moved from C++ to Python. The latest version, `bempp-cl`, is a complete rewrite of the library, with
the C++ core replaced by just-in-time compiled OpenCL kernels, and has many improvements over past versions of the library.

Bempp is divided into two parts: `bempp.api` and `bempp.core`.
The user interface of the library is contained in `bempp.api`.
The core assembly routines of the library are contained in `bempp.core`. The majority of users of Bempp are unlikely to need
to directly interact with the functionality in `bempp.core`.

In this handbook, we introduce and demonstrate the functionality of Bempp. The handbook is split into three parts.
First, we present a guide to using Bempp. This part of the handbook takes the reader
through all the major functionality contained in the `bempp.api` user interface.

In the second part of the handbook, we take a journey into the Bempp core where we look in more detail
at the internal behaviour of the Bempp assemblers

For the final part of the handbook, we present a Bempp user's introduction to boundary element methods.
This part of the handbook aims the introduce the mathematics underlying BEM and highlight important aspects of the
theory that should be taken into account when deciding how to approach BEM problems.

This handbook is hosted on [GitHub](https://github.com/bempp/bempp-handbook) and we welcome suggestions for improving it
in the issues and pull requests.
