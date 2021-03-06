# Function Spaces for scalar problems

In {ref}`content:green_representation`, we derived Green's representation
theorem for Helmholtz type problems in three dimensions. In this section, we
discuss in more detail what the correct function spaces for the various objects
in Green's representation theorem are. This is important for choosing the right
type of discretisations in actual computations.

We recall Green's representation theorem for the solution $u$ of the PDE $-\Delta u-k^2u=f$ in a domain $\Omega\subset\mathbb{R}^3$.

$$
u_{\Omega} = \mathcal{V}u_{\Gamma} - \mathcal{K}u_\mathbf{n} +\mathcal{N}f.
$$

Here, $u_{\Omega}$ is the solution $u$ inside $\Omega$, $u_{\Gamma}$ is the
restriction of $u_{\Omega}$ to the boundary $\Gamma$ and $u_\mathbf{n}$ is the
normal derivative of $u$ at the boundary $\Gamma$. The operators $\mathcal{V}$,
$\mathcal{K}$, and $\mathcal{N}$ are the single layer potential operator,
double layer potential operator, and the Newton potential operator,
respectively.

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

## The spaces $L^2(\Omega)$ and $H^1(\Omega)$

In order for {eq}`eq:squared_helmholtz` to make sense, we require all terms to be finite. This motivates the definition of the following spaces.

We define the following two spaces:

* The space of square integrable functions $L^2(\Omega)$ of all functions $v$ that satisfy $\int_{\Omega}|v|^2\ dV < \infty$.
* The space $H^1(\Omega)$ of all square integrable functions $v$ in $L^2(\Omega)$ that also have a square integrable derivative, that is $\int_{\Omega}|\nabla v|^2\ dV < \infty$.

The space $H^1(\Omega)$ is called a Sobolev space. The notion of derivative
here is a bit more general than then standard notion of derivative. It only
requires functions in the space to be weakly differentiable. While we want to
avoid going into too much detail of weak differentiability, a very good example
is the function $f(x) = |x|$ for $x\in [-1, 1]$. It is differentiable for
$x\neq 0$, but not at the point $x=0$. However, it is still weakly
differentiable. The derivative is well defined for all points $x\neq 0$, and at
zero we can assign the derivative any finite value to obtain $\int_{[-1, 1]}
|\nabla f(x)|^2\,\mathrm{d}x < \infty$. 

The space $H^1(\Omega)$ can also be interpreted as a space of functions with
bounded energy. It therefore makes physical sense to look for solutions in this
space, and indeed it is the right space of functions for Helmholtz problems.
This might be surprising as the original Helmholtz equation requires the
solution to be twice differentiable. But we have seen that the second
derivative disappears after integration by parts and this trick allows the
treatment of larger classes of problems than just those where a second
derivative exists in a strong classical sense. This is not artifical but
involves problems in domains with corners or where the forcing term $f$ on the
right-hand side is just a point load.

## The trace spaces $H^{1/2}(\Omega)$ and $H^{-1/2}(\Omega)$

We have not yet discussed the spaces associated with the term $\int_{\Gamma}u_{\Gamma}u_\mathbf{n}$ in {eq}`eq:squared_helmholtz`. The function $u_{\Gamma}$ is the restriction of $u_{\Omega}$ to $\Gamma$. It is possible to define a trace operator $\gamma_0$, which maps functions in $H^1(\Omega)$ to the values on the boundary. We define the space $H^{1/2}(\Omega)$ as the range of this operator, that is

$$
H^{1/2}(\Gamma) := \gamma_0(H^{1}(\Omega)).
$$

Hence, $H^{1/2}(\Gamma)$ consists of all functions that are the boundary values
of functions in $H^1(\Omega)$. The index $1/2$ may seem strange. Functions in
$H^1(\Omega)$ are 1 times weakly differentiable. The exponent $1/2$ denotes a
half-order loss of smoothness. There are different ways to define fractional
Sobolev spaces. But this is a technical topic, which we will not cover in more
detail here. For our purpose the only relevance is that the space
$H^{1/2}(\Omega)$ contains the boundary values of solutions to the Helmholtz
equation.

The other important boundary space is the space $H^{-1/2}(\Gamma)$. The
definition of this space is a bit more tricky. Loosely spoken, this space
contains all normal derivatives of functions $u_{\Omega}$ satisfying the
Helmholtz equation $Lu_{\Omega} = 0$.

We will not go into details of the meaning of the exponent $-1/2$. An intuitive
explanation is that taking derivatives reduces the order of a Sobolev space by
$1$. The space of boundary traces has order $1/2$, and henceforth the space of
normal derivatives has order one less, which is $-1/2$.


