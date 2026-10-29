# Convexity

> **IOAI Guide — Convex Optimization**

> **Goal.** Identify convex sets and objectives and understand why convexity makes global optimization more tractable.

## Prerequisites and notation

Know derivatives, gradients, Hessian matrices, and positive semidefinite matrices. A convex set contains the segment joining any two of its points.

## Convex sets

A set $\mathcal C\subseteq\mathbb R^n$ is convex if the line segment between any two points in the set also lies in the set:

$$
\mathbf x,\mathbf y\in\mathcal C,\quad t\in[0,1]
\quad\Longrightarrow\quad t\mathbf x+(1-t)\mathbf y\in\mathcal C.
$$

Examples include intervals, affine subspaces, Euclidean balls, and half-spaces such as $\{\mathbf x:\mathbf a^\top\mathbf x\le b\}$. A circle's circumference alone is not a convex set, although the filled disk is.

## Convex functions

A function $f:\mathcal C\to\mathbb R$ on a convex domain is convex if

$$
f(t\mathbf x+(1-t)\mathbf y)\le tf(\mathbf x)+(1-t)f(\mathbf y)
$$

for every $\mathbf x,\mathbf y\in\mathcal C$ and $t\in[0,1]$. Geometrically, the graph lies below every chord joining two graph points. Strict convexity replaces the inequality with a strict inequality for distinct points and $t\in(0,1)$; strict convexity guarantees at most one minimizer. Strong convexity gives a quantitative lower bound on curvature and also guarantees uniqueness.

Examples:

- Affine $f(\mathbf x)=\mathbf a^\top\mathbf x+b$ is convex (but not strictly convex unless the domain is degenerate).
- A quadratic $f(\mathbf x)=\tfrac12\mathbf x^\top Q\mathbf x+\mathbf c^\top\mathbf x+b$ is convex if $Q$ is symmetric positive semidefinite (PSD): $Q\succeq0$.
- $f(x)=x^2$ and $f(x)=e^x$ are convex on $\mathbb R$; $f(x)=|x|$ is convex but not differentiable at zero.
- $f(x)=\log x$ is concave on $x>0$, not convex; $-\log x$ is convex there.

## First- and second-order tests

For differentiable $f$ on a convex domain, convexity is equivalent to the first-order condition

$$
f(\mathbf y)\ge f(\mathbf x)+\nabla f(\mathbf x)^\top(\mathbf y-\mathbf x)
$$

for all domain points $\mathbf x,\mathbf y$. The tangent plane lies below the function.

If $f$ is twice continuously differentiable on an open convex domain, then

$$
f\text{ is convex}\quad\Longleftrightarrow\quad\nabla^2 f(\mathbf x)\succeq0\text{ for every }\mathbf x.
$$

For a quadratic, this reduces to checking whether all eigenvalues of the symmetric matrix $Q$ are nonnegative. In one variable, $f''(x)\ge0$ throughout an interval is a sufficient and, under the stated smoothness, necessary condition for convexity there.

For a differentiable convex function over an unconstrained convex domain, a point satisfying $\nabla f(\mathbf x^*)=0$ is a global minimizer. For a convex but nondifferentiable function, subgradients generalize this condition: $0\in\partial f(\mathbf x^*)$ certifies a global minimum.

## Operations that preserve convexity

Useful rules include:

- A nonnegative weighted sum of convex functions is convex.
- Composing a convex function with an affine map preserves convexity: if $f$ is convex, then $g(\mathbf x)=f(A\mathbf x+\mathbf b)$ is convex.
- The pointwise maximum of convex functions is convex.
- The squared Euclidean norm $\|A\mathbf x-\mathbf b\|_2^2$ is convex in $\mathbf x$.

The feasible set of a convex optimization problem is commonly formed by affine equalities and convex inequality constraints $g_i(\mathbf x)\le0$. Sublevel sets $\{\mathbf x:f(\mathbf x)\le c\}$ of a convex function are convex.

## Why convexity matters in ML

Least-squares linear regression with objective $f(\mathbf w)=\frac{1}{2n}\|X\mathbf w-\mathbf y\|_2^2$ is convex in $\mathbf w$ because its Hessian is $X^\top X/n\succeq0$. Logistic regression with the usual log-loss is also convex in its weight vector. Deep neural-network training is generally nonconvex, so global-optimum guarantees from convex analysis do not directly apply to the full model.

## Common pitfalls and IOAI checklist

- Convexity depends on both the function and its domain.
- A positive semidefinite Hessian everywhere on a convex domain proves convexity when the function is twice differentiable.
- A zero gradient certifies a global minimum for a differentiable convex unconstrained function, but not for an arbitrary nonconvex function.
- Strict convexity guarantees at most one minimizer; existence still requires appropriate conditions.
- A circle's circumference is not convex, but the filled disk is.

## Quick self-check

1. Is $f(x)=x^2+2x+1$ convex on $\mathbb R$?
2. What Hessian condition is sufficient for twice-differentiable convexity on an open convex domain?
3. Does every local minimizer of a convex function have to be global?

**Answers:** (1) Yes, since $f''(x)=2$. (2) $\nabla^2 f(x)\succeq0$ everywhere on the domain. (3) Yes.
