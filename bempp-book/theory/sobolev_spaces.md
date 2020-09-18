Sobolev Spaces
==============

This section of the Bempp Handbook introduces the Sobolev function spaces in which the solutions
to the variational boundary integral equation are sought.

Let $\Omega^-\subset\mathbb{R}^3$ be a bounded domain and let $\Gamma$
be the boundary of $\Omega^-$. Let $\Omega^+=\mathbb{R}^3\setminus\Omega^-$ be the region exterior
to $\Omega^-$.

## Scalar function spaces
For Laplace and Helmholtz problems, we use spaces containing scalar functions
$f:\Omega^-\to\mathbb{C}$.
We begin by defining the space of square integrable functions:

$$
H^0(\Omega^-):=L^2(\Omega^-):=\left\{v:\Omega^-\to\mathbb{C}\middle|\int_{\Omega^-} |v|^2<\infty\right\}
$$

We then define the Sobolev space $H^1(\Omega^-)$ to be the space of square integrable functions
whose first derivatives are also square integrable.

$$
H^1(\Omega^-):=\left\{v\in L^2(\Omega^-)\middle|\frac{\partial v}{\partial x}, \frac{\partial v}{\partial y}, \frac{\partial v}{\partial z}\in L^2(\Omega)\right\}
$$

In general, for each positive integer $k$, we define the space $H^k(\Omega^-)$ to be the space
of square integrable functions whose derivatives of order up to and including $k$ are also
square integrable.

### Traces
Next, we define the Dirichlet and Neumann traces of a function on the boundary by

$$
(\gamma^-_\text{D}v)(\mathbf{x}):=\lim_{\Omega^-\ni \mathbf{x}'\to \mathbf{x}\in\Gamma}v(\mathbf{x}'),$$

$$
(\gamma^-_\text{N}v)(\mathbf{x}):=\gamma_\text{D}\nabla v(\mathbf{x'})\cdot\mathbf{n}_\mathbf{x}.
$$

We define the space $H^{1/2}(\Gamma)$ to be the Dirichlet trace of the space $H^1(\Omega^-)$:

$$
H^{1/2}(\Gamma):=\gamma_\text{D}H^1(\Omega^-)=\left\{\gamma_\text{D}v\middle|v\in H^1(\Omega^-)\right\}
$$

In general, for each positive integer $k$, we define the space $H^{k-1/2}(\Gamma)$ to be the Dirchlet
trace of the space $H^k(\Omega^-)$.

The space $H^{-1/2}(\Gamma)$ is defined as the dual space of $H^{1/2}(\Gamma)$:

$$
H^{-1/2}(\Gamma) = \left\{f:H^{1/2}(\Gamma)\to\mathbb{C}\right\}.
$$

## Vector function spaces
For Maxwell problems, we use spaces containing vector functions
$\mathbf{f}:\Omega^-\to\mathbb{C}^3$.
We begin by defining the space of square integrable functions:

$$
\mathbf{H}^0(\Omega^-):=\mathbf{L}^2(\Omega^-):=\left\{\mathbf{v}:\Omega^-\to\mathbb{C}^3\middle|\int_{\Omega^-} |\mathbf{v}|^2<\infty\right\}
$$

We then define the Sobolev space $\mathbf{H}^1(\Omega^-)$ to be the space of square integrable functions
whose first derivatives are also square integrable.


$$
\mathbf{H}^1(\Omega^-):=\left\{\mathbf{v}\in \mathbf{L}^2(\Omega^-)\middle|\frac{\partial \mathbf{v}}{\partial x}, \frac{\partial \mathbf{v}}{\partial y}, \frac{\partial \mathbf{v}}{\partial z}\in \mathbf{L}^2(\Omega)\right\}
$$

In general, for each positive integer $k$, we define the space $\mathbf{H}^k(\Omega^-)$ to be the space
of square integrable functions whose derivatives of order up to and including $k$ are also
square integrable.

### Traces
On $\Gamma$, we define the space of square integrable tangential vector fields:

$$
\mathbf{L}^2_\mathbf{t}(\Gamma):=\left\{\mathbf{v}\in\mathbf{L}^2(\Gamma)\middle|\mathbf{v}\cdot\mathbf{n}=0\right\}
$$

Next, we define the tangential and Neumann traces of a function on the boundary by

$$
(\mathbf{\gamma}^-_\textbf{t}\mathbf{v})(\mathbf{x}):=\lim_{\Omega^-\ni \mathbf{x}'\to \mathbf{x}\in\Gamma}\mathbf{v}(\mathbf{x}')\times\mathbf{n}_\mathbf{x},
$$

$$
(\mathbf{\gamma}^-_\textbf{N,k}\mathbf{v})(\mathbf{x}):=\frac1{\mathrm{i}k}\mathbf{\gamma}_\textbf{t}\nabla\times\mathbf{v}(\mathbf{x'}).
$$

We define the space $\mathbf{H}^{1/2}_\times(\Gamma)$ to be the tangential trace of the space $\mathbf{H}^1(\Omega^-)$:

$$
\mathbf{H}^{1/2}_\times(\Gamma):=\mathbf\gamma_\textbf{t}\mathbf{H}^1(\Omega^-)=\left\{\mathbf\gamma_\textbf{t}\mathbf{v}\middle|\mathbf{v}\in \mathbf{H}^1(\Omega^-)\right\}
$$

We define the spaces of div- and curl-conforming functions by:

$$
\mathbf{H}^{-1/2}_\times(\operatorname{div}_\Gamma,\Gamma):=\left\{\mathbf{v}\in\mathbf{H}^{1/2}_\times(\Gamma)\middle|\operatorname{div}_\Gamma\mathbf{v}\in H^{1/2}\times(\Gamma)\right\}
$$

$$
\mathbf{H}^{-1/2}_\times(\operatorname{curl}_\Gamma,\Gamma):=\left\{\mathbf{v}\in\mathbf{H}^{1/2}_\times(\Gamma)\middle|\operatorname{curl}_\Gamma\mathbf{v}\in H^{1/2}\times(\Gamma)\right\}
$$

In these definitions, $\operatorname{div}_\Gamma$
and $\operatorname{curl}_\Gamma$ are the scalar
surface div and curl operators. Using the definition of these, it can be seen that

$$
\mathbf{H}^{-1/2}_\times(\operatorname{curl}_\Gamma,\Gamma)=\left\{\mathbf{n}\times\mathbf{v}\middle|\mathbf{v}\in\mathbf{H}^{-1/2}_\times(\operatorname{div}_\Gamma,\Gamma)\right\}.
$$


