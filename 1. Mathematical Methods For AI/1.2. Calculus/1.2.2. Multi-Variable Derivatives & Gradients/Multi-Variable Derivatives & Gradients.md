# IOAI Guide — Calculus Foundations II: Multivariable Derivatives & Gradients

> **Goal.** Differentiate functions of vectors, interpret gradients geometrically, and compute common derivatives used by loss functions and optimization in machine learning.

## 1. Prerequisites: vectors, norms, and multivariable limits

A vector input is \(\mathbf{x}=(x_1,\ldots,x_n)^\top\in\mathbb{R}^n\). The Euclidean norm is \(\|\mathbf{x}\|_2=\sqrt{\sum_i x_i^2}\), and the dot product is \(\mathbf{a}^\top\mathbf{b}=\sum_i a_i b_i\).

A multivariable limit

\[
\lim_{\mathbf{x}\to\mathbf{a}}f(\mathbf{x})=L
\]

means that \(f(\mathbf{x})\) approaches \(L\) as the full vector \(\mathbf{x}\) approaches \(\mathbf{a}\) from every direction. Formally, for every \(\varepsilon>0\) there exists \(\delta>0\) such that

\[
0<\|\mathbf{x}-\mathbf{a}\|_2<\delta\implies |f(\mathbf{x})-L|<\varepsilon.
\]

**Path test:** if two paths approaching the same point give different limiting values, the limit does not exist. Agreement along a few paths is not enough by itself to prove that the limit exists.

Example:

\[
f(x,y)=\frac{xy}{x^2+y^2},\quad (x,y)\ne(0,0).
\]

Along \(y=0\), the function is \(0\); along \(y=x\), it is \(1/2\). Thus the limit at \((0,0)\) does not exist. For polynomials, and for rational functions with nonzero denominator at the target point, direct substitution is valid.

Continuity at \(\mathbf{a}\) means \(\lim_{\mathbf{x}\to\mathbf{a}}f(\mathbf{x})=f(\mathbf{a})\).

## 2. Partial derivatives

For \(f:\mathbb{R}^n\to\mathbb{R}\), the partial derivative with respect to coordinate \(x_i\) is

\[
\frac{\partial f}{\partial x_i}(\mathbf{x})
=\lim_{h\to0}\frac{f(\mathbf{x}+h\mathbf{e}_i)-f(\mathbf{x})}{h},
\]

where \(\mathbf{e}_i\) is the vector with a 1 in coordinate \(i\) and zeros elsewhere. Computationally, vary one coordinate and hold the others fixed.

For example, if \(f(x,y)=x^2y+3y\), then

\[
f_x=2xy,\qquad f_y=x^2+3.
\]

A partial derivative is a slope along one coordinate direction. In two variables, these are the slopes of tangent lines to coordinate-direction traces of the surface.

## 3. Gradient and directional derivatives

For a **scalar-valued** function \(f:\mathbb{R}^n\to\mathbb{R}\), we use the column-gradient convention

\[
\nabla f(\mathbf{x})=
\begin{bmatrix}\partial f/\partial x_1\\\vdots\\\partial f/\partial x_n\end{bmatrix}\in\mathbb{R}^n.
\]

The directional derivative in a unit direction \(\mathbf{u}\), with \(\|\mathbf{u}\|_2=1\), is

\[
D_{\mathbf{u}}f(\mathbf{x})=
\lim_{h\to0}\frac{f(\mathbf{x}+h\mathbf{u})-f(\mathbf{x})}{h}.
\]

If \(f\) is differentiable, then

\[
D_{\mathbf{u}}f(\mathbf{x})=\nabla f(\mathbf{x})^\top\mathbf{u}.
\]

The gradient points in the direction of steepest local increase; the maximum directional derivative over unit directions is \(\|\nabla f\|_2\), attained along \(\nabla f/\|\nabla f\|_2\) when the gradient is nonzero. The steepest decrease direction is the negative gradient.

Level sets \(f(\mathbf{x})=c\) are locally perpendicular to \(\nabla f\) wherever the gradient is nonzero. This is useful for understanding contours of a loss function.

## 4. Differentiability and linear approximation

Existence of all first partial derivatives at a point does **not** by itself guarantee differentiability there. Differentiability requires one linear map to approximate the change in every direction:

\[
f(\mathbf{a}+\mathbf{h})=f(\mathbf{a})+\nabla f(\mathbf{a})^\top\mathbf{h}+o(\|\mathbf{h}\|).
\]

If first partial derivatives exist in a neighborhood and are continuous at \(\mathbf{a}\), that is a common sufficient condition for differentiability.

The first-order linearization is

