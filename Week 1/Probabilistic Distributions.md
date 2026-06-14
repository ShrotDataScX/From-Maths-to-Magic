# Probability Foundations: Normal Distribution, Bernoulli Distribution, Covariance Matrix, and Correlation

Probability and statistics provide the mathematical language for dealing with uncertainty. Whether we are building machine learning models, analyzing stock markets, designing experiments, or studying natural phenomena, a few concepts appear repeatedly:

1. Normal Distribution
2. Bernoulli Distribution
3. Covariance
4. Covariance Matrix
5. Correlation

Understanding these concepts deeply provides the foundation for advanced topics such as Linear Regression, Principal Component Analysis (PCA), Bayesian Statistics, Neural Networks, and Quantitative Finance.

---

# 1. Normal Distribution

The Normal Distribution, also called the Gaussian Distribution or Bell Curve, is the most important continuous probability distribution in statistics.

Many real-world quantities approximately follow a normal distribution:

* Human heights
* IQ scores
* Measurement errors
* Sensor noise
* Financial returns (approximately)
* Biological measurements

Its probability density function (PDF) is

$$
f(x)=\frac{1}{\sqrt{2\pi\sigma^2}}
\exp\left(
-\frac{(x-\mu)^2}{2\sigma^2}
\right)
$$

where:

* `\mu` = mean
* `\sigma^2` = variance
* `\sigma` = standard deviation

---

## Understanding the Parameters

### Mean

The parameter `\mu` determines the center of the distribution.

If `\mu` increases:

* The entire curve shifts right.

If `\mu` decreases:

* The entire curve shifts left.

The expected value is

$$
E[X]=\mu
$$

---

### Variance

The parameter `\sigma^2` determines the spread.

A larger variance produces a wider bell curve.

A smaller variance produces a narrower bell curve.

The variance is

$$
Var(X)=\sigma^2
$$

and the standard deviation is

$$
\sigma=\sqrt{Var(X)}
$$

---

## Why Is the Normal Distribution So Important?

One major reason is the Central Limit Theorem.

The theorem states that under very general conditions, the sum or average of many independent random variables becomes approximately normal.

This explains why normal distributions appear everywhere in nature and engineering.

---

## Standard Normal Distribution

A special normal distribution is

$$
N(0,1)
$$

which has

$$
\mu=0
$$

and

$$
\sigma^2=1
$$

Its PDF is

$$
f(z)=
\frac{1}{\sqrt{2\pi}}
e^{-z^2/2}
$$

This distribution is called the Standard Normal Distribution.

---

## Standardisation

Suppose

$$
X\sim N(\mu,\sigma^2)
$$

We can transform it into a standard normal variable using

$$
Z=\frac{X-\mu}{\sigma}
$$

Then

$$
Z\sim N(0,1)
$$

This process is called standardisation or computing a z-score.

---

## Why Standardise?

Different normal distributions have different means and variances.

Instead of maintaining separate probability tables for every distribution, we convert everything to a standard normal distribution.

For example,

$$
X\sim N(100,25)
$$

To find

$$
P(X<110)
$$

compute

$$
Z=
\frac{110-100}{5}=2
$$

Then

$$
P(X<110)=P(Z<2)
$$

which can be looked up from a standard normal table.

---

## The 68-95-99.7 Rule

A remarkable property of normal distributions is:

### One Standard Deviation

$$
P(|X-\mu|<\sigma)\approx 0.68
$$

Approximately 68% of observations lie within one standard deviation of the mean.

---

### Two Standard Deviations

$$
P(|X-\mu|<2\sigma)\approx 0.95
$$

Approximately 95% lie within two standard deviations.

---

### Three Standard Deviations

$$
P(|X-\mu|<3\sigma)\approx 0.997
$$

Approximately 99.7% lie within three standard deviations.

---

## Linear Combinations Remain Normal

One of the most powerful properties of the normal distribution is:

If

$$
X\sim N(\mu_X,\sigma_X^2)
$$

and

$$
Y\sim N(\mu_Y,\sigma_Y^2)
$$

