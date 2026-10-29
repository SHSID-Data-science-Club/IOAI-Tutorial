# Variance, Covariance

> **IOAI Guide — Probability & Statistics**

> **Goal.** Quantify dispersion, pairwise co-variation, and multivariate uncertainty.

## Prerequisites and notation

Know expectation $E[X]$ and expectation of products. Variance is the expected squared deviation from the mean; covariance applies the same centering idea to two variables.

## Variance and standard deviation

Variance measures squared spread around the mean:

$$
\operatorname{Var}(X)=E[(X-E[X])^2]=E[X^2]-(E[X])^2.
$$

The second form is often easier computationally. Standard deviation is $\sigma_X=\sqrt{\operatorname{Var}(X)}$ and returns to the units of $X$. Variance is nonnegative, and it is zero precisely when $X$ is constant with probability one.

For constants $a,b$,

$$
\operatorname{Var}(aX+b)=a^2\operatorname{Var}(X).
$$

Adding a constant shifts a variable but does not change its spread; scaling by $a$ scales variance by $a^2$.

## Population variance versus sample variance

For a complete finite population or a probability distribution, variance is defined relative to the true mean. Given data $x_1,\ldots,x_n$, the empirical variance using the sample mean is often written

$$
s_n^2=\frac{1}{n-1}\sum_{i=1}^n(x_i-\bar{x})^2.
$$

The $n-1$ denominator gives an unbiased estimator of the population variance when the observations are i.i.d. with finite variance. Dividing by $n$ instead computes the variance of the observed data when viewed as an empirical distribution. Neither denominator should be selected without knowing what quantity is being estimated.

## Covariance

Covariance describes how two variables vary together:

$$
\operatorname{Cov}(X,Y)=E[(X-E[X])(Y-E[Y])]=E[XY]-E[X]E[Y].
$$

Positive covariance means above-average values of one variable tend to pair with above-average values of the other; negative covariance indicates an opposite tendency. Covariance depends on measurement units, so its magnitude alone is difficult to compare across datasets.

If $X$ and $Y$ are independent and the expectations exist, their covariance is zero. The converse is generally false: zero covariance does not imply independence.

## Variance of a sum

The general identity is

$$
\operatorname{Var}(X+Y)=\operatorname{Var}(X)+\operatorname{Var}(Y)+2\operatorname{Cov}(X,Y).
$$

For constants $a_i$ and random variables $X_i$,

$$
\operatorname{Var}\!\left(\sum_i a_iX_i\right)
=\sum_i a_i^2\operatorname{Var}(X_i)+2\sum_{i<j}a_i a_j\operatorname{Cov}(X_i,X_j).
$$

If the variables are pairwise uncorrelated, the covariance terms vanish. Independence is sufficient for this, but stronger than necessary.

## Correlation and covariance matrix

The correlation coefficient is

$$
\rho_{XY}=\frac{\operatorname{Cov}(X,Y)}{\sigma_X\sigma_Y},
$$

when both standard deviations are nonzero. It lies in $[-1,1]$ and is invariant under positive changes in scale. Correlation measures linear association; zero correlation does not rule out nonlinear dependence.

For a random vector $\mathbf X=(X_1,\ldots,X_d)^\top$, its covariance matrix is

$$
\Sigma=E\!\left[(\mathbf X-E[\mathbf X])(\mathbf X-E[\mathbf X])^\top\right].
$$

Diagonal entries are variances and off-diagonal entries are covariances. The matrix is symmetric and positive semidefinite because $\mathbf a^\top\Sigma\mathbf a=\operatorname{Var}(\mathbf a^\top\mathbf X)\ge0$. Covariance matrices are central to multivariate Gaussian models, feature scaling, and uncertainty analysis.

## Common pitfalls and IOAI checklist

- Variance uses squared deviations, so $\operatorname{Var}(aX+b)=a^2\operatorname{Var}(X)$.
- Remember the covariance term in the variance of a sum.
- Zero covariance does not in general imply independence.
- The unbiased sample variance uses denominator $n-1$; the empirical variance uses denominator $n$.
- A covariance matrix is symmetric positive semidefinite; its diagonal contains variances.

## Quick self-check

1. If $\operatorname{Var}(X)=4$, find $\operatorname{Var}(3X+7)$.
2. If $\operatorname{Var}(X)=2$, $\operatorname{Var}(Y)=5$, and $\operatorname{Cov}(X,Y)=1$, find $\operatorname{Var}(X+Y)$.
3. What appears on the diagonal of a covariance matrix?

**Answers:** (1) $36$. (2) $2+5+2(1)=9$. (3) The component variances.
