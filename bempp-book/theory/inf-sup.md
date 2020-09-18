Inf-Sup Stability
=================

$\mathcal{V}_h=\operatorname{span}\{\phi_1,...,\phi_n\}$
and
$\mathcal{W}_h=\operatorname{span}\{\psi_1,...,\psi_n\}$
be two finite dimensional spaces. We define the mass matrix
$M=(m_{ij})$
between these two spaces by

$$
m_{ij}=\int_\Gamma \psi_j\cdot\phi_i.
$$

When forming products of operators, the inverse of this mass matrix will be used. It is therefore
important that the matrix is non-singular. It can be shown that the matrix will be non-singular
if the following inf-sup condition holds:

There exists an $h$-independent constant $c>0$ such that

$$
\inf_{\phi\in\mathcal{V}_h}\sup_{\psi\in\mathcal{W}_h}\frac{\int_\Gamma \psi\cdot\phi}
{\|\phi\|\|\psi\|}
\geqslant c.
$$

This condition does not hold for the mass matrix between RWG and SNC spaces. It does however
hold between RWG and RBC, and between BC and SNC spaces. When solving Maxwell problems, care
must therefore be taken to ensure that all mass matrices involved are stably invertible.
