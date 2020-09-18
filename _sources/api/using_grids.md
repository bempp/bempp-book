# Using Grids

Once you have created a Bempp grid, you may want to use information about your grid.
This page show how commonly used information can be obtained from a Bempp grid.

## Querying grid information

The number of elements, edges and vertices in a grid are given by:

```python
grid.number_of_elements
grid.number_of_edges
grid.number_of_vertices
```

To query the maximum and minimum element diameter use the following attributes:

```python
grid.maximum_element_diameter
grid.minimum_element_diameter
```

The vertex indices of the element 5 can be obtained using:

```python
grid.elements[:, 5]
```

Note that the numbering of element starts at 0, so element 5 is the grid's sixth element.

The vertex coordinates of element 5 can be found using:

```python
grid.vertices[:, grid.elements[:, 5]]
```

The area of the element 5 is:

```python
grid.volumes[5]
```

The edge indices associated with element 5 are:

```python
grid.element_edges[5]
```

The vertex indices of the edges of element 5 can be obtained using:

```python
grid.edges[:, grid.element_edges[:, 5]]
```

This returns a 2&times;3 array of the vertex coordinates associated
with the three edges of the element.
Edges in Bempp are ordered in the following way:

---- | ------------ | -------------
Edge | First vertex | Second vertex
---- | ------------ | -------------
 0   |  0           |  1
 1   |  0           |  2
 2   |  1           |  2
---- | ------------ | -------------

Full automatically-generated documentation of the Bempp `Grid` class can be found
[here](https://bempp-cl.readthedocs.io/en/latest/docs/bempp/api/grid/grid/index.html#bempp.api.grid.grid.Grid).

## Plotting and exporting grids
To export a grid, we can use the `export` command:

```python
bempp.api.export('grid.msh', grid=grid)
```

This commands export the object `grid` as Gmsh file with the
name `grid.msh`.

In order to plot a grid, we can simply use the command:

```python
grid.plot()
```

By default, this will plot using Gmsh (or plotly if you are inside a Jupyter notebook).
The following command can be used to change the plotting backend.

```python
bempp.api.PLOT_BACKEND = "gmsh"
bempp.api.PLOT_BACKEND = "paraview"
```

This requires Gmsh or Paraview to be available in the system path.