\[
L(\mathbf{x})=f(\mathbf{a})+\nabla f(\mathbf{a})^\top(\mathbf{x}-\mathbf{a}),
\]

so \(f(\mathbf{x})\approx L(\mathbf{x})\) for \(\mathbf{x}\) near \(\mathbf{a}\). For \(z=f(x,y)\), the graph of this approximation is the tangent plane

\[
z-z_0=f_x(a,b)(x-a)+f_y(a,b)(y-b),\quad z_0=f(a,b).
\]

The total differential records this linear change:

\[
df=\nabla f(\mathbf{x})^\top d\mathbf{x}=\sum_i\frac{\partial f}{\partial x_i}dx_i.
\]

## 5. Vector-valued functions and the Jacobian

Let \(F:\mathbb{R}^n\to\mathbb{R}^m\), with components \(F_1,\ldots,F_m\). Its Jacobian is an \(m\times n\) matrix:

\[
J_F(\mathbf{x})=\begin{bmatrix}
\partial F_1/\partial x_1&\cdots&\partial F_1/\partial x_n\\
\vdots&\ddots&\vdots\\
\partial F_m/\partial x_1&\cdots&\partial F_m/\partial x_n
\end{bmatrix}.
\]

Rows correspond to output components; columns correspond to input coordinates. When \(F\) is differentiable,

\[
F(\mathbf{x}+\mathbf{h})\approx F(\mathbf{x})+J_F(\mathbf{x})\mathbf{h}.
\]

For a scalar output (\(m=1\)), the Jacobian is a row vector and is the transpose of our column gradient:

\[
J_f=(\nabla f)^\top.
\]

**Shape rule:** \(J_F\) has shape `(number of outputs, number of inputs)`. Keeping track of shapes prevents many chain-rule and matrix-calculus mistakes.

## 6. Second derivatives and the Hessian

The Hessian of a scalar-valued function is the matrix of second partial derivatives:

\[
H_f(\mathbf{x})=\nabla^2 f(\mathbf{x})=
\begin{bmatrix}
\partial^2 f/\partial x_1^2&\cdots&\partial^2 f/\partial x_1\partial x_n\\
\vdots&\ddots&\vdots\\
\partial^2 f/\partial x_n\partial x_1&\cdots&\partial^2 f/\partial x_n^2
\end{bmatrix}.
\]

If the relevant second partial derivatives are continuous, mixed partials agree and the Hessian is symmetric. The Hessian measures curvature and appears in second-order optimization methods.

For a function of two variables, at a critical point let

\[
D=f_{xx}f_{yy}-f_{xy}^2.
\]

If \(D>0\) and \(f_{xx}>0\), it is a local minimum; if \(D>0\) and \(f_{xx}<0\), a local maximum; if \(D<0\), a saddle point. If \(D=0\), this test is inconclusive.

## 7. Common matrix derivatives (column-gradient convention)

Let \(\mathbf{x}\in\mathbb{R}^n\), \(\mathbf{a},\mathbf{b}\) be fixed vectors, and \(A\) be a fixed matrix of compatible shape. Unless noted, the gradient is with respect to the column vector \(\mathbf{x}\).

| Scalar expression \(f(\mathbf{x})\) | Gradient \(\nabla_{\mathbf{x}}f\) |
|---|---|
| \(c\) | \(\mathbf{0}\) |
| \(\mathbf{a}^\top\mathbf{x}\) | \(\mathbf{a}\) |
| \(\mathbf{x}^\top\mathbf{a}\) | \(\mathbf{a}\) |
| \(\mathbf{x}^\top\mathbf{x}=\|\mathbf{x}\|_2^2\) | \(2\mathbf{x}\) |
| \(\mathbf{c}^\top A\mathbf{x}\) | \(A^\top\mathbf{c}\) |
| \(\mathbf{x}^\top A\mathbf{x}\) | \((A+A^\top)\mathbf{x}\) |
| \(\frac12\mathbf{x}^\top A\mathbf{x}\), with \(A=A^\top\) | \(A\mathbf{x}\) |
| \(\|A\mathbf{x}-\mathbf{b}\|_2^2\) | \(2A^\top(A\mathbf{x}-\mathbf{b})\) |
| \(\frac12\|A\mathbf{x}-\mathbf{b}\|_2^2\) | \(A^\top(A\mathbf{x}-\mathbf{b})\) |

For matrix variables \(X\), use the Frobenius inner product convention: the gradient \(G\) satisfies \(df=\operatorname{tr}(G^\top dX)\).

