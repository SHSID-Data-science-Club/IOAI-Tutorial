# IOAI Guide — Calculus Foundations I: Single-Variable Derivatives

> **Goal.** Understand a derivative as a limit, calculate it reliably, and interpret it as local linear change. These ideas are prerequisites for gradients, Jacobians, and backpropagation.

## 1. Prerequisites: limits

### 1.1 What a limit means

We write

\[
\lim_{x\to a}f(x)=L
\]

when values of \(f(x)\) can be made arbitrarily close to \(L\) by taking \(x\) sufficiently close to \(a\), without requiring \(x=a\). Formally, for every \(\varepsilon>0\), there is a \(\delta>0\) such that

\[
0<|x-a|<\delta\quad\Longrightarrow\quad |f(x)-L|<\varepsilon.
\]

The value \(f(a)\) may be undefined or may differ from \(L\). A limit describes nearby behavior, not necessarily the function's value at the point.

### 1.2 Limit laws and one-sided limits

If \(\lim f(x)=L\) and \(\lim g(x)=M\) as \(x\to a\), then, wherever the expressions are defined,

\[
\begin{aligned}
\lim(f\pm g)&=L\pm M, & \lim(cf)&=cL,\\
\lim(fg)&=LM, & \lim\frac{f}{g}&=\frac{L}{M}\quad(M\ne0).
\end{aligned}
\]

For polynomials, substitute directly. For rational functions, direct substitution works when the denominator's value is nonzero.

The two-sided limit exists and equals \(L\) precisely when both one-sided limits exist and equal \(L\):

\[
\lim_{x\to a^-}f(x)=\lim_{x\to a^+}f(x)=L.
\]

### 1.3 Common limit techniques

1. **Direct substitution** when the function is continuous at the point.
2. **Factor and cancel** common factors in a \(0/0\) expression; cancel only for \(x\ne a\), then take the limit.
3. **Rationalize** radical expressions by multiplying by a conjugate.
4. **Squeeze theorem:** if \(g(x)\le f(x)\le h(x)\) near \(a\) and both bounds tend to \(L\), then \(f(x)\to L\).
5. **L'Hôpital's rule** may be used for suitable \(0/0\) or \(\infty/\infty\) forms when its hypotheses hold; it is not a rule for arbitrary quotients.

Important limits (angles in radians):

\[
\lim_{x\to0}\frac{\sin x}{x}=1,\qquad
\lim_{x\to0}\frac{1-\cos x}{x^2}=\frac12,\qquad
\lim_{x\to0}(1+x)^{1/x}=e.
\]

For example,

\[
\lim_{x\to 2}\frac{x^2-4}{x-2}
=\lim_{x\to2}\frac{(x-2)(x+2)}{x-2}=4.
\]

### 1.4 Continuity

A function is continuous at \(a\) if it is defined there and

\[
\lim_{x\to a}f(x)=f(a).
\]

Sums, products, and compositions of continuous functions remain continuous (where defined); a quotient is continuous where its denominator is nonzero. **Differentiability implies continuity**, but continuity does not imply differentiability: \(f(x)=|x|\) is continuous at \(0\), but has a corner there.

## 2. Derivative: definition and meaning

The derivative of \(f\) at \(a\) is

\[
f'(a)=\lim_{h\to0}\frac{f(a+h)-f(a)}{h},
\]