## Norms, inner products and dual pairings

Consider that we have computed some approximate solution $\tilde{u_{\Omega}}$
to an exact solution $u_{\Omega}$. We would like to quantify the error
$e_{\Omega} := \tilde{u_{\Omega}} - u_{\Omega}$. A typical measure here is the
square integral of the function, giving us the definition

$$
\|u\|_{\Omega} := \left[\int_{\Omega}|u(x)|^2\ dx\right]^{1/2}.
$$

Closely associated with this norm is the definition of the $L^2(\Omega)$ inner product

$$
\langle u, v\rangle_{\Omega} := \int_{\Omega} u(x)\overline{v(x)}\ dx.
$$

From this it follows that $\|u\|_{\Omega}^2 = \left[\langle u, u \rangle_{\Omega}\right]^{1/2}$.

Similarly, we define the $L^2(\Gamma)$ inner product over the boundary as

$$
\|u\|_{\Gamma} := \left[\int_{\Gamma}|u(x)|^2\ dx\right]^{1/2}.
$$

The related inner product definition is

$$
\langle u, v\rangle_{\Gamma} := \int_{\Gamma} u(x)\overline{v(x)}\ dx.
$$

Finally, we want to briefly talk about dual pairings. In
{eq}`eq:squared_helmholtz` we have two dual pairings. These are the terms
$\int_{\Gamma}\overline{u_{\Gamma}}u_n\ dS$ and
$\int_{\Omega}\overline{u_{\Omega}}f\ dV$. These look like the $L^2$ inner
products that we just defined, and in terms of practical implementation we will
treat them like this. Nevertheless, the definition is a bit more subtle. The
function $u_{\Gamma}$ is the trace of $u_{\Omega}$. Hence $u_{\Gamma}\in
H^{1/2}(\Omega)$. However, as stated above the normal derivative $u_n$ is in
the space $H^{-1/2}(\Gamma)$. The question is whether this is well defined, and
indeed it is. A dual pairing is a generalisation of $L^2$ inner products to
situations when the functions are in these opposite spaces. Practically, for
implementation purposes we treat this like any other $L^2$ inner product. But
mathematically the definition is more general. Indeed, a precise definition of
the space $H^{-1/2}(\Gamma)$ is that it is the space of all bounded
sesquilinear (linear, but taking complex conjugation into account) maps from
$H^{1/2}(\Gamma)$ into the complex numbers. We say that a function $v\in
H^{-1/2}(\Gamma)$ if the sesquilinear map

$$
\ell_v(u) :=\int_{\Gamma}v(x)\overline{u}(x)
$$
is well defined and bounded for $u\in H^{1/2}(\Gamma)$.

Correspondingly, in {eq}`eq:squared_helmholtz` the pairing $\int_{\Omega}\overline{u_{\Omega}}f\ dV$ is between a function $u\in H^1{\Omega}$ and an object $f$ in the dual space $H^{-1}(\Omega)$.

## A remark on the smoothness of $\Gamma$.

For the derivation of Green's representation theorem we assumed that the
boundary $\Gamma$ of $\Omega$ is sufficiently smooth and stated that it is
enough to be twice differentiable. Indeed, this condition can be weakened quite
substantially. It is sufficient to assume that $\Gamma$ is a Lipschitz
boundary. While the actual definition is quite intricate, for most practical
purposes it is enough to think of $\Omega$ as a bounded domain whose boundary
$\Gamma$ is piecewise smooth with no cusps or slits.

## Function spaces for potential operators

We recall Green's representation theorem from {ref}`content:green_representation`.

$$
u_{\Omega} = \mathcal{V}u_{\mathbf{n}} - \mathcal{K}u_\Gamma +\mathcal{N}f.
$$

Let us know introduce the correct function spaces for the single-layer potential operator $\mathcal{V}$, the double-layer potential operator $\mathcal{K}$, and the Newton potential $\mathcal{N}$.

Remember that from the discussion in this section we have $u_{\Omega}\in H^1(\Omega)$, $u_{\Gamma}\in H^{1/2}(\Gamma)$, $u_\mathbf{n}\in H^{-1/2}(\Gamma)$, $f\in H^{-1}(\Omega)$.

It follows that we require the potential operators to satisfy the following mapping properties:

* $\mathcal{V}:\ H^{-1/2}(\Gamma)\rightarrow H^{1}(\Omega)$
* $\mathcal{K}:\ H^{-1/2}(\Gamma)\rightarrow H^{1}(\Omega)$
* $\mathcal{N}:\ H^{-1}(\Omega)\rightarrow H^{1}(\Omega)$


