# Vector Function Spaces


The following vector-valued spaces are supported in Bempp:

Space Type | Order | Description
---------- | ----- | -----------
`"RWG"`    | 0     | Rao--Wilson--Glisson Hdiv functions
`"SNC"`    | 0     | Scaled N&eacute;d&eacute;lec Hcurl functions
`"BC"`     | 0     | Buffa--Christiansen Hdiv functions
`"RBC"`    | 0     | Rotated Buffa--Christiansen Hcurl functions

When solving Maxwell's equations, the correct combination of Hdiv and Hcurl spaces must be used.

## RWG and SNC spaces
RWG and SNC spaces are vector-valued spaces, whose values are tangential to the surface triangles.
Inside each cell, these spaces are linear combinations of the vectors
$\left(\begin{array}{c}1\\0\end{array}\right)$,
$\left(\begin{array}{c}0\\1\end{array}\right)$, and
$\left(\begin{array}{c}-y\\x\end{array}\right)$. Between cells, RWG functions are continuous normal
to the triangle's edges, while SNC spaces are continuous tangential to the triangle's edges.
Example RWG (left) and SNC (right) basis functions are shown below.

![An RWG and a SNC basis function](../img/rwg_and_snc.png){: .smaller }

These spaces can be created in Bempp with:

```python
rwg_space = bempp.api.function_space(grid, "RWG", 0)
snc_space = bempp.api.function_space(grid, "SNC", 0)
```

The DOFs of RWG and SNC spaces are at the midpoints of the edges of each cell.

## Barycentric dual spaces
Like the scalar DUAL spaces, BC and RBC spaces are defined on the barycentrically refined grid.
This grid is formed by joining
each vertex of every triangle with the centre of the opposite side, as shown below.
![Barycentrically refining a grid](../img/barycentric_mesh.png){: .smaller }

BC and RBC spaces are combinations of RWG and SNC (repectively) spaces on the barycentric grid,
and are defined in
[<em>A dual finite element complex on the barycentric refinement</em> (2007) by A. Buffa and S. Christiansen](https://www.jstor.org/stable/40234460?seq=1).
Example BC (left) and RBC (right) basis functions are shown below.

![Dual order 0 basis function](../img/bc_and_rbc.png){: .smaller }

These spaces can be created in Bempp with:

```python
bc_space = bempp.api.function_space(grid, "BC", 0)
rbc_space = bempp.api.function_space(grid, "RBC", 0)
```

The DOFs of BC and RBC spaces are at the midpoints of the edges of each cell (or equivalently at
a point on the edges of the barycentric dual cells).

