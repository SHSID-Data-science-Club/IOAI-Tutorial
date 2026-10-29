# IOAI Guide — Calculus Foundations III: Chain Rule

> **Goal.** Differentiate nested functions and compositions of vector maps. The chain rule is the calculus operation that powers implicit differentiation, gradients through neural-network layers, and backpropagation.

## 1. Prerequisites and the central idea

The chain rule assumes the functions involved are differentiable at the relevant points. Review the derivative definition and scalar derivative rules in **Pile I**, and gradients/Jacobians in **Pile II**.

If a quantity changes through intermediate variables, its total rate of change is assembled by multiplying rates along each path and adding contributions from all paths.

## 2. Single-variable chain rule

If \(y=f(u)\) and \(u=g(x)\), then \(y=f(g(x))\) and

\[
\boxed{\frac{dy}{dx}=\frac{dy}{du}\frac{du}{dx}=f'(g(x))g'(x)}.
\]

**Procedure:** identify the outer function and the inner function; differentiate the outer function while keeping the inner expression intact; multiply by the derivative of the inner expression.

Example:

\[
\frac{d}{dx}\sin(x^2)=\cos(x^2)\cdot2x=2x\cos(x^2).
\]

For a deeper composition, continue applying the rule:

\[
\frac{d}{dx}e^{\sin(x^2)}=e^{\sin(x^2)}\cos(x^2)\cdot2x.
\]

A common error is to stop after differentiating the outer function, omitting the inner derivative.

## 3. Chain rule when the intermediate variable depends on several variables

Suppose \(z=f(x,y)\) and \(x=x(t), y=y(t)\). Then

\[
\boxed{\frac{dz}{dt}=\frac{\partial f}{\partial x}\frac{dx}{dt}+\frac{\partial f}{\partial y}\frac{dy}{dt}}.
\]

Each partial derivative measures one route by which \(t\) affects \(z\); add all routes. More generally, if \(u=f(x_1,\ldots,x_n)\) and each \(x_i=x_i(t)\),

\[
\frac{du}{dt}=\sum_{i=1}^{n}\frac{\partial f}{\partial x_i}\frac{dx_i}{dt}.
\]

If \(u=f(x,y)\), with \(x=x(s,t)\) and \(y=y(s,t)\), then

\[
\begin{aligned}
\frac{\partial u}{\partial s}&=u_x x_s+u_y y_s,\\
\frac{\partial u}{\partial t}&=u_x x_t+u_y y_t.
\end{aligned}
\]

The partial derivative \(u_x\) in this expression means the derivative of the outer function with respect to its intermediate coordinate; it is evaluated at the current \((x,y)\).

## 4. Multivariable chain rule in Jacobian form

Let \(g:\mathbb{R}^p\to\mathbb{R}^n\) and \(f:\mathbb{R}^n\to\mathbb{R}^m\), with \(y=g(x)\) and \(z=f(y)\). Using the convention that Jacobians have output coordinates in rows and input coordinates in columns,

\[
\boxed{J_{f\circ g}(x)=J_f(g(x))J_g(x)}.
\]

Dimensions verify the order:

\[
(m\times n)(n\times p)=m\times p.
\]

**Order matters:** the Jacobians multiply in the same order as the maps are applied in the composition, with the outer map's Jacobian on the left.

### 4.1 Scalar loss and reverse-mode form

For a scalar loss \(L=f(y)\), where \(y=g(x)\), and using **column gradients**,

\[
\boxed{\nabla_x L=J_g(x)^\top\nabla_y L}.
\]

This transpose form is central to backpropagation. A forward map sends a small input change to output change via \(dy\approx J_g\,dx\). A reverse gradient step propagates sensitivities backward by multiplying by \(J_g^\top\).

## 5. Computational graphs and backpropagation

Consider a computation with intermediate nodes. If \(z=a(b(x))\), then

\[
\frac{dz}{dx}=\frac{dz}{db}\frac{db}{dx}.
\]

With branching, sum the contribution from each outgoing path. For example, if \(L=u+v\), where \(u=u(x)\) and \(v=v(x)\), then \(dL/dx=du/dx+dv/dx\).

For a simple linear layer \(y=Wx+b\) with \(W\) and \(b\) fixed,

\[
J_y=W,\qquad \nabla_x L=W^\top\nabla_y L.
\]

If \(L=\frac12\|y-t\|^2\), then \(\nabla_y L=y-t\), so

\[
\nabla_x L=W^\top(y-t).
\]

This is the same chain rule used in neural-network training. In code, automatic differentiation systems construct these products efficiently without explicitly storing a full Jacobian in many cases.

## 6. Implicit differentiation

Sometimes a dependent variable is defined by an equation instead of an explicit formula. If \(F(x,y)=0\) defines \(y\) as a differentiable function of \(x\), differentiate both sides with respect to \(x\):

\[
F_x+F_y\frac{dy}{dx}=0.
\]

When \(F_y\ne0\),

\[
\boxed{\frac{dy}{dx}=-\frac{F_x}{F_y}}.
\]

