# Function Spaces for scalar problems

In {ref}`content:green_representation`, we derived Green's representation theorem for Helmholtz type problems in three dimensions. In this section, we discuss in more detail what the correct function spaces for the various objects in Green's representation theorem are. This is important for choosing the right type of discretisations in actual computations.

We recall Green's representation theorem for the solution $u$ of the PDE $-\Delta u-k^2u=f$ in a domain $\Omega\subset\mathbb{R}^3$.

$$
u_{\Omega} = \mathcal{V}u_{\Gamma} - \mathcal{K}u_\mathbf{n} +\mathcal{N}f.
$$

Here, $u_{\Omega}$ is the solution $u$ inside $\Omega$, $u_{\Gamma}$ is the restriction of $u_{\Omega}$ to the boundary $\Gamma$ and $u_\mathbf{n}$ is the normal derivative of $u$ at the boundary $\Gamma$. The operators $\mathcal{V}$, $\mathcal{K}$, and $\mathcal{N}$ are the single layer potential operator, double layer potential operator, and the Newton potential operator, respectively.

In this section, we discuss the suitable function spaces for Green's representation theorem to make sense.

We start off with the solution $u_{\Omega}$ satisfying

$$
-\Delta u_{\Omega}(x) - k^2u_{\Omega}(x) = f(x)
$$ 

for $x\in\Omega$. To obtain more insight into the properties of $u_{\Omega}$ we multiply this equation with $\overline{u_{\Omega}}$ (the complex conjugate of $u_{\Omega}$) and integrate by parts to obtain

$$
\int_{\Omega}|\nabla u_{\Omega}|^2\,\mathrm{d}V - k^2\int_{\Omega} |u_{\Omega}|^2\,\mathrm{d}V - \int_{\Gamma}\overline{u_{\Gamma}}u_\mathbf{n}\,\mathrm{d}S = \int_{\Omega}\overline{u_{\Omega}}f\,\mathrm{d}V
$$ (eq:squared_helmholtz)

By $u_{\Gamma}$ we denote the restriction of the domain solution $u_{\Omega}$ the boundary $\Gamma$.

In order for this equation to make sense, we require all terms to be finite. This motivates the definition of the following spaces.

## The spaces $L^2(\Omega)$ and $H^1(\Omega)$
We define:
* the space of square integrable functions $L^2(\Omega)$ of all functions $v$ that satisfy $\int_{\Omega}|v|^2\ dV < \infty$.
* the space $H^1(\Omega)$ of all square integrable functions $v$ in $L^2(\Omega)$ that also have a square integrable derivative, that is $\int_{\Omega}|\nabla v|^2\ dV < \infty$.

The space $H^1(\Omega)$ is called a Sobolev space. The notion of derivative here is a bit more general than then standard notion of derivative. It only requires functions in the space to be weakly differentiable. While we want to avoid going into too much detail of weak differentiability, a very good example is the function $f(x) = |x|$ for $x\in [-1, 1]$. It is differentiable for $x\neq 0$, but not at the point $x=0$. However, it is still weakly differentiable. The derivative is well defined for all points $x\neq 0$, and at zero we can assign the derivative any finite value to obtain $\int_{[-1, 1]} |\nabla f(x)|^2\,\mathrm{d}x < \infty$. 

The space $H^1(\Omega)$ can also be interpreted as a space of functions with bounded energy. It therefore makes physical sense to look for solutions in this space, and indeed it is the right space of functions for Helmholtz problems. This might be surprising as the original Helmholtz equation requires the solution to be twice differentiable. But we have seen that the second derivative disappears after integration by parts and this trick allows the treatment of larger classes of problems than just those where a second derivative exists in a strong classical sense. This is not artifical but involves problems in domains with corners or where the forcing term $f$ on the right-hand side is just a point load.

## The trace spaces $H^{1/2}(\Omega)$ and $H^{-1/2}(\Omega)$.

We have not yet discussed the spaces associated with the term $\int_{\Gamma}u_{\Gamma}u_\mathbf{n}$ in {eq}`eq:squared_helmholtz`. The function $u_{\Gamma}$ is the restriction of $u_{\Omega}$ to $\Gamma$. It is possible to define a trace operator $\gamma_0$, which maps functions in $H^1(\Omega)$ to the values on the boundary. We define the space $H^{1/2}(\Omega)$ as the range of this operator, that is

$$
H^{1/2}(\Gamma) := \gamma_0(H^{1}(\Omega)).
$$

Hence, $H^{1/2}(\Gamma)$ consists of all functions that are the boundary values of functions in $H^1(\Omega)$. The index $1/2$ may seem strange. Functions in $H^1(\Omega)$ are 1 times weakly differentiable. The exponent $1/2$ denotes a half-order loss of smoothness. There are different ways to define fractional Sobolev spaces. But this is a technical topic, which we will not cover in more detail here. For our purpose the only relevance is that the space $H^{1/2}(\Omega)$ contains the boundary values of solutions to the Helmholtz equation.

The other important boundary space is the space $H^{-1/2}(\Gamma)$. This space contains all normal derivatives of functions in $H^1(\Omega)$. We define the operator $\gamma_1$, which maps a function $u$ in $H^1(\Omega)$ to its normal derivative $u_n$ on $\Gamma$. Then 

$$
H^{-1/2}(\Gamma) := \gamma_1(H^{1}(\Omega)).
$$

We will not go into details of the meaning of the exponent $-1/2$. An intuitive explanation is that taking derivatives reduces the order of a Sobolev space by $1$. The space of boundary traces has order $1/2$, and henceforth the space of normal derivatives has order one less, which is $-1/2$.


## Norms, inner products and dual pairings


