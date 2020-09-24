(content:green_representation)=
# Green's Representation Theorem

In this section, we will derive Green's representation theorem, which allows us to represent solutions of certain types of partial differential equations using only values and derivatives on the boundary.

## The divergence theorem

Our discussion starts with the divergence theorem. Assume that $\Omega\subset\mathbb{R}^3$ is a bounded domain with boundary $\Gamma$. For now we assume that $\Gamma$ is sufficiently smooth so that the following statements remain valid. For simplicity, we can just assume that $\Gamma\in C^2$. This means that in the neighborhood of each point $\mathbf{x}\in\Gamma$ we can find a local parameterisation of the boundary $\Gamma$, which is twice continuously differentiable.

The divergence theorem now states that for each continuously differentiable vector valued function $\mathbf{F}\in\mathbb{R}^3$ it holds that

$$
\int_{\Omega} (\nabla \cdot \mathbf{F})\,\mathrm{d}V = \int_{\Gamma} (\mathbf{P}\cdot \mathbf{n})\,\mathrm{d}S.
$$

Here, $\mathbf{n}$ is the exterior normal at the boundary $\Gamma$. The expression $\nabla\cdot \mathbf{F}$ on the left-hand side of the theorem is the divergence of $\mathbf{F}$, also abbreviated $\text{div} \mathbf{F}$. The divergence theorem motivates another definition of the divergence. Let $S_r$ be a small sphere with radius $r$ and center $\mathbf{x}$. Then 

$$
\operatorname{div} \mathbf{F}(\mathbf{x}) = \lim_{r\rightarrow 0}\frac{1}{|S_r|}\int_{\Gamma}(\mathbf{F}\cdot \mathbf{n})\,\mathrm{d}S.
$$

The divergence is positive if the field $\mathbf{F}$ is outward pointing at the point $\mathbf{x}$. If the field at $\mathbf{x}$ is inward pointing the divergence is negative.

## Green's identities

Based on the divergence theorem, we can now derive the Green's identities. 
We start with the first Green's identity. Let $u$ and $v$ be scalar functions with $u$ continuously differentiable and $v$ twice continuously differentiable. Choose $\mathbf{F} = u\nabla v$. From the product rule of differentiation it follows that

$$
\nabla \cdot (u\nabla v) = \nabla u \cdot \nabla v + u\Delta v.
$$
The operator $\Delta v$ is the Laplacian of $v$ defined as 

$$
\nabla\cdot(\nabla v) = \frac{\partial^2v}{\partial x^2} + \frac{\partial^2v}{\partial y^2} + \frac{\partial^2v}{\partial z^2}.
$$
Plugging $\mathbf{F} = u\nabla v$ into the divergence theorem we arrive at Green's first identity, which states that

$$
\int_{\Omega} u\Delta v + \nabla u\cdot \nabla v\,\mathrm{d}V = \int_{\Gamma} u\frac{\partial v}{\partial \mathbf{n}}\,\mathrm{d}S.
$$

The expression $\frac{\partial v}{\partial \mathbf{n}} := \nabla v\cdot \mathbf{n}$ is the normal derivative of $v$.

Now assume that also $u$ is twice differentiable and swap the roles of $u$ and $v$ in Green's first identity. Subtracting the two identities for $F=u\nabla v$ and $F=v\nabla u$ we obtain

$$
\int_{\Omega}u\Delta v - v\Delta u\ dV = \int_{\Gamma} u\frac{\partial v}{\partial \mathbf{n}} - v\frac{\partial u}{\partial \mathbf{n}}\,\mathrm{d}S.
$$

This equation is called Green's second identity.

## Green's representation theorem

We can now derive Green's representation theorem. We first need to derive the notion of a Green's function. We consider the model PDE problem

$$
\mathcal{L}u(\mathbf{y}) = f(\mathbf{y}),\quad\mathbf{y}\in\Omega
$$
with $\mathcal{L} := -\Delta - k^2$ and $f$ a given scalar function. This equation is called the Helmholtz equation with wavenumber $k$. We allow $k$ to take any value in the complex plane, including $0$. For $k=0$ the equation reduces to the Poisson equation $-\Delta u = f$.

