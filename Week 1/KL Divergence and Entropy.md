# Kullback-Leibler (KL) Divergence

## Introduction

In probability theory, statistics, information theory, and machine learning, we often need to compare two probability distributions.

Suppose:

* $P(x)$ represents the true distribution of data.
* $Q(x)$ represents an approximation of that distribution.

A natural question arises:

> How different is $Q$ from $P$?

The most widely used measure for answering this question is the **Kullback-Leibler (KL) Divergence**, often called **relative entropy**.

KL divergence plays a central role in:

* Variational Autoencoders (VAEs)
* Bayesian Statistics
* Information Theory
* Reinforcement Learning
* Generative Models
* Variational Inference

---

# Motivation

Imagine two weather forecasters.

Forecaster A predicts:

| Weather | Probability |
| ------- | ----------- |
| Sunny   | 0.8         |
| Rainy   | 0.2         |

Forecaster B predicts:

| Weather | Probability |
| ------- | ----------- |
| Sunny   | 0.6         |
| Rainy   | 0.4         |

Both describe the same event but assign different probabilities.

KL divergence measures the amount of information lost when we use one distribution instead of another.

---

# Information Content

Before understanding KL divergence, we need the concept of information.

If an event occurs with probability $p$, its information content is:

$$ I(x) = -\log p(x) $$

Rare events carry more information.

For example:

$$ -\log(0.9) < -\log(0.01) $$

Observing a very unlikely event is more surprising and therefore contains more information.

---

# Entropy

Entropy measures the average uncertainty of a probability distribution.

For a discrete random variable:

$$ H(P) = -\sum_x P(x)\log P(x) $$

Interpretation:

* High entropy → high uncertainty.
* Low entropy → low uncertainty.

For example:

| Distribution | Entropy |
| ------------ | ------- |
| (0.5, 0.5)   | High    |
| (0.99, 0.01) | Low     |

---

# Cross Entropy

Suppose the true distribution is $P$ but we model it using $Q$.

The expected number of bits required becomes:

$$ H(P,Q) = -\sum_x P(x)\log Q(x) $$

This quantity is called **cross entropy**.

Cross entropy is always at least as large as the true entropy.

---

# Deriving KL Divergence

The extra information required because we used $Q$ instead of $P$ is:

$$ D_{KL}(P||Q) = H(P,Q) - H(P) $$

Substituting the formulas:

$$ D_{KL}(P||Q) = -\sum_x P(x)\log Q(x) + \sum_x P(x)\log P(x) $$

Combining terms:

$$ D_{KL}(P||Q) = \sum_x P(x)\log\frac{P(x)}{Q(x)} $$

This is the standard definition of KL divergence.

---

# KL Divergence Formula

For discrete distributions:

$$ D_{KL}(P||Q) = \sum_x P(x)\log\frac{P(x)}{Q(x)} $$

For continuous distributions:

$$ D_{KL}(P||Q) = \int P(x)\log\frac{P(x)}{Q(x)},dx $$

---

# Interpretation

KL divergence answers the question:

> How much extra information is needed when distribution $Q$ is used to represent data actually generated from distribution $P$?

If:

$$ D_{KL}(P||Q)=0 $$

then:

$$ P(x)=Q(x) $$

for every value of $x$.

The larger the KL divergence, the more different the two distributions are.

---

# Important Properties

## 1. Non-Negativity

KL divergence is always non-negative:

$$ D_{KL}(P||Q)\ge 0 $$

This result follows from Gibbs' Inequality.

---

## 2. Zero Only When Distributions Match

$$ D_{KL}(P||Q)=0 \iff P=Q $$

Thus, identical distributions have zero divergence.

---

## 3. Not Symmetric

In general:

$$ D_{KL}(P||Q)\ne D_{KL}(Q||P) $$

This means:

$$ D_{KL}(P||Q) \ne D_{KL}(Q||P) $$

Therefore KL divergence is **not a true distance metric**.

---

## 4. Triangle Inequality Does Not Hold

Generally:

$$ D_{KL}(P||R)\le D_{KL}(P||Q)+D_{KL}(Q||R) $$

is not true.

Hence KL divergence is not a mathematical metric.

---

# Numerical Example

Consider:

| Outcome | P(x) | Q(x) |
| ------- | ---- | ---- |
| Heads   | 0.8  | 0.6  |
| Tails   | 0.2  | 0.4  |

Using the formula:

$$ D_{KL}(P||Q) = 0.8\log\frac{0.8}{0.6} + 0.2\log\frac{0.2}{0.4} $$

Computing:

$$ D_{KL}(P||Q) \approx 0.0915 $$

This indicates that the approximation $Q$ differs from $P$ but not drastically.

---

# Forward vs Reverse KL

There are two common forms.

## Forward KL

$$ D_{KL}(P||Q) $$

Penalty is large when $Q$ misses regions where $P$ has probability mass.

This tends to produce **mode-covering** behavior.

---

## Reverse KL

$$ D_{KL}(Q||P) $$

Penalty is large when $Q$ places mass where $P$ has little probability.

This tends to produce **mode-seeking** behavior.

---

# KL Divergence in Machine Learning

KL divergence appears everywhere in machine learning.

Common applications include:

* Variational Autoencoders
* Bayesian Inference
* Reinforcement Learning
* Language Models
* Knowledge Distillation
* Generative Modeling

The objective often involves minimizing:

$$ D_{KL}(P||Q) $$

so that the learned distribution becomes close to the target distribution.

---

# KL Divergence in Variational Autoencoders

A Variational Autoencoder learns:

$$ q(z|x) $$

to approximate the true posterior:

$$ p(z|x) $$

The VAE objective contains a KL penalty:

$$ D_{KL}(q(z|x)||p(z)) $$

where:

* $q(z|x)$ is the encoder distribution.
* $p(z)$ is the prior distribution.

This term prevents the latent space from becoming arbitrary and encourages it to resemble a simple prior distribution.

---

# Closed-Form KL Divergence for Gaussian Distributions

Suppose:

$$ q(z)=\mathcal{N}(\mu,\sigma^2) $$

and

$$ p(z)=\mathcal{N}(0,1) $$

Then:

$$ D_{KL}(q||p) = \frac{1}{2}\left(\mu^2+\sigma^2-\log\sigma^2-1\right) $$

For multiple dimensions:

$$ D_{KL}(q||p) = \frac{1}{2}\sum_{i=1}^{d}\left(\mu_i^2+\sigma_i^2-\log\sigma_i^2-1\right) $$

This formula is used directly in VAE implementations.

---

# Relationship Between Entropy, Cross Entropy and KL Divergence

The three quantities are connected through:

$$ H(P,Q)=H(P)+D_{KL}(P||Q) $$

Therefore:

$$ D_{KL}(P||Q)=H(P,Q)-H(P) $$

KL divergence measures the additional uncertainty introduced by using the wrong distribution.

---

# Intuition in One Sentence

KL divergence measures how much information is lost when probability distribution $Q$ is used to approximate probability distribution $P$.

---

# Key Takeaways

* KL divergence compares two probability distributions.
* It measures information loss.
* It is always non-negative.
* It equals zero only when the distributions are identical.
* It is not symmetric.
* It is not a distance metric.
* It is fundamental to information theory and machine learning.
* Variational Autoencoders use KL divergence to regularize the latent space.
* Entropy, cross entropy, and KL divergence are closely related through $$ H(P,Q)=H(P)+D_{KL}(P||Q) $$.
