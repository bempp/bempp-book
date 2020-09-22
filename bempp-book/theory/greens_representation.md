(content:green_representation)=
# Green's Representation Theorem

In this chapter we will derive Green's representation theorem, which allows us to represent solutions of certain types of partial differential equations using only values and derivatives on the boundary.

## The divergence theorem

Our discussion starts with the divergence theorem. Assume that $\Omega\subset\mathbb{R}^3$ is a bounded domain with boundary $\Gamma$. For now we assume that $\Gamma$ is sufficiently smooth so that the following statements remain valid. For simplicity, we can just assume that $\Gamma\subset\mathcal{C}^2$. This means that in the neighborhood of each point $x\in\Gamma$ we can find a local parameterisation of the boundary $\Gamma$, which is twice continuously differentiable.

The divergence theorem now states that for each continuously differentiable vector valued function $F\in\mathbb{R}^3$ it holds that

$$
\int_{\Omega} (\nabla \cdot F) dV = \int_{\Gamma} (F\cdot n)dS.
$$

Here, $n$ is the exterior normal at the boundary $\Gamma$. The expression $\nabla\cdot F$ on the left-hand side of the theorem is the divergence of $F$, also abbreviated $\text{div} F$. The divergence theorem motivates another definition of the divergence. Let $S_r$ be a small sphere with radius $r$ and center $x$. Then 

$$
\text{div} F(x) = \lim_{r\rightarrow 0}\frac{1}{|S_r|}\int_{\Gamma}(F\cdot n)dS.
$$

The divergence if positive if the field $F$ is outward pointing at the point $x$. If the field at $x$ is inward pointing the divergence is negative.

## Green's identities

Based on the divergence theorem we can now derive the Green's identities. 
We start with the first Green's identity. Let $u$ and $v$ be scalar functions with $u$ continuously differentiable and $v$ twice continuously differentiable. Choose $F = u\nabla v$. From the product formula of differentiation it follows that

$$
\nabla \cdot (u\nabla v) = \nabla u \cdot \nabla v + u\Delta v.
$$
The operator $\Delta v$ is the Laplacian of $v$ defined as 

$$
\nabla\cdot(\nabla v) = \frac{\partial^2v}{\partial x^2} + \frac{\partial^2v}{\partial y^2} + \frac{\partial^2v}{\partial z^2}.
$$
Plugging $F = u\nabla v$ into the divergence theorem we arrive at Green's first identity, which states that

$$
\int_{\Omega} u\Delta v + \nabla u\cdot \nabla v\ dV = \int_{\Gamma} u\frac{\partial v}{\partial n} dS.
$$

The expression $\frac{\partial v}{\partial n} := \nabla v\cdot n$ is the normal derivative of $v$.

Now assume that also $u$ is twice differentiable and swap the roles of $u$ and $v$ in Green's first identity. Subtracting the two identities for $F=u\nabla v$ and $F=v\nabla u$ we obtain

$$
\int_{\Omega}u\Delta v - v\Delta u\ dV = \int_{\Gamma} u\frac{\partial v}{\partial n} - v\frac{\partial u}{\partial n}dS.
$$

This equation is called Green's second identity.

## Green's representation theorem

We can now derive Green's representation theorem. We first need to derive the notion of a Green's function. We consider the model PDE problem

$$
\mathcal{L}u(y) = f(y),~y\in\Omega
$$
with $\mathcal{L} := -\Delta - k^2$ and $f$ a given scalar function. This equation is called the Helmholtz equation with wavenumber $k$. We allow $k$ to take any value in the complex plane, including $0$. For $k=0$ the equation reduces to the Poisson equation $-\Delta u = f$.

We now introduce a special solution. Let $\delta_x(y)$ be the shifted Dirac delta function with $\delta_x(y) = 0$ for $x\neq y$.

A Green's function $g(x, y)$ is a function that satisfies

$$
\mathcal{L}g(x, y) = \delta_y(x)
$$
in $\Omega$.

Typically, for $g(x, y)$ we choose the free space Green's function that satisfies that equation in the whole of $\mathbb{R}^3$. For the given Helmholtz equation the free space Green's function is defined as

$$
g(x, y) = \frac{e^{ik|x - y|}}{4\pi|x-y|}
$$

Another valid definition is obtained by replacing $k$ with $-k$. The choice of the sign determines what is considered to be an outgoing wave solution. We will come back to this topic later.

For this function it holds for $x\neq y$ that

$$
\Delta_yg(x, y) = k^2g(x, y),
$$

where $\Delta_y$ denotes that we take the derivatives with respect to $y$. 

We now apply Green's second identity with $u(y)$ being a solution of $\mathcal{L}u(y)=f(y)$ in $\Omega$ and $v(y) = g(x, y)$. The resulting equation is

$$
u(x) = \int_{\Gamma}g(x, y)\frac{\partial u}{\partial n(y)}\ dS(y) - \int_{\Gamma} \frac{\partial g(x, y)}{\partial n(y)} u(y)\ dS(y) + \int_{\Omega}g(x, y)f(y)\ dV(y).
$$

This is Green's representation theorem. Let us consider the three appearing terms in some more detail. The first term is called the **single-layer potential operator**. For a given function $\phi$ it is defined as

$$
[\mathcal{V}\phi](x) = \int_{\Gamma}g(x, y)\frac{\partial u}{\partial n(y)}\ dS(y).
$$

The second term is called the **double-layer potential operator**. For a given function $\psi$ it is defined as

$$
[\mathcal{K}\psi](x) = \int_{\Gamma} \frac{\partial g(x, y)}{\partial n(y)} u(y)\ dS(y).
$$

Finally, the third term is the **Newton potential operator**. For a given function $f$ it is defined as

$$
[\mathcal{N}f](x) = \int_{\Omega}g(x, y)f(y)\ dV(y).
$$

With this notation Green's representation theorem has the compact form

$$
u_{\Omega} = \mathcal{V}u_{\Gamma} - \mathcal{K}u_n +\mathcal{N}f.
$$

Here, $u_{\Omega}$ is the function $u$ inside $\Omega$, $u_{\Gamma}$ denotes the boundary data of $u$ (or more precisely the trace of $u$), and $u_n$ denotes the normal derivative of $u$ on the boundary $\Gamma$.
