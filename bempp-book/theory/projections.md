Interpolation and Projection
============================


We now take a closer look at what happens in the initialisation of this GridFunction.
Denote the global basis functions of the space by $\psi_j$, for $j=1,\dots,N$.
The computation of the grid function consists of two steps:

+ Compute the projection coefficients
  $p_j=\int_{\Gamma}\overline{\psi_j(\mathbf{y})}f(\mathbf{y})\mathrm{d}\mathbf{y}$,
  where $f$ is the analytic function to be converted into a grid function and $\Gamma$
  is the surface defined by the grid.
+ Compute the basis coefficients $c_j$ from $Mc=p$, where $M$ is the mass matrix defined by
  $M_{ij}=\int_{\Gamma}\overline{\psi_i(\mathbf{y})}\psi_j(\mathbf{y})\mathrm{d}\mathbf{y}$.

This is an orthogonal $\mathcal{L}^2(\Gamma)$-projection onto the basis $\{\psi_1,...,\psi_N\}$.
