# Duality

> **IOAI Guide — Convex Optimization**

> **Goal.** Construct a Lagrange dual problem, use weak/strong duality, and interpret KKT conditions as an optimality certificate.

## Prerequisites and notation

Know constrained minimization, inequality constraints written as $g_i(x)\le0$, derivatives, and feasible points. Lagrange multipliers encode how constraints influence the objective.

Duality provides an alternative optimization problem whose value gives a bound on the original problem. It can yield optimality certificates, reveal shadow prices for constraints, and make some problems easier to solve.

## Primal problem and Lagrangian

Consider a minimization problem

$$
\begin{aligned}
p^*=\min_{\mathbf x}\quad & f_0(\mathbf x)\\
\text{subject to}\quad & g_i(\mathbf x)\le0,\quad i=1,\ldots,m,\\
& h_j(\mathbf x)=0,\quad j=1,\ldots,r.
\end{aligned}
$$

The **primal problem** is the original constrained problem. Introduce multipliers $\lambda_i\ge0$ for inequalities and $\nu_j\in\mathbb R$ for equalities. The Lagrangian is

$$
\mathcal L(\mathbf x,\boldsymbol\lambda,\boldsymbol\nu)
=f_0(\mathbf x)+\sum_{i=1}^m\lambda_i g_i(\mathbf x)+\sum_{j=1}^r\nu_jh_j(\mathbf x).
$$

Inequality multipliers must be nonnegative; equality multipliers are unrestricted in sign.

## The dual function and dual problem

The dual function is the infimum of the Lagrangian over the primal variable:

$$
q(\boldsymbol\lambda,\boldsymbol\nu)=\inf_{\mathbf x}\mathcal L(\mathbf x,\boldsymbol\lambda,\boldsymbol\nu).
$$

For every dual-feasible multiplier vector, $q$ gives a lower bound on the primal minimum. The **Lagrange dual problem** is

$$
d^*=\sup_{\boldsymbol\lambda\ge0,\,\boldsymbol\nu}q(\boldsymbol\lambda,\boldsymbol\nu).
$$

It is a maximization problem even though the primal is a minimization problem. The dual function is always concave, including when the primal problem is nonconvex, because it is a pointwise infimum of affine functions of the multipliers.

## Weak and strong duality

**Weak duality** always gives $d^*\le p^*$ for a feasible primal problem and its Lagrange dual. Thus the duality gap $p^*-d^*$ is nonnegative. If a feasible dual point has value $q$ close to a known primal value, the gap bounds how far from optimal that primal value could be.

**Strong duality** means $d^*=p^*$, so the optimal values agree. Strong duality does not hold for every constrained problem. For a convex problem with a convex objective, convex inequality constraints, affine equality constraints, and an appropriate strict-feasibility condition such as Slater's condition, strong duality holds under standard assumptions.

## Worked example: minimizing a quadratic subject to a lower bound

Consider

$$
\min_x x^2\quad\text{subject to }x\ge1.
$$

Write the inequality as $g(x)=1-x\le0$. The primal optimum is $x^*=1$ with $p^*=1$. Its Lagrangian is

$$
\mathcal L(x,\lambda)=x^2+\lambda(1-x),\qquad \lambda\ge0.
$$

For a fixed $\lambda$, minimize over $x$. Differentiating gives $2x-\lambda=0$, so $x=\lambda/2$. Substitution yields the dual function

$$
q(\lambda)=\inf_x\mathcal L(x,\lambda)=\lambda-\frac{\lambda^2}{4},\qquad \lambda\ge0.
$$

This concave quadratic is maximized at $\lambda^*=2$, with $d^*=q(2)=1=p^*$. The duality gap is zero. The optimal multiplier can be interpreted as the marginal increase in optimal cost when the constraint is tightened locally (a shadow price, subject to regularity conditions).

## KKT conditions

For a differentiable convex problem with suitable constraint qualifications, the Karush–Kuhn–Tucker conditions characterize optimality. A primal point $\mathbf x^*$ and multipliers $(\boldsymbol\lambda^*,\boldsymbol\nu^*)$ satisfy:

1. **Primal feasibility:** $g_i(\mathbf x^*)\le0$ and $h_j(\mathbf x^*)=0$.
2. **Dual feasibility:** $\lambda_i^*\ge0$.
3. **Stationarity:**

   $$
   \nabla f_0(\mathbf x^*)+\sum_i\lambda_i^*\nabla g_i(\mathbf x^*)+\sum_j\nu_j^*\nabla h_j(\mathbf x^*)=0.
   $$

4. **Complementary slackness:** $\lambda_i^*g_i(\mathbf x^*)=0$ for every inequality constraint.

Complementary slackness says each inequality constraint is either inactive ($g_i(\mathbf x^*)<0$), in which case its multiplier must be zero, or active ($g_i(\mathbf x^*)=0$), where its multiplier may be positive. For convex problems under suitable regularity, these conditions are sufficient for global optimality; with suitable constraint qualifications they are also necessary.

For the quadratic example, stationarity gives $2x-\lambda=0$, feasibility gives $x\ge1$, dual feasibility gives $\lambda\ge0$, and complementary slackness gives $\lambda(1-x)=0$. Together these yield $x^*=1$ and $\lambda^*=2$.

## Equality constraints and Lagrange multipliers

For an equality-constrained problem, the multiplier $\nu$ is unrestricted. At a regular constrained optimum, the gradient of the objective lies in the span of the gradients of the active constraints. Geometrically, the objective cannot decrease to first order along any feasible direction. Do not impose $\nu\ge0$ for equality constraints.

## Common pitfalls and IOAI checklist

- For a minimization primal problem, weak duality gives $d^*\le p^*$.
- The dual problem maximizes the dual function over dual-feasible multipliers.
- Multipliers for constraints written $g_i(x)\le0$ must satisfy $\lambda_i\ge0$; equality multipliers are unrestricted.
- Strong duality requires additional conditions; it does not hold automatically for every problem.
- KKT includes primal feasibility, dual feasibility, stationarity, and complementary slackness.

## Quick self-check

1. What inequality does weak duality guarantee for a minimization problem?
2. What sign is required for multipliers of $g_i(x)\le0$ constraints?
3. Write complementary slackness for one inequality constraint.

**Answers:** (1) $d^*\le p^*$. (2) $\lambda_i\ge0$. (3) $\lambda_i g_i(x^*)=0$.
