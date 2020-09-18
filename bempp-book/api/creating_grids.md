# Overview

A Bempp grid can be created using a built-in grid, by importing a gmsh file,
or by providing the grid data.

We first import Bempp and NumPy.

```python
import bempp.api
import numpy as np
```

## Built-in grids
Various shapes are included in the `bempp.api.shapes` module, and discretisations with
different numbers of elements can be created using these.
In order for the these built-in grids to work, Gmsh must be
installed and the command `gmsh` must be available in the path.

The command `regular_sphere` creates a sphere by refining a
base octahedron. The number of elements in the sphere is given by
$8 \times 4^n$, where $n$ is the refinement level.
The following command creates a triangulation of a sphere with refinement level 3:

```python
grid = bempp.api.shapes.regular_sphere(3)
```

The command `sphere` creates a sphere with a chosen element size.
The following command creates a sphere with element diameter $h=0.1$:

```python
grid = bempp.api.shapes.sphere(h=0.1)
```

The command `cube` creates a cube with a chosen element size.
The following command creates a cube with element diameter $h=0.3$:

```python
grid = bempp.api.shapes.cube(h=0.3)
```

Full automatically-generated documentation of Bempp's available built-in grids can be found
[here](https://bempp-cl.readthedocs.io/en/latest/docs/bempp/api/shapes/index.html).

## Importing a grid
Grids can be importedusing Bempp's `import_grid` command.
For example, the following command will load a grid from the Gmsh file `my_grid.msh`.

```python
grid = bempp.api.import_grid('my_grid.msh')
```

Bempp uses the file ending to recognise a number of grid formats.
Importing grids is handled by the [meshio](https://github.com/nschloe/meshio) library.
    
This works through the external `meshio` library.
A list of all files types that can be imported can be found in the meshio documentation.
Frequently used formats with Bempp are `.msh` (Gmsh),
`.vtk` (Legacy VTK), and `.vtu` (VTK Xml Format).

## Creating a grid from element data
Bempp grids can be generated from arrays containing vertex coordinates and
connectivity information. For example, to create a grid consisting of two
triangles with vertices $\\{(0, 0, 0), (1, 0, 0), (0, 1, 0)\\}$ and
$\\{(1, 0, 0), (1, 1, 0), (0, 1, 0)\\}$ we use the following commands:

```python
vertices = np.array(
    [[0, 1, 0, 1], [0, 0, 1, 1], [0, 0, 0, 0]],
    dtype=np.float64)
elements = np.array(
    [[0, 1], [1, 3], [2, 2]], dtype=np.uint32)
grid = bempp.api.Grid(vertices, elements)
```

Note that the three arrays in the `vertices` array are the $x$-coordinates,
then the $y$-coordinates, then the $z$-coordinates.
Similarly, the three arrays in the `elements` array are the first points of each triangle,
then the second points, then the third points.
In general, the `vertices` and `elements` arrays should have shapes $3\times M$ and $3\times N$
(respectively) for a grid with $M$ vertices and $N$ elements.

The array `vertices` contains the 3D coordinates of all vertices. The array
`elements` contains the connectivity information. In this case the first
triangle consists of the vertices 0, 1, 2, and the second triangle consists
of the vertices 1, 3, 2.

Optionally, we can specify a list `domain_indices`
that gives different groups of elements the same id. This can be used
for example to generate different types of boundary data on different parts
of the grid, or to specify function spaces only on parts of the grid. In this
example, both triangles automatically have the identifier 0 since nothing
else was specified. This is equivalent to running:

```python
grid = bempp.api.Grid(vertices, elements, domain_indices=[0, 0])
```