We now introduce a special solution. Let $\delta_\mathbf{x}(\mathbf{y})$ be the shifted Dirac delta function with $\delta_\mathbf{x}(\mathbf{y}) = 0$ for $\mathbf{x}\neq \mathbf{y}$.

A Green's function $g(\mathbf{x}, \mathbf{y})$ is a function that satisfies

$$
\mathcal{L}g(\mathbf{x}, \mathbf{y}) = \delta_\mathbf{y}(\mathbf{x})
$$
in $\Omega$.

Typically, for $g(\mathbf{x}, \mathbf{y})$ we choose the free space Green's function that satisfies that equation in the whole of $\mathbb{R}^3$. For the given Helmholtz equation the free space Green's function is defined as

$$
g(\mathbf{x}, \mathbf{y}) = \frac{e^{\mathrm{i}k|\mathrm{x} - \mathbf{y}|}}{4\text{π}|\mathbf{x}-\mathbf{y}|}
$$

Another valid definition is obtained by replacing $k$ with $-k$. The choice of the sign determines what is considered to be an outgoing wave solution. We will come back to this topic later.

For this function it holds for $\mathbf{x}\neq \mathbf{y}$ that

$$
\Delta_\mathbf{y}g(\mathbf{x}, \mathbf{y}) = k^2g(\mathbf{x}, \mathbf{y}),
$$

where $\Delta_\mathbf{y}$ denotes that we take the derivatives with respect to $\mathbf{y}$. 

We now apply Green's second identity with $u(\mathbf{y})$ being a solution of $\mathcal{L}u(\mathbf{y})=f(\mathbf{y})$ in $\Omega$ and $v(\mathbf{y}) = g(\mathbf{x}, \mathbf{y})$. The resulting equation is

$$
u(\mathbf{x}) = \int_{\Gamma}g(\mathbf{x}, \mathbf{y})\frac{\partial u}{\partial \mathbf{n}(\mathbf{y})}\,\mathrm{d}S(\mathbf{y}) - \int_{\Gamma} \frac{\partial g(\mathbf{x}, \mathbf{y})}{\partial \mathbf{n}(\mathbf{y})} u(\mathbf{y})\,\mathrm{d}S(\mathbf{y}) + \int_{\Omega}g(\mathbf{x}, \mathbf{y})f(\mathbf{y})\,\mathrm{d}V(\mathbf{y}).
$$

This is Green's representation theorem. Let us consider the three appearing terms in some more detail. The first term is called the **single-layer potential operator**. For a given function $\phi$ it is defined as

$$
[\mathcal{V}\phi](\mathbf{x}) = \int_{\Gamma}g(\mathbf{x}, \mathbf{y})\frac{\partial u}{\partial \mathbf{n}(\mathbf{y})}\,\mathrm{d}S(\mathbf{y}).
$$

The second term is called the **double-layer potential operator**. For a given function $\psi$ it is defined as

$$
[\mathcal{K}\psi](\mathbf{x}) = \int_{\Gamma} \frac{\partial g(\mathbf{x}, \mathbf{y})}{\partial \mathbf{n}(\mathbf{y})} u(\mathbf{y})\,\mathrm{d}S(\mathbf{y}).
$$

Finally, the third term is the **Newton potential operator**. For a given function $f$ it is defined as

$$
[\mathcal{N}f](\mathbf{x}) = \int_{\Omega}g(\mathbf{x}, \mathbf{y})f(\mathbf{y})\,\mathrm{d}V(\mathbf{y}).
$$

With this notation, Green's representation theorem has the compact form

$$
u_{\Omega} = \mathcal{V}u_{\mathbf{n}} - \mathcal{K}u_\Gamma +\mathcal{N}f.
$$

Here, $u_{\Omega}$ is the function $u$ inside $\Omega$, $u_{\Gamma}$ denotes the boundary data of $u$ (or more precisely the trace of $u$), and $u_\mathbf{n}$ denotes the normal derivative of $u$ on the boundary $\Gamma$.