are independent, then

$$
aX+bY\simN\left(a\mu_X+b\mu_Y,a^2\sigma_X^2+b^2\sigma_Y^2\right)
$$

---

### Mean of the Combination

Using linearity of expectation,

$$
E[aX+bY]
========

aE[X]+bE[Y]
$$

which gives

$$
a\mu_X+b\mu_Y
$$

---

### Variance of the Combination

Using independence,

$$
Var(aX+bY)
==========

a^2Var(X)+b^2Var(Y)
$$

which becomes

$$
a^2\sigma_X^2+b^2\sigma_Y^2
$$

This property is heavily used in finance, signal processing, and machine learning.

---

# 2. Bernoulli Distribution

The Bernoulli Distribution is the simplest probability distribution.

It represents a single experiment with only two outcomes:

* Success
* Failure

Examples:

* Coin toss
* Pass/fail exam
* Email spam/not spam
* Customer buys/does not buy

---

## Definition

A Bernoulli random variable takes values

$$
X\in{0,1}
$$

where

$$
P(X=1)=p
$$

and

$$
P(X=0)=1-p
$$

The parameter `p` is the probability of success.

---

## Probability Mass Function

The PMF can be written compactly as

$$
P(X=x)=p^x(1-p)^{1-x}\quadx\in{0,1}
$$

---

## Mean

Using the definition of expectation,

$$
E[X]=1\cdot p+0\cdot(1-p)
$$

Therefore

$$
E[X]=p
$$

---

## Interpretation of the Mean

Suppose

$$
p=0.8
$$

The expected value is

$$
E[X]=0.8
$$

This does not mean the outcome is 0.8.

It means that over many repeated trials, the average outcome approaches 0.8.

---

## Variance

Since

$$
X\in{0,1}
$$

we have

$$
X^2=X
$$

Therefore

$$
E[X^2]=p
$$

Using

$$
Var(X)=
## E[X^2]
(E[X])^2
$$

gives

$$
Var(X)=p-p^2
$$

or

$$
Var(X)=p(1-p)
$$

---

## Interpretation of Variance

Variance measures uncertainty.

When

$$
p=0
$$

or

$$
p=1
$$

there is no uncertainty:

$$
Var(X)=0
$$

The outcome is always known.

The maximum variance occurs at

$$
p=\frac12
$$

giving

$$
Var(X)=\frac14
$$

This is the most uncertain case.

---

## Bernoulli in Machine Learning

Bernoulli variables appear everywhere:

* Binary classification
* Logistic regression
* Neural network outputs
* Reinforcement learning actions
* Spam detection

Many machine learning models ultimately predict a Bernoulli probability.

---

# 3. Covariance

Covariance measures how two random variables move together.

Suppose we have random variables

$$
X
$$

and

$$
Y
$$

Their covariance is

$$
Cov(X,Y)
========

E[(X-E[X])(Y-E[Y])]
$$

---

## Intuition

Covariance tells us whether variables tend to increase together.

### Positive Covariance

If large values of `X` tend to occur with large values of `Y`

then

$$
Cov(X,Y)>0
$$

Example:

* Hours studied
* Exam score

---

### Negative Covariance

If large values of `X` tend to occur with small values of `Y`

then

$$
Cov(X,Y)<0
$$

Example:

* Speed
* Travel time

---

### Zero Covariance

If no linear relationship exists

$$
Cov(X,Y)=0
$$

---

## Alternative Formula

Expanding the definition gives

$$
Cov(X,Y)
========

## E[XY]

E[X]E[Y]
$$

This formula is usually easier to compute.

---

## Relationship with Variance

Variance is simply covariance with itself.

$$
Var(X)
======

Cov(X,X)
$$

---

# 4. Covariance Matrix

When we have multiple variables, we organize all variances and covariances into a matrix.

Suppose

$$
X=\begin{bmatrix}X_1\X_2\\vdots\X_n\end{bmatrix}
$$

Then the covariance matrix is

