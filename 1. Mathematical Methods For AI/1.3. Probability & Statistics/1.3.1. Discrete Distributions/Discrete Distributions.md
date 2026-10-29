# Discrete Distributions

> **IOAI Guide — Probability & Statistics**

> **Goal.** Model random counts with probability mass functions and select a distribution whose assumptions match the experiment.

## Prerequisites and notation

A probability mass function (PMF) assigns nonnegative probabilities to discrete outcomes, and the probabilities sum to 1. Be comfortable with conditional probability, independence, factorials, and combinations.

A discrete random variable takes values in a finite or countable set. Its **probability mass function (PMF)** is

$$
p_X(x)=P(X=x),\qquad p_X(x)\ge 0,\qquad \sum_x p_X(x)=1.
$$

Probabilities are found by adding masses: $P(X\in S)=\sum_{x\in S}p_X(x)$. A CDF accumulates these masses: $F_X(x)=\sum_{t\le x}p_X(t)$.

## Bernoulli distribution

A Bernoulli random variable records one success/failure trial: $X\in\{0,1\}$ and $P(X=1)=p$. Write $X\sim\operatorname{Bernoulli}(p)$. Then

$$
P(X=x)=p^x(1-p)^{1-x},\quad x\in\{0,1\},
$$

with $E[X]=p$ and $\operatorname{Var}(X)=p(1-p)$. This is a useful model for a binary label or one successful event.

## Binomial distribution

If $n$ trials are independent and each has the same success probability $p$, the number of successes $X$ follows $\operatorname{Binomial}(n,p)$:

$$
P(X=k)=\binom{n}{k}p^k(1-p)^{n-k},\quad k=0,1,\ldots,n.
$$

Its mean is $np$ and variance is $np(1-p)$. The assumptions matter: fixed trial count, independent trials, two outcomes per trial, and a constant success probability. The coefficient $\binom{n}{k}=n!/[k!(n-k)!]$ counts which $k$ trials succeed.

## Geometric distribution

With independent Bernoulli trials of success probability $p$, let $X$ be the **trial number of the first success**. Under this convention, $X\in\{1,2,\ldots\}$ and

$$
P(X=k)=(1-p)^{k-1}p,\qquad E[X]=\frac1p,\qquad \operatorname{Var}(X)=\frac{1-p}{p^2}.
$$

Some texts instead count failures before the first success, starting at zero; check the convention before using a formula. The geometric distribution is memoryless: $P(X>m+n\mid X>m)=P(X>n)$.

## Poisson distribution

A Poisson random variable models a count over a fixed interval when events occur at an approximately constant rate $\lambda$ and independently:

$$
P(X=k)=e^{-\lambda}\frac{\lambda^k}{k!},\quad k=0,1,2,\ldots
$$

Both mean and variance equal $\lambda$. A binomial distribution with large $n$, small $p$, and $np\approx\lambda$ is approximated by $\operatorname{Poisson}(\lambda)$.

## Hypergeometric distribution (sampling without replacement)

Suppose a population has $N$ items, of which $K$ are marked, and we sample $n$ items uniformly without replacement. The number of marked items $X$ has

$$
P(X=k)=\frac{\binom{K}{k}\binom{N-K}{n-k}}{\binom{N}{n}},
$$

for feasible $k$. Unlike the binomial model, draws are dependent because each item is removed after it is drawn.

## Choosing a discrete model

- **Bernoulli:** one binary outcome.
- **Binomial:** successes in a fixed number of independent, equal-probability trials.
- **Geometric:** number of trials until the first success.
- **Poisson:** event count in an interval under a rate model.
- **Hypergeometric:** marked items in a sample drawn without replacement.

A model is an assumption about the data-generating process, not just a formula that can be fitted to any count.

## Common pitfalls and IOAI checklist

- Confirm whether trials are independent and whether sampling is with or without replacement.
- The Binomial model requires a fixed number of trials and a constant success probability.
- The Geometric convention here counts the trial on which the first success occurs, so support begins at 1.
- A Poisson model counts events over an interval; its rate parameter is the expected count for that interval.
- A PMF sums to 1 over all possible outcomes.

## Quick self-check

1. If $X\sim\operatorname{Binomial}(12,0.25)$, what are $E[X]$ and $\operatorname{Var}(X)$?
2. Which distribution models the number of marked objects in a sample drawn without replacement?
3. Under the trial-number convention, what is $P(X=3)$ for $X\sim\operatorname{Geometric}(p)$?

**Answers:** (1) $3$ and $12(0.25)(0.75)=2.25$. (2) Hypergeometric. (3) $(1-p)^2p$.
