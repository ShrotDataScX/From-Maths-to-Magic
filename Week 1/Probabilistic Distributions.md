# Probability Foundations: Normal Distribution, Bernoulli Distribution, Covariance Matrix, and Correlation

## Key Equation Fixes (GitHub README Format)

$$ f(x)=\frac{1}{\sqrt{2\pi\sigma^2}}\exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right) $$

$$ E[X]=\mu $$

$$ Var(X)=\sigma^2 $$

$$ \sigma=\sqrt{Var(X)} $$

$$ N(0,1) $$

$$ Z=\frac{X-\mu}{\sigma} $$

$$ X\sim N(100,25) $$

$$ P(X<110) $$

$$ Z=\frac{110-100}{5}=2 $$

$$ P(X<110)=P(Z<2) $$

$$ P(|X-\mu|<\sigma)\approx 0.68 $$

$$ P(|X-\mu|<2\sigma)\approx 0.95 $$

$$ P(|X-\mu|<3\sigma)\approx 0.997 $$

$$ aX+bY\sim N(a\mu_X+b\mu_Y,a^2\sigma_X^2+b^2\sigma_Y^2) $$

$$ E[aX+bY]=aE[X]+bE[Y] $$

$$ Var(aX+bY)=a^2Var(X)+b^2Var(Y) $$

$$ X\in\{0,1\} $$

$$ P(X=1)=p $$

$$ P(X=0)=1-p $$

$$ P(X=x)=p^x(1-p)^{1-x},\quad x\in\{0,1\} $$

$$ E[X]=1\cdot p+0\cdot(1-p)=p $$

$$ E[X^2]=p $$

$$ Var(X)=E[X^2]-(E[X])^2 $$

$$ Var(X)=p-p^2=p(1-p) $$

$$ p=\frac12 $$

$$ Var(X)=\frac14 $$

$$ Cov(X,Y)=E[(X-E[X])(Y-E[Y])] $$

$$ Cov(X,Y)>0 $$

$$ Cov(X,Y)<0 $$

$$ Cov(X,Y)=0 $$

$$ Cov(X,Y)=E[XY]-E[X]E[Y] $$

$$ Var(X)=Cov(X,X) $$

$$ \Sigma=\begin{bmatrix} Cov(X_1,X_1) & Cov(X_1,X_2) & \cdots & Cov(X_1,X_n) \\ Cov(X_2,X_1) & Cov(X_2,X_2) & \cdots & Cov(X_2,X_n) \\ \vdots & \vdots & \ddots & \vdots \\ Cov(X_n,X_1) & Cov(X_n,X_2) & \cdots & Cov(X_n,X_n) \end{bmatrix} $$

$$ Cov(X_i,X_i)=Var(X_i) $$

$$ \Sigma=\begin{bmatrix} Var(Height) & Cov(Height,Weight) \\ Cov(Weight,Height) & Var(Weight) \end{bmatrix} $$

$$ Cov(X,Y)=Cov(Y,X) $$

$$ \Sigma=\Sigma^T $$

$$ a^T\Sigma a \ge 0 $$

$$ \rho_{XY}=\frac{Cov(X,Y)}{\sigma_X\sigma_Y} $$

$$ \sigma_X=\sqrt{Var(X)} $$

$$ \sigma_Y=\sqrt{Var(Y)} $$

$$ -1\le\rho_{XY}\le1 $$

$$ \rho=1 $$

$$ \rho=-1 $$

$$ \rho=0 $$

$$ Y=2X $$

$$ Y=-3X $$

This file demonstrates the GitHub README-compatible formatting style where every display equation is written on a single physical line.