$$
\Sigma=
\begin{bmatrix}
Cov(X_1,X_1) & Cov(X_1,X_2) & \cdots & Cov(X_1,X_n)\
Cov(X_2,X_1) & Cov(X_2,X_2) & \cdots & Cov(X_2,X_n)\
\vdots & \vdots & \ddots & \vdots\
Cov(X_n,X_1) & Cov(X_n,X_2) & \cdots & Cov(X_n,X_n)
\end{bmatrix}
$$

---

## Structure

Diagonal entries:

$$
Cov(X_i,X_i)
============

Var(X_i)
$$

Off-diagonal entries:

$$
Cov(X_i,X_j)
$$

measure relationships between different variables.

---

## Example

Suppose

* Height
* Weight

Then

$$
\Sigma=
\begin{bmatrix}
Var(Height) & Cov(Height,Weight)\
Cov(Weight,Height) & Var(Weight)
\end{bmatrix}
$$

---

## Important Properties

### Symmetry

Because

$$
Cov(X,Y)=Cov(Y,X)
$$

the covariance matrix satisfies

$$
\Sigma=\Sigma^T
$$

---

### Positive Semi-Definite

For any vector

$$
a
$$

$$
a^T\Sigma a \ge 0
$$

This property is extremely important in optimization and machine learning.

---

# Why Covariance Matrices Matter

Covariance matrices are central to:

* Principal Component Analysis (PCA)
* Multivariate Gaussian distributions
* Kalman Filters
* Portfolio optimization
* Feature engineering
* Representation learning

In many machine learning algorithms, the covariance matrix captures the structure of the data.

---

# 5. Correlation

A major problem with covariance is scale.

Suppose

* Height measured in meters
* Income measured in dollars

The covariance depends heavily on units.

To remove this dependence, we use correlation.

---

## Definition

The correlation coefficient is

$$
\rho_{XY}
=========

\frac{Cov(X,Y)}
{\sigma_X\sigma_Y}
$$

where

$$
\sigma_X
========

\sqrt{Var(X)}
$$

and

$$
\sigma_Y
========

\sqrt{Var(Y)}
$$

---

## Range of Correlation

Correlation always satisfies

$$
-1
\le
\rho_{XY}
\le
1
$$

---

### Perfect Positive Correlation

$$
\rho=1
$$

Variables move together exactly.

---

### Perfect Negative Correlation

$$
\rho=-1
$$

Variables move in opposite directions exactly.

---

### No Linear Relationship

$$
\rho=0
$$

No linear relationship exists.

---

## Example

Suppose

$$
Y=2X
$$

Then

$$
\rho=1
$$

because the relationship is perfectly linear.

---

Suppose

$$
Y=-3X
$$

Then

$$
\rho=-1
$$

because the relationship is perfectly negative.

---

# Covariance vs Correlation

| Property              | Covariance      | Correlation |
| --------------------- | --------------- | ----------- |
| Measures relationship | Yes             | Yes         |
| Depends on units      | Yes             | No          |
| Bounded               | No              | Yes         |
| Range                 | Any real number | `[-1,1]`    |
| Easy to interpret     | No              | Yes         |

---

# Connection to Machine Learning

These concepts appear throughout machine learning:

### Normal Distribution

Used in:

* Bayesian methods
* Gaussian Processes
* Kalman Filters
* Variational Autoencoders

### Bernoulli Distribution

Used in:

* Binary classification
* Logistic regression
* Neural network outputs

### Covariance Matrix

Used in:

* PCA
* Multivariate Gaussian models
* Representation learning

### Correlation

Used in:

* Feature selection
* Data analysis
* Exploratory data analysis
* Financial modeling

---

# Key Takeaways

* The Normal Distribution models continuous data and is fundamental because of the Central Limit Theorem.
* The Bernoulli Distribution models a single success/failure experiment.
* Covariance measures how two variables move together.
* Variance is a special case of covariance.
* The Covariance Matrix summarizes relationships among many variables simultaneously.
* Correlation is a normalized covariance that always lies between `-1` and `1`.
* These concepts form the mathematical foundation for statistics, machine learning, data science, quantitative finance, and signal processing.
