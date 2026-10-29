# Bayes' Rule

> **IOAI Guide — Probability & Statistics**

> **Goal.** Update the probability of a hypothesis after observing evidence, while correctly accounting for the prior and base rate.

## Prerequisites and notation

Know conditional probability $P(A\mid B)=P(A\cap B)/P(B)$ and the law of total probability. Bayes’ Rule reverses the conditioning direction.

Bayes' rule reverses a conditional probability:

$$
P(A\mid B)=\frac{P(B\mid A)P(A)}{P(B)},\qquad P(B)>0.
$$

Here $P(A)$ is the **prior**, $P(B\mid A)$ is the likelihood of the evidence under $A$, and $P(A\mid B)$ is the **posterior**. If $A$ and $A^c$ form a partition, the denominator can be expanded using total probability:

$$
P(B)=P(B\mid A)P(A)+P(B\mid A^c)P(A^c).
$$

For multiple mutually exclusive hypotheses $H_i$ that cover all possibilities,

$$
P(H_i\mid B)=\frac{P(B\mid H_i)P(H_i)}{\sum_jP(B\mid H_j)P(H_j)}.
$$

## Worked example: a positive screening result

Suppose a condition affects $1\%$ of a population. A test has sensitivity $99\%$ (positive when the condition is present) and false-positive rate $5\%$ (positive when it is absent). Let $D$ mean the condition is present and $+$ mean a positive result. Then

$$
P(D\mid +)=\frac{P(+\mid D)P(D)}{P(+\mid D)P(D)+P(+\mid D^c)P(D^c)}
=\frac{0.99(0.01)}{0.99(0.01)+0.05(0.99)}=\frac16\approx0.167.
$$

Even a sensitive test does not make every positive result a true positive when the condition is rare. The base rate matters. In this example, most people do not have the condition, so the false-positive rate applies to a much larger group.

## Naive Bayes connection

A Naive Bayes classifier applies Bayes' rule to predict a class $C$ from features $x_1,\ldots,x_d$:

$$
P(C\mid x_1,\ldots,x_d)\propto P(C)P(x_1,\ldots,x_d\mid C).
$$

Its simplifying assumption is conditional independence of features given the class:

$$
P(x_1,\ldots,x_d\mid C)=\prod_{j=1}^d P(x_j\mid C).
$$

The features need not be independent overall. This assumption is often unrealistic but can still produce useful classifiers. For numerical stability, implementations typically add log-probabilities rather than multiply many tiny probabilities.

## Common pitfalls and IOAI checklist

- Do not reverse $P(A\mid B)$ and $P(B\mid A)$; they answer different questions.
- The denominator is the total probability of the observed evidence.
- Base rates matter, especially when the event being predicted is rare.
- In Naive Bayes, features are assumed conditionally independent given the class, not necessarily independent overall.
- The posterior probabilities across a complete set of hypotheses must sum to 1.

## Quick self-check

1. State Bayes' Rule for events $A$ and $B$.
2. Why can a test with high sensitivity still have a modest positive predictive value for a rare condition?
3. What is the conditional-independence assumption in Naive Bayes?

**Answers:** (1) $P(A\mid B)=P(B\mid A)P(A)/P(B)$. (2) False positives can arise from a much larger unaffected population. (3) $P(x_1,\ldots,x_d\mid C)=\prod_j P(x_j\mid C)$.
