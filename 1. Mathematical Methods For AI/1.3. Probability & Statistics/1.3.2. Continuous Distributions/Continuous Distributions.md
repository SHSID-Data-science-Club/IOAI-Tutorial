# Continuous Distributions

> **IOAI Guide — Probability & Statistics**

> **Goal.** Use probability densities and CDFs to model continuous measurements and waiting times.

## Prerequisites and notation

Know definite integrals, derivatives, exponentials, and the meaning of a density. A PDF integrates to 1; interval probabilities are areas under that density.

A continuous random variable is described by a **probability density function (PDF)** $f_X(x)\ge0$ satisfying

$$
\int_{-\infty}^{\infty} f_X(x)\,dx=1,\qquad P(a\le X\le b)=\int_a^b f_X(x)\,dx.
$$

The CDF is $F_X(x)=\int_{-\infty}^{x}f_X(t)\,dt$. Where differentiable, $F_X'(x)=f_X(x)$. For a continuous variable, $P(X=x)=0$ at every single point; probabilities concern intervals, not the height of the density. A PDF can exceed $1$ if its support is sufficiently narrow; its **area** must equal $1$.

## Uniform distribution

If $X\sim\operatorname{Uniform}(a,b)$, then

$$
f_X(x)=\begin{cases}\frac{1}{b-a},&a\le x\le b,\\0,&\text{otherwise},\end{cases}
\quad E[X]=\frac{a+b}{2},\quad \operatorname{Var}(X)=\frac{(b-a)^2}{12}.
$$

Every interval of a given length inside $[a,b]$ has equal probability.

## Exponential distribution

For a waiting time with rate $\lambda>0$, $X\sim\operatorname{Exponential}(\lambda)$ has

$$
f_X(x)=\lambda e^{-\lambda x}\quad (x\ge0),\qquad F_X(x)=1-e^{-\lambda x},
$$

and $E[X]=1/\lambda$, $\operatorname{Var}(X)=1/\lambda^2$. The exponential distribution is memoryless: $P(X>s+t\mid X>s)=P(X>t)$. Here $\lambda$ is a **rate**, not a scale; some software APIs parameterize the same distribution by scale $1/\lambda$.

## Normal distribution

The normal (Gaussian) distribution $X\sim\mathcal N(\mu,\sigma^2)$ has density

$$
f_X(x)=\frac{1}{\sqrt{2\pi\sigma^2}}\exp\!\left(-\frac{(x-\mu)^2}{2\sigma^2}\right).
$$

Its mean is $\mu$ and variance is $\sigma^2$ (so standard deviation is $\sigma$). Standardize using

$$
Z=\frac{X-\mu}{\sigma}\sim\mathcal N(0,1),\qquad P(X\le x)=\Phi\!\left(\frac{x-\mu}{\sigma}\right),
$$

where $\Phi$ is the standard normal CDF. The CDF generally has no elementary closed form, so numerical libraries or tables are used.

## Density versus probability

A PDF value $f_X(x)$ is a density, not $P(X=x)$. For a small interval $[x,x+\Delta x]$, its probability is approximately $f_X(x)\Delta x$ when the density changes little over the interval. For continuous variables, $P(a<X<b)=P(a\le X\le b)$ because endpoints have probability zero.

## Common pitfalls and IOAI checklist

- Integrate a PDF over an interval to obtain probability; its height is not itself a probability.
- A continuous random variable satisfies $P(X=x)=0$ for every point $x$.
- Check the parameterization: an Exponential distribution may use a rate $\lambda$ or a scale $1/\lambda$.
- For a Normal distribution, $\sigma$ is the standard deviation and $\sigma^2$ is the variance.
- Standardize with $Z=(X-\mu)/\sigma$, not by dividing by the variance.

## Quick self-check

1. If $X\sim\operatorname{Uniform}(2,8)$, find its mean and variance.
2. If $X\sim\operatorname{Exponential}(3)$ with rate 3, find $P(X>2)$.
3. What is $P(X=0)$ for a continuous random variable with a PDF?

**Answers:** (1) Mean $5$, variance $3$. (2) $e^{-6}$. (3) $0$.
