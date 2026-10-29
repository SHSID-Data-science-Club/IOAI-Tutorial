# Mean

> **IOAI Guide — Probability & Statistics**

> **Goal.** Compute expected values, exploit linearity, and understand how sample averages behave.

## Prerequisites and notation

For discrete variables, expectation is a sum over outcomes; for continuous variables, it is an integral against the density. Know basic summation and integration.

The **expected value** is a probability-weighted average. For a discrete variable,

$$
E[X]=\sum_x x\,p_X(x),
$$

and for a continuous variable with density $f_X$,

$$
E[X]=\int_{-\infty}^{\infty}x f_X(x)\,dx,
$$

provided the expectation is well-defined (for example, $E[|X|]<\infty$). The expectation need not be a value that $X$ can actually take.

## Functions of a random variable (LOTUS)

For a function $g$, the law of the unconscious statistician gives

$$
E[g(X)]=\sum_x g(x)p_X(x)\quad\text{(discrete)},
\qquad E[g(X)]=\int_{-\infty}^{\infty}g(x)f_X(x)\,dx\quad\text{(continuous)}.
$$

This lets us calculate $E[X^2]$ directly without first finding the distribution of $X^2$.

## Linearity of expectation

For constants $a,b$ and random variables with finite expectations,

$$
E[aX+bY+c]=aE[X]+bE[Y]+c.
$$

**No independence assumption is needed.** This is exceptionally useful for sums of indicator variables. If $I_i=1$ when event $A_i$ occurs and $0$ otherwise, then $E[I_i]=P(A_i)$, so the expected number of events that occur is $E[\sum_i I_i]=\sum_i P(A_i)$.

For a binomial variable viewed as the sum of $n$ independent Bernoulli variables, $X=\sum_i X_i$, we get $E[X]=np$. Linearity is still true if those indicators are dependent, though the variance calculation will then need covariance terms.

## Conditional expectation

$E[X\mid A]$ is the expected value when event $A$ is known to have happened. The law of total expectation for a partition $A_1,\ldots,A_k$ is

$$
E[X]=\sum_{i=1}^k E[X\mid A_i]P(A_i).
$$

This is an averaging rule: average each conditional mean using the probability of the corresponding case.

## Sample mean

For observed data $x_1,\ldots,x_n$, the sample mean is

$$
\bar{x}=\frac1n\sum_{i=1}^n x_i.
$$

If the observations are independent and identically distributed with finite mean $\mu$, the law of large numbers says $\bar X$ approaches $\mu$ as sample size grows. The central limit theorem says that, under common regularity conditions, the standardized sample mean is approximately normal for large $n$:

$$
\frac{\bar X-\mu}{\sigma/\sqrt n}\ \approx\ \mathcal N(0,1).
$$

The approximation is not automatically accurate for tiny samples or very heavy-tailed data.

## Common pitfalls and IOAI checklist

- Expectation is a probability-weighted average, not necessarily a value the variable can take.
- Use the Law of the Unconscious Statistician (LOTUS) to calculate $E[g(X)]$ directly.
- Linearity of expectation does not require independence.
- Distinguish a theoretical expectation $E[X]$ from an observed sample mean $\bar x$.
- The Central Limit Theorem is an approximation under conditions, not a guarantee for every small sample.

## Quick self-check

1. If $P(X=0)=0.4$ and $P(X=5)=0.6$, find $E[X]$.
2. If $E[X]=2$ and $E[Y]=3$, find $E[4X-Y+1]$.
3. Does linearity of expectation require independence?

**Answers:** (1) $3$. (2) $4(2)-3+1=6$. (3) No.
