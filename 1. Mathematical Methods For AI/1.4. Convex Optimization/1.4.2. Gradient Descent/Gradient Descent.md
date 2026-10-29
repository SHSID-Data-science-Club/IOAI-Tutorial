# Gradient Descent

> **IOAI Guide — Convex Optimization**

> **Goal.** Minimize a differentiable objective iteratively by moving in the direction of steepest local decrease.

## Prerequisites and notation

Know the gradient $\nabla f(x)$ and how to evaluate an objective. Gradient descent requires a starting point, a gradient, and a learning rate (step size).

## Update rule

For a differentiable objective $f:\mathbb R^d\to\mathbb R$, gradient descent iterates

$$
\mathbf x_{k+1}=\mathbf x_k-\eta_k\nabla f(\mathbf x_k),
$$

where $\eta_k>0$ is the learning rate (step size). Since the gradient points toward steepest local increase under the Euclidean norm, its negative is a local direction of decrease. The update uses a local linear approximation; an excessively large step may overshoot or diverge.

## A one-dimensional example

Let $f(x)=(x-3)^2$. Then $f'(x)=2(x-3)$ and gradient descent becomes

$$
x_{k+1}=x_k-2\eta(x_k-3).
$$

The error relative to the minimizer $3$ obeys

$$
x_{k+1}-3=(1-2\eta)(x_k-3).
$$

For this quadratic, convergence from any starting point occurs when $|1-2\eta|<1$, or $0<\eta<1$. At $\eta=1/2$, one step reaches the minimizer exactly. This is a special simple quadratic, not a universal learning-rate rule.

## Smoothness and step size

A differentiable function is $L$-smooth when its gradient is Lipschitz continuous:

$$
\|\nabla f(\mathbf x)-\nabla f(\mathbf y)\|_2\le L\|\mathbf x-\mathbf y\|_2.
$$

For an $L$-smooth function, the descent lemma states

$$
f(\mathbf y)\le f(\mathbf x)+\nabla f(\mathbf x)^\top(\mathbf y-\mathbf x)+\frac L2\|\mathbf y-\mathbf x\|_2^2.
$$

Substituting the gradient step with $0<\eta\le1/L$ gives a guaranteed decrease whenever the gradient is nonzero:

$$
f(\mathbf x-\eta\nabla f(\mathbf x))\le f(\mathbf x)-\eta\left(1-\frac{L\eta}{2}\right)\|\nabla f(\mathbf x)\|_2^2.
$$

This condition is a safe theoretical step-size range for smooth objectives, though practical algorithms may use line search, schedules, adaptive methods, or stochastic gradients.

## Convex versus strongly convex objectives

For a convex differentiable function, gradient descent with suitable step sizes converges in objective value under standard assumptions, but a minimizer may not be unique. Strong convexity means that for some $\mu>0$,

$$
f(\mathbf y)\ge f(\mathbf x)+\nabla f(\mathbf x)^\top(\mathbf y-\mathbf x)+\frac\mu2\|\mathbf y-\mathbf x\|_2^2.
$$

Strong convexity prevents flat directions, ensures a unique minimizer, and permits faster linear convergence guarantees when combined with smoothness and suitable step sizes. The condition number $L/\mu$ measures how uneven the curvature can be; a large condition number often makes optimization slow.

## Batch, stochastic, and mini-batch gradients

If the loss is an average of sample losses,

$$
f(\mathbf w)=\frac1n\sum_{i=1}^n\ell_i(\mathbf w),\qquad \nabla f(\mathbf w)=\frac1n\sum_{i=1}^n\nabla\ell_i(\mathbf w),
$$

**batch gradient descent** uses every sample for each update. **Stochastic gradient descent (SGD)** uses one randomly selected sample's gradient, and **mini-batch SGD** uses a small batch. Stochastic estimates are cheaper per update but noisy. The learning rate, batch size, data order, feature scaling, and stopping criterion all affect training.

## Practical workflow and diagnostics

1. Write down the objective and identify the variables being optimized.
2. Derive the gradient and check its dimensions.
3. Initialize parameters and choose a step size.
4. Update parameters, track objective values, and stop using a justified tolerance or iteration limit.
5. Compare the analytic gradient against a finite-difference approximation on a tiny example.
6. If the loss increases or becomes non-finite, check the gradient, learning rate, scaling, and numerical stability.

Gradient descent can find only what its assumptions allow. For a nonconvex objective, a stationary point may be a local minimum, a local maximum, or a saddle point.

## Common pitfalls and IOAI checklist

- Use the negative gradient for minimization: $x_{k+1}=x_k-\eta\nabla f(x_k)$.
- A learning rate that is too large can cause oscillation or divergence.
- Derive gradients carefully and check their dimensions.
- Track the objective and gradient norm; a falling loss is not guaranteed for every step size.
- For nonconvex objectives, a stationary point need not be a global minimum.

## Quick self-check

1. Write one gradient-descent update for $f(x)=x^2$.
2. For $f(x)=(x-3)^2$, what is $f'(x)$?
3. What does $L$-smoothness bound?

**Answers:** (1) $x_{k+1}=x_k-2\eta x_k$. (2) $2(x-3)$. (3) How quickly the gradient can change, via a Lipschitz bound.
