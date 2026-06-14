# Probability Foundations: Normal Distribution, Bernoulli Distribution, Covariance Matrix, and Correlation

Probability and statistics provide the mathematical language for reasoning under uncertainty. Whether we are analyzing stock markets, building machine learning models, studying biological systems, or designing engineering solutions, a few concepts appear repeatedly: the Normal Distribution, the Bernoulli Distribution, Covariance, the Covariance Matrix, and Correlation.

---

# Normal Distribution

The Normal Distribution, also known as the Gaussian Distribution or Bell Curve, is the most important continuous probability distribution in statistics.

Many real-world quantities approximately follow a normal distribution:

- Human heights
- Measurement errors
- Sensor noise
- IQ scores
- Biological measurements
- Financial returns (approximately)

Its probability density function (PDF) is:

$$ f(x) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right) $$

where:

- $\mu$ is the mean
- $\sigma^2$ is the variance
- $\sigma$ is the standard deviation

## Mean and Variance

The center of the distribution is controlled by the mean.

$$ E[X] = \mu $$

The spread of the distribution is controlled by the variance.

$$ Var(X) = \sigma^2 $$

The standard deviation is:

$$ \sigma = \sqrt{Var(X)} $$

A larger variance produces a wider bell curve, while a smaller variance produces a narrower one.

## Standardisation

Suppose:

$$ X \sim N(\mu,\sigma^2) $$

We can transform it into a standard normal random variable using:

$$ Z = \frac{X-\mu}{\sigma} $$

Then:

$$ Z \sim N(0,1) $$

This process is called standardisation and allows probabilities from any normal distribution to be converted into probabilities from the standard normal distribution.

## The 68-95-99.7 Rule

One of the most useful properties of the normal distribution is:

$$ P(|X-\mu|<\sigma) \approx 0.68 $$

$$ P(|X-\mu|<2\sigma) \approx 0.95 $$

$$ P(|X-\mu|<3\sigma) \approx 0.997 $$

This means:

- About 68% of observations lie within one standard deviation of the mean.
- About 95% lie within two standard deviations.
- About 99.7% lie within three standard deviations.

## Linear Combinations Stay Normal

If:

$$ X \sim N(\mu_X,\sigma_X^2) $$

and

$$ Y \sim N(\mu_Y,\sigma_Y^2) $$

are independent, then:

$$ aX+bY \sim N(a\mu_X+b\mu_Y,\;a^2\sigma_X^2+b^2\sigma_Y^2) $$

The mean follows from linearity of expectation:

$$ E[aX+bY] = aE[X] + bE[Y] $$

The variance follows from independence:

$$ Var(aX+bY) = a^2Var(X)+b^2Var(Y) $$

This property is widely used in quantitative finance and signal processing.

---

# Bernoulli Distribution

The Bernoulli Distribution models a single experiment with only two outcomes:

- Success
- Failure

Examples include:

- Coin tosses
- Pass/fail exams
- Spam/not spam emails
- Customer purchases

A Bernoulli random variable takes values in:

$$ X \in \{0,1\} $$

with:

$$ P(X=1)=p,\qquad P(X=0)=1-p $$

where $p$ is the probability of success.

## Mean

Using the definition of expectation:

$$ E[X] = 1\cdot p + 0\cdot(1-p) = p $$

The mean represents the long-run proportion of successes.

## Variance

Since a Bernoulli variable can only be 0 or 1:

$$ X^2 = X $$

Therefore:

$$ E[X^2] = p $$

Using the variance formula:

$$ Var(X)=E[X^2]-(E[X])^2 $$

we obtain:

$$ Var(X)=p-p^2=p(1-p) $$

## Interpretation

Variance is largest when uncertainty is highest.

The maximum occurs at:

$$ p=\frac{1}{2} $$

giving:

$$ Var(X)=\frac{1}{4} $$

Variance becomes zero when:

$$ p=0 $$

or

$$ p=1 $$

because the outcome is then completely certain.

---

# Covariance

Covariance measures how two random variables move together.

For random variables $X$ and $Y$:

$$ Cov(X,Y)=E[(X-E[X])(Y-E[Y])] $$

An equivalent formula is:

$$ Cov(X,Y)=E[XY]-E[X]E[Y] $$

## Interpretation

### Positive Covariance

$$ Cov(X,Y)>0 $$

Large values of $X$ tend to occur with large values of $Y$.

Example:

