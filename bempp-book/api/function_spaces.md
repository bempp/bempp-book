# Function Spaces

Once we have created a grid, we can define finite-dimensional function spaces
on the grid. These spaces will then be used to discretise the boundary integral
formulations of our problem.

Full documentation of Bempp function spaces can be found on [Read the Docs](https://bempp-cl.readthedocs.io/en/latest/docs/bempp/api/space/index.html).

## Defining a function space

The function `function_space` is used to initialise spaces. To define
a space of piecewise constant functions we use the command:

```python
space = bempp.api.function_space(grid, "DP", 0)
```

The parameter `DP` is short for Discontinuous Polynomial. The number 0 is
the degree of the polynomial space. To define a space of continuous, piecewise
linear functions use:

```python
space = bempp.api.function_space(grid, "P", 1)
```

Bempp-cl only supports function spaces up to degree 1. This is an important
difference to earlier versions that also supported higher order spaces.

The number of degrees of freedom (DOFs) in a space can be found using:

```python
space.global_dof_count
```

For solving Laplace or Helmholtz problems, [scalar function spaces](#scalar-function-spaces)
should be used.
For solving Maxwell's equations, [vector function spaces](#vector-function-spaces)
should be used.

## Scalar Function Spaces

The following scalar-valued spaces are supported in Bempp:

Space Type | Order(s) | Description
---------- | -------- | -----------
`"DP"`     | 0 or 1   | Discontinuous [polynomials](https://defelement.com/elements/lagrange.html)
`"P"`      | 1        | Continuous [polynomials](https://defelement.com/elements/lagrange.html)
`"DUAL"`   | 0 or 1   | [Dual spaces](https://defelement.com/elements/dual.html) on the barycentrically refined grid

### Discontinuous polynomial spaces
DP spaces are polynomial inside each element and discontinuous between elements.
An example basis function of an order 0 DP space is shown in {numref}`dp0`.

```{figure} ../img/dp0.png
---
height: 200px
name: dp0
---
Discontinuous polynomial order 0 basis function
```

These spaces can be created in Bempp with:

```python
space = bempp.api.function_space(grid, "DP", 0)
space = bempp.api.function_space(grid, "DP", 1)
```

The DOFs of an order 0 DP space are at the midpoints of each cell.
The DOFs of an order 1 DP space are at the three vertices of each cell.

### Continuous polynomial spaces
P spaces are polynomial inside each element and continuous between elements.
An example basis function of an order 1 P space is shown in {numref}`p1`.

```{figure} ../img/p1.png
---
height: 200px
name: p1
---
Continuous polynomial order 1 basis function
```

This space can be created in Bempp with:

```python
space = bempp.api.function_space(grid, "P", 1)
```

The DOFs of an order 1 P space are at the three vertices of each cell.

### Barycentric dual spaces
To define the barycentric dual space, we first create the barycentrically refined mesh by joining
each vertex of every triangle with the centre of the opposite side, as shown in {numref}`barymesh`.

```{figure} ../img/barycentric_mesh.png
---
width: 100%
name: barymesh
---
Barycentrically refining a grid
```

The order 0 dual spaces are piecewise constant functions on the dual cells.
An example basis function of an order 0 DUAL space is shown in {numref}`dual0`.
Order 0 DUAL spaces form a stable dual pairing with order 1 P spaces.
```{figure} ../img/dual0.png
---
height: 200px
name: dual0
---
Dual order 0 basis function
```

The order 1 dual basis functions are linear combinations of piecewise linear
functions on the barycentric cells, and are defined in
[<em>A dual finite element complex on the barycentric refinement</em> (2007) by A. Buffa and S. Christiansen](https://www.jstor.org/stable/40234460?seq=1).
An example basis function of an order 1 DUAL space is shown in {numref}`dual1`.
Order 1 DUAL spaces form a stable dual pairing with order 0 DP spaces.

```{figure} ../img/dual1.png
---
height: 200px
name: dual1
---
Dual order 1 basis function
```

These spaces can be created in Bempp with:

```python
space = bempp.api.function_space(grid, "DUAL", 0)
space = bempp.api.function_space(grid, "DUAL", 1)
```

The DOFs of an order 0 DUAL space are at the three vertices of each cell
(ie the midpoints of each barycentric dual cell).
The DOFs of an order 1 DUAL space are at the mispoints of each cell
(ie the vertices of each barycentric dual cell).

## Vector Function Spaces


The following vector-valued spaces are supported in Bempp:

Space Type | Order | Description
---------- | ----- | -----------
`"RWG"`    | 0     | [Rao--Wilson--Glisson](https://defelement.com/elements/raviart-thomas.html) Hdiv functions
`"SNC"`    | 0     | [Scaled N&eacute;d&eacute;lec](https://defelement.com/elements/nedelec1.html) Hcurl functions
`"BC"`     | 0     | [Buffa--Christiansen](https://defelement.com/elements/buffa-christiansen.html) Hdiv functions
`"RBC"`    | 0     | [Rotated Buffa--Christiansen](https://defelement.com/elements/rotated-buffa-christiansen.html) Hcurl functions

When solving Maxwell's equations, the correct combination of Hdiv and Hcurl spaces must be used.

### RWG and SNC spaces
RWG and SNC spaces are vector-valued spaces, whose values are tangential to the surface triangles.
Between cells, RWG functions are continuous normal
to the triangle's edges, while SNC spaces are continuous tangential to the triangle's edges.
Example RWG (left) and SNC (right) basis functions are shown in {numref}`rwg_and_snc`.

```{figure} ../img/rwg_and_snc.png
---
height: 200px
name: rwg_and_snc
---
An RWG and a SNC basis function
```

These spaces can be created in Bempp with:

```python
rwg_space = bempp.api.function_space(grid, "RWG", 0)
snc_space = bempp.api.function_space(grid, "SNC", 0)
```

The DOFs of RWG and SNC spaces are at the midpoints of the edges of each cell.

### Barycentric dual spaces
Like the scalar DUAL spaces, BC and RBC spaces are defined on the barycentrically refined grid.
This grid is formed by joining
each vertex of every triangle with the centre of the opposite side, as shown in {numref}`barymesh`.

BC and RBC spaces are combinations of RWG and SNC (repectively) spaces on the barycentric grid,
and are defined in
[<em>A dual finite element complex on the barycentric refinement</em> (2007) by A. Buffa and S. Christiansen](https://www.jstor.org/stable/40234460?seq=1).
Example BC (left) and RBC (right) basis functions are shown in {numref}`bc_and_rbc`.

```{figure} ../img/bc_and_rbc.png
---
height: 200px
name: bc_and_rbc
---
A BC and a RBC basis function
```

These spaces can be created in Bempp with:

```python
bc_space = bempp.api.function_space(grid, "BC", 0)
rbc_space = bempp.api.function_space(grid, "RBC", 0)
```

The DOFs of BC and RBC spaces are at the midpoints of the edges of each cell (or equivalently at
a point on the edges of the barycentric dual cells).

## Function Spaces on Segments

Bempp can create spaces on segments of a grid as well as on the entire grid.
In order to do this, domain indices must be provided when [creating .md).
Some built-in grids have domain indices: for example, the cube has six segments
for the faces (numbered 1 to 6).

To create a space on a segment, first create the grid:
```python
grid = bempp.api.shapes.cube()
```

A space on segments 1 and 2 of the grid can then be created using:
```python
space = bempp.api.function_space(grid, "DP", 0, segments=[1, 2])
```

### Controlling segment spaces
There are two options that can be used to control the behaviour of a space on a segment:
`include_boundary_dofs` and `truncate_at_segment_edge`.

If `include_boundary_dofs` is set to `True`, DOF points on vertices and edges on the boundary.
By default, this is set to `False`. Setting this option to `True` is likely to make the
function space extend outside its segments, as part of the basis functions with DOFs on the
boundary will be outside the domain.

The option `truncate_at_segment_edge` can be used to truncate basis functions at the edge of the
segment, whenever a basis function will extend outside the segments. By default, this is `False`.
Setting this option to `True` will cause the function space to be discontinuous at the edge
of the segment.