Example: for \(x^2+y^2=1\), treat the equation as \(F(x,y)=x^2+y^2-1=0\). Then

\[
\frac{dy}{dx}=-\frac{2x}{2y}=-\frac{x}{y},\qquad y\ne0.
\]

The formula is local: it applies on a portion of the curve where \(y\) can be expressed as a differentiable function of \(x\). At \(y=0\), this graph representation has a vertical tangent and the formula cannot give a finite slope.

For \(F(x_1,\ldots,x_n,y)=0\), if \(F_y\ne0\), then

\[
\frac{\partial y}{\partial x_i}=-\frac{F_{x_i}}{F_y}.
\]

## 7. Parametric curves and inverse functions

If \(x=x(t)\) and \(y=y(t)\), then, when \(dx/dt\ne0\),

\[
\frac{dy}{dx}=\frac{dy/dt}{dx/dt}.
\]

This is the chain rule written as \(dy/dt=(dy/dx)(dx/dt)\). It is useful for curves for which eliminating the parameter is difficult.

If \(y=f^{-1}(x)\) and \(f'(f^{-1}(x))\ne0\), differentiating \(f(f^{-1}(x))=x\) yields

\[
(f^{-1})'(x)=\frac{1}{f'(f^{-1}(x))}.
\]

## 8. Matrix chain-rule patterns used in ML

### 8.1 Linear map followed by a scalar loss

Let \(z=Ax+b\), and let \(L=\ell(z)\), with \(A\) fixed. Then

\[
\nabla_x L=A^\top\nabla_z\ell.
\]

For \(L(x)=\frac12\|Ax-b\|_2^2\), this gives \(\nabla_x L=A^\top(Ax-b)\), matching the matrix-derivative table in Pile II.

### 8.2 Quadratic form through an intermediate vector

Let \(z=Ax\) and \(L=z^\top z\). Then \(\nabla_z L=2z\), so

\[
\nabla_x L=A^\top(2z)=2A^\top A x.
\]

This demonstrates why gradient propagation uses a transpose.

### 8.3 Parameter gradients

For a linear model \(y=Wx+b\) and scalar loss \(L(y)\), let \(g=\nabla_y L\). Then

\[
\nabla_b L=g,\qquad \nabla_W L=gx^\top.
\]

The dimensions are \(g\in\mathbb{R}^m\), \(x\in\mathbb{R}^n\), so \(gx^\top\in\mathbb{R}^{m\times n}\), matching the shape of \(W\).

## 9. Worked example: total derivative

Let \(z=x^2y+\sin y\), with \(x=t^2\) and \(y=3t\). First compute

\[
z_x=2xy,\qquad z_y=x^2+\cos y,
\]

then

\[
\frac{dz}{dt}=z_x\frac{dx}{dt}+z_y\frac{dy}{dt}
=(2xy)(2t)+(x^2+\cos y)3.
\]

Substituting \(x=t^2, y=3t\),

\[
\frac{dz}{dt}=12t^4+3t^4+3\cos(3t)=15t^4+3\cos(3t).
\]

Direct substitution gives \(z(t)=3t^5+\sin(3t)\), whose derivative confirms the result.

## 10. Common mistakes

- Forgetting the derivative of the inner function.
- Confusing a partial derivative with a total derivative when intermediate variables depend on the input.
- Multiplying Jacobians in the wrong order or using incompatible dimensions.
- Forgetting the transpose when propagating a column gradient backward: \(\nabla_x L=J_g^\top\nabla_y L\).
- Using implicit differentiation where the denominator partial \(F_y\) is zero.
- Treating a variable matrix or vector as constant when differentiating with respect to it.

## 11. Checklist and practice

1. Differentiate \(\cos(5x^3)\).
2. If \(z=x^2+y^2\), \(x=t\), and \(y=t^2\), find \(dz/dt\).
3. If \(g:\mathbb{R}^4\to\mathbb{R}^3\) and \(f:\mathbb{R}^3\to\mathbb{R}^2\), what are the shapes of \(J_g\), \(J_f\), and \(J_{f\circ g}\)?
4. For \(x^2+xy+y^2=7\), find \(dy/dx\) where \(x+2y\ne0\).
5. Let \(y=Wx+b\) and \(\nabla_y L=g\). State \(\nabla_x L\) and \(\nabla_W L\).

**Answers:** 1. \(-15x^2\sin(5x^3)\). 2. \(2t+4t^3\). 3. \(J_g:3\times4\), \(J_f:2\times3\), composite: \(2\times4\). 4. Differentiate: \(2x+y+x y'+2yy'=0\), so \(y'=-(2x+y)/(x+2y)\). 5. \(W^\top g\) and \(gx^\top\).

## 12. Connection to the other piles

- **Pile I — Single-Variable Derivatives:** limits, continuity, derivative definition, elementary derivative rules.
- **Pile II — Multivariable Derivatives & Gradients:** partial derivatives, gradients, Jacobians, Hessians, matrix derivatives.
- **This pile:** how those derivatives compose and propagate through intermediate variables, implicit equations, and ML computation graphs.