- Hours studied and exam score.

### Negative Covariance

$$ Cov(X,Y)<0 $$

Large values of $X$ tend to occur with small values of $Y$.

Example:

- Speed and travel time.

### Zero Covariance

$$ Cov(X,Y)=0 $$

No linear relationship exists between the variables.

## Relationship with Variance

Variance is a special case of covariance:

$$ Var(X)=Cov(X,X) $$

---

# Covariance Matrix

When we work with many variables simultaneously, we organize all variances and covariances into a covariance matrix.

Suppose:

$$ X = \begin{bmatrix} X_1 \\ X_2 \\ \vdots \\ X_n \end{bmatrix} $$

Then the covariance matrix is:

$$ \Sigma = \begin{bmatrix} Cov(X_1,X_1) & Cov(X_1,X_2) & \cdots & Cov(X_1,X_n) \\ Cov(X_2,X_1) & Cov(X_2,X_2) & \cdots & Cov(X_2,X_n) \\ \vdots & \vdots & \ddots & \vdots \\ Cov(X_n,X_1) & Cov(X_n,X_2) & \cdots & Cov(X_n,X_n) \end{bmatrix} $$

## Structure

The diagonal entries are variances:

$$ Cov(X_i,X_i)=Var(X_i) $$

The off-diagonal entries are covariances:

$$ Cov(X_i,X_j) $$

These measure how different variables move together.

## Example

For height and weight:

$$ \Sigma = \begin{bmatrix} Var(Height) & Cov(Height,Weight) \\ Cov(Weight,Height) & Var(Weight) \end{bmatrix} $$

## Properties

### Symmetry

$$ Cov(X,Y)=Cov(Y,X) $$

Therefore:

$$ \Sigma=\Sigma^T $$

### Positive Semi-Definite

For any vector $a$:

$$ a^T\Sigma a \ge 0 $$

This property is fundamental in optimization, statistics, and machine learning.

## Why Covariance Matrices Matter

Covariance matrices appear throughout:

- Principal Component Analysis (PCA)
- Portfolio Optimization
- Kalman Filters
- Multivariate Gaussian Models
- Representation Learning
- Feature Engineering

---

# Correlation

A major limitation of covariance is that it depends on scale and units.

To remove this dependency, we use correlation.

The correlation coefficient is:

$$ \rho_{XY}=\frac{Cov(X,Y)}{\sigma_X\sigma_Y} $$

where:

$$ \sigma_X=\sqrt{Var(X)} $$

$$ \sigma_Y=\sqrt{Var(Y)} $$

## Range

Correlation always satisfies:

$$ -1 \le \rho_{XY} \le 1 $$

### Perfect Positive Correlation

$$ \rho=1 $$

Variables move together perfectly.

### Perfect Negative Correlation

$$ \rho=-1 $$

Variables move in exactly opposite directions.

### No Linear Relationship

$$ \rho=0 $$

No linear relationship exists.

## Examples

If:

$$ Y=2X $$

then:

$$ \rho=1 $$

If:

$$ Y=-3X $$

then:

$$ \rho=-1 $$

---

# Covariance vs Correlation

| Property | Covariance | Correlation |
|----------|------------|------------|
| Measures relationship | Yes | Yes |
| Depends on units | Yes | No |
| Bounded | No | Yes |
| Range | Any real number | [-1,1] |
| Easy to interpret | No | Yes |

---

# Applications in Machine Learning

## Normal Distribution

Used in:

- Gaussian Processes
- Bayesian Inference
- Kalman Filters
- Variational Autoencoders

## Bernoulli Distribution

Used in:

- Binary Classification
- Logistic Regression
- Neural Network Outputs
- Reinforcement Learning

## Covariance Matrix

Used in:

- PCA
- Multivariate Gaussian Models
- Feature Engineering

## Correlation

Used in:

- Feature Selection
- Exploratory Data Analysis
- Financial Modeling

---

# Key Takeaways

- The Normal Distribution is the most important continuous probability distribution.
- Standardisation converts any normal variable into a standard normal variable.
- The Bernoulli Distribution models a single success/failure experiment.
- Covariance measures how two variables move together.
- Variance is a special case of covariance.
- The Covariance Matrix summarizes relationships among multiple variables.
- Correlation is a normalized version of covariance that always lies between -1 and 1.
- These concepts form the foundation of statistics, machine learning, data science, and quantitative finance.