provided this limit exists. The quotient is the slope of a secant line; its limit is the tangent slope and instantaneous rate of change. Equivalent notation includes \(\frac{df}{dx}\), \(\frac{d}{dx}f(x)\), and \(y'\).

The tangent line at \((a,f(a))\) is

\[
y=f(a)+f'(a)(x-a).
\]

For small \(h\), differentiability means the function is locally approximated by a line:

\[
f(a+h)=f(a)+f'(a)h+o(h),\qquad h\to0.
\]

### 2.1 One-sided derivatives and points where a derivative fails

At an endpoint, use a right- or left-hand derivative. At an interior point, the two one-sided derivatives must agree and be finite. Common failure modes:

- **Corner:** one-sided slopes disagree, as for \(|x|\) at \(0\).
- **Cusp:** one-sided slopes diverge with opposite signs, as for \(x^{2/3}\) at \(0\).
- **Vertical tangent:** slopes become unbounded in the same signed direction, as for \(x^{1/3}\) at \(0\); the ordinary finite derivative does not exist.
- **Discontinuity:** differentiability is impossible because differentiability implies continuity.

### 2.2 A first-principles example

For \(f(x)=x^2\),

\[
\begin{aligned}
f'(x)&=\lim_{h\to0}\frac{(x+h)^2-x^2}{h}\\
&=\lim_{h\to0}\frac{2xh+h^2}{h}
=\lim_{h\to0}(2x+h)=2x.
\end{aligned}
\]

This is the core pattern: expand, simplify/cancel, then take the limit.

## 3. Differentiation rules

Assume each expression is differentiable on the domain considered.

| Rule | Formula |
|---|---|
| Constant | \(\frac{d}{dx}c=0\) |
| Power | \(\frac{d}{dx}x^p=px^{p-1}\), where the real-valued expression is defined and differentiable |
| Constant multiple | \((cf)'=cf'\) |
| Sum/difference | \((f\pm g)'=f'\pm g'\) |
| Product | \((fg)'=f'g+fg'\) |
| Quotient | \((f/g)'=(f'g-fg')/g^2\), \(g\ne0\) |
| Chain rule | \((f\circ g)'(x)=f'(g(x))g'(x)\) |

For a product of many factors,

\[
\frac{d}{dx}\prod_{i=1}^{n}u_i(x)
=\sum_{i=1}^{n}u_i'(x)\prod_{j\ne i}u_j(x).
\]

The power rule is often used for integer and rational exponents. Be careful at points where a power expression is not real-valued or where its derivative is singular.

## 4. Common derivatives

### 4.1 Exponential and logarithmic

\[
\begin{aligned}
\frac{d}{dx}e^x&=e^x,&
\frac{d}{dx}a^x&=a^x\ln a\quad(a>0),\\
\frac{d}{dx}\ln x&=\frac1x\quad(x>0),&
\frac{d}{dx}\log_a x&=\frac{1}{x\ln a}\quad(a>0, a\ne1).
\end{aligned}
\]

### 4.2 Trigonometric

\[
\begin{aligned}
(\sin x)'&=\cos x,&(\cos x)'&=-\sin x,\\
(\tan x)'&=\sec^2x,&(\cot x)'&=-\csc^2x,\\
(\sec x)'&=\sec x\tan x,&(\csc x)'&=-\csc x\cot x.
\end{aligned}
\]

### 4.3 Inverse trigonometric

\[
\begin{aligned}
(\arcsin x)'&=\frac1{\sqrt{1-x^2}},&
(\arccos x)'&=-\frac1{\sqrt{1-x^2}},\\
(\arctan x)'&=\frac1{1+x^2},&
(\operatorname{arccot}x)'&=-\frac1{1+x^2}.
\end{aligned}
\]

For the real-valued principal branches, the first two formulas apply on \(-1<x<1\). Notation such as \(\sin^{-1}x\) commonly means \(\arcsin x\), not \(1/\sin x\).

## 5. Second and higher derivatives

The second derivative is \(f''=(f')'\); the \(k\)-th derivative is written \(f^{(k)}\) or \(d^kf/dx^k\). It describes how the rate of change itself changes. In a time model, position \(p(t)\), velocity \(v(t)=p'(t)\), acceleration \(a(t)=p''(t)\), and jerk \(j(t)=p^{(3)}(t)\).

## 6. Taylor approximation: a bridge to numerical optimization

If \(f\) has enough derivatives near \(a\),

\[
f(a+h)=f(a)+f'(a)h+\frac{f''(a)}{2!}h^2+\cdots+\frac{f^{(k)}(a)}{k!}h^k+R_k(h).
\]

The first-order approximation is the tangent line. The second-order approximation incorporates curvature. When \(f\) is sufficiently smooth, the local expansion helps analyze approximation error and optimization algorithms.

A central finite-difference approximation is

\[
f'(a)\approx\frac{f(a+h)-f(a-h)}{2h},
\]

which is often more accurate than a one-sided difference for a suitably small step \(h\). Too-small \(h\) can amplify floating-point rounding error.

## 7. Worked examples

### Example A: product and chain rule

For \(f(x)=x^2\sin(3x)\),

\[
f'(x)=2x\sin(3x)+3x^2\cos(3x).
\]

### Example B: logarithmic differentiation

For \(y=x^x\), \(x>0\), take logs: \(\ln y=x\ln x\). Then

\[
\frac{y'}y=\ln x+1\quad\Rightarrow\quad y'=x^x(\ln x+1).
\]

### Example C: derivative from the definition

For \(f(x)=1/x\), with \(x\ne0\),

\[
f'(x)=\lim_{h\to0}\frac{1/(x+h)-1/x}{h}
=\lim_{h\to0}\frac{-1}{x(x+h)}=-\frac1{x^2}.
\]

## 8. Checklist and practice

Before differentiating, identify the outer structure: sum, product, quotient, or composition. Then apply the corresponding rule and check the domain.

1. Use the definition to derive the derivative of \(f(x)=3x+2\).
2. Find the derivative of \(g(x)=\ln(1+x^2)\).
3. Find and classify differentiability at \(x=0\) for \(h(x)=|x|\).
4. Find the linear approximation of \(e^x\) at \(x=0\).

**Answers:** 1. \(3\). 2. \(2x/(1+x^2)\). 3. Continuous but not differentiable (left slope \(-1\), right slope \(1\)). 4. \(e^x\approx1+x\) near zero.

## 9. Source-note corrections and scope

These notes reorganize the supplied limits/derivatives material. The limit prerequisites are intentionally included here because the derivative is defined by a limit. Parametric differentiation and inverse-function differentiation can be treated as applications of the chain rule in the third pile; integral techniques and differential equations are outside this chapter's scope.