| Scalar expression \(f(X)\) | Gradient with respect to \(X\) |
|---|---|
| \(\operatorname{tr}(A^\top X)\) | \(A\) |
| \(\|X\|_F^2=\operatorname{tr}(X^\top X)\) | \(2X\) |
| \(\operatorname{tr}(X^\top A X)\) | \((A+A^\top)X\) |
| \(\log|\det X|\), invertible square \(X\) | \(X^{-\top}\) |
| \(\det X\), invertible square \(X\) | \(\det(X)X^{-\top}\) |

For \(\operatorname{tr}(X^\top A X)\), \(X\) is a matrix and \(A\) is square of compatible size. If \(A\) is symmetric, the gradient is \(2AX\). The log-determinant formulas require invertibility; in optimization, \(\log\det X\) is usually used on positive-definite matrices.

### 7.1 Why the quadratic rule works

For \(f(\mathbf{x})=\mathbf{x}^\top A\mathbf{x}=\sum_{i,j}x_iA_{ij}x_j\), differentiating coordinate-wise gives

\[
\frac{\partial f}{\partial x_k}=\sum_j A_{kj}x_j+\sum_i x_iA_{ik}
= (A\mathbf{x})_k+(A^\top\mathbf{x})_k.
\]

Hence \(\nabla f=(A+A^\top)\mathbf{x}\). Only when \(A\) is symmetric can this be simplified to \(2A\mathbf{x}\).

## 8. ML connection: least-squares loss

Let \(A\in\mathbb{R}^{m\times n}\), \(\mathbf{x}\in\mathbb{R}^n\), and \(\mathbf{b}\in\mathbb{R}^m\). Define

\[
L(\mathbf{x})=\frac12\|A\mathbf{x}-\mathbf{b}\|_2^2.
\]

Set the residual \(\mathbf{r}=A\mathbf{x}-\mathbf{b}\). Since \(d\mathbf{r}=A\,d\mathbf{x}\),

\[
dL=\mathbf{r}^\top d\mathbf{r}=\mathbf{r}^\top A\,d\mathbf{x}
=(A^\top\mathbf{r})^\top d\mathbf{x},
\]

so

\[
\boxed{\nabla_{\mathbf{x}}L=A^\top(A\mathbf{x}-\mathbf{b})}.
\]

The Hessian is \(H_L=A^\top A\), which is positive semidefinite because

\[
\mathbf{v}^\top A^\top A\mathbf{v}=\|A\mathbf{v}\|_2^2\ge0.
\]

Thus this loss is convex. If \(A\) has full column rank, the Hessian is positive definite and the minimizer is unique. At a stationary point, \(A^\top A\mathbf{x}=A^\top\mathbf{b}\), the normal equations.

## 9. Gradient-based optimization

For a differentiable loss \(L(\mathbf{x})\), gradient descent updates

\[
\mathbf{x}_{t+1}=\mathbf{x}_t-\eta\nabla L(\mathbf{x}_t),
\]

where \(\eta>0\) is the learning rate. A gradient is a local direction of steepest increase, so subtracting it is a first-order step toward decreasing the loss. This does not guarantee convergence for an arbitrary learning rate or arbitrary nonconvex loss.

## 10. Worked example

Let \(f(x,y)=x^2+3xy+2y^2\). Then

\[
\nabla f=\begin{bmatrix}2x+3y\\3x+4y\end{bmatrix},\qquad
H_f=\begin{bmatrix}2&3\\3&4\end{bmatrix}.
\]

At \((1,2)\), \(\nabla f=(8,11)^\top\). The directional derivative in unit direction \(\mathbf{u}=(3/5,4/5)^\top\) is

\[
D_{\mathbf{u}}f=(8,11)\begin{bmatrix}3/5\\4/5\end{bmatrix}=\frac{68}{5}.
\]

## 11. Checklist and practice

1. For \(f(x,y)=e^{xy}+y^3\), calculate the gradient.
2. For \(L(\mathbf{x})=\frac12\|A\mathbf{x}-\mathbf{b}\|^2\), state the gradient and Hessian.
3. If \(F:\mathbb{R}^4\to\mathbb{R}^3\), what is the shape of \(J_F\)?
4. For non-symmetric \(A\), simplify \(\nabla_{\mathbf{x}}(\mathbf{x}^\top A\mathbf{x})\).

**Answers:** 1. \((ye^{xy},\ xe^{xy}+3y^2)^\top\). 2. \(A^\top(Ax-b)\) and \(A^\top A\). 3. \(3\times4\). 4. \((A+A^\top)x\).

## 12. Notation convention

These notes use **column gradients** for scalar functions, so \(\nabla f\in\mathbb{R}^n\), while a scalar-output Jacobian is the row \(J_f=(\nabla f)^\top\). Some textbooks define \(df/d\mathbf{x}\) as a row vector; that is a notation convention, not a disagreement about the derivative. Always write dimensions before multiplying matrices.
