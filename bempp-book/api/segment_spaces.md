Function Spaces on Segments
===========================

Bempp can create spaces on segments of a grid as well as on the entire grid.
In order to do this, domain indices must be provided when [creating the grid](creating_grids.md).
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

## Controlling segment spaces
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
