Degrees of Freedom (DOFs)
=========================

An abstract finite element is defined by:

- A reference element $R\subset\mathbb{R}^d$. In Bempp, $R$ is always a triangle with vertices at
  $(0,0)$, $(1,0)$ and $(0,1)$.
- A finite dimensional polynomial space $\mathcal{V}$. Inside each triangle in the mesh, the solution
  will be approximated by a function in this space.
- A set of functionals $\mathcal{L}={f_1, ... f_n}$ that form a basis of the dual space
  $\mathcal{V}^*=\{f:\mathcal{V}\to\mathbb{R}\}$.

Given a functional $f_i\in\mathcal{L}$, a corresponding polynomial basis function
$\phi_i\in\mathcal{V}$ is defined as the function such that

$$
f_j(\phi_i)=\begin{cases}1&i=j\\0&i\not=j\end{cases}.
$$

## Example: P1 space
As an example, for a P1 (continuous piecewise linear space) the following are used:

- $R$ is the reference triangle.
- $\mathcal{V}=\operatorname{span}\{1, x, y\}$.
- $\mathcal{L}$ is the set of point evaluations at the vertices of $R$.

In this case, it is common to say that the space has a DOF at each vertex of the mesh.

## Spaces used by Bempp
The definitions of the spaces available in Bempp are summarised in the following table.
In each case, $R$ is the unit triangle.

----- | ------------- | -------------
Space | $\mathcal{V}$ | $\mathcal{L}$
----- | ------------- | -------------
DP0   | $\operatorname{span}\{1\}$ | Point evaluation at centre of $R$
P1    | $\operatorname{span}\{1, x, y\}$ | point evaluations at vertices of $R$
RWG1  | $\operatorname{span}\left\{\left(\begin{array}{c}1\\0\end{array}\right),\left(\begin{array}{c}0\\1\end{array}\right),\left(\begin{array}{c}x\\y\end{array}\right)\right\}$ | Point evaluations at the midpoints of edges of $R$ in a direction normal to the edge
SNC1  | $\operatorname{span}\left\{\left(\begin{array}{c}1\\0\end{array}\right),\left(\begin{array}{c}0\\1\end{array}\right),\left(\begin{array}{c}y\\-x\end{array}\right)\right\}$ | Point evaluations at the midpoints of edges of $R$ in a direction tangential to the edge
----- | ------------- | -------------

The spaces defined on the barycentric dual grid are defined as subspaces of the spaces
in the table above. Their definitions can be found in
[<em>A dual finite element complex on the barycentric refinement</em> (2007) by A. Buffa and S. Christiansen](https://www.jstor.org/stable/40234460?seq=1).
