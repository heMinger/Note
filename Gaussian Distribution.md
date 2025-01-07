[The Latent: Code the Maths - All you need to know about Gaussian distribution](https://magic-with-latents.github.io/latent/posts/ddpms/part2/)

All you need to know about Gaussian Distribution

## Covariance

$$
Cov(X,Y)=E[(X-E[X])(Y-E[Y])]=E[XY]-E[X]E[Y]
$$

### Information in covariance

1. a sense of how much two random variables as well wheir scales are **linearly related**
2. only **linear dependence**
3. sign of convariance
    1. positive: both variables tend to take on relatively high values simultaneously
    2. negative: one large one small
4. independent and value of covariance

$$
x,y:independent \rightarrow Cov(x,y)=0 
$$
$$
Cov(x,y)=0 \nrightarrow x,y is independent
$$

## Isotropic Gaussina

An isotropic Gaussian is one where the covariance matrix Σ can be represented in this form:

$\Sigma=\sigma ^ 2I$
where, $I$ is the Identity matrix, and $\sigma^2$ is the scalar variance. 

- This form is a diagonal matrix multiplied by a scalar variance. Therefore, an isotropic multivariate Gaussian is circular or spherical.
- **multicariate normal** distribution and **$Cov(x1, x2)=0$** $\Rightarrow$ $x1$ and $x2$ are independent.
- multivariate distribution is isotropic $\Rightarrow$
1. Covariance matrix is diagonal
2. distribution can be represented as a product of univariate Gaussians, $P(X)=P(x1)P(x2)$

Q: Why do we want to represent the covarince matrix in this form?
A: As the dimensions of a multivariate Gaussian grows, the mean follows a linear growth where the covarince matrix follows quadratic growth in terms of number of parameters. This quadratic growth isn’t computation friendly. A diagonal covariance matrix makes things much easier.

## Conditional Distribution

There is a multivariate distribution over $x$ where
$$
x=\left\[
\begin{align}
x_1 \\
x_2 
\end{align}
\right\]
$$

$$
\mu=\left\[
\begin{align}
\mu_1 \\
\mu_2 
\end{align}
\right\]
$$

$$
\Sigma=\left\[
\begin{align}
\Sigma_{11} & \Sigma_{12}\\
\Sigma_{21} & \Sigma_{22} 
\end{align}
\right\]
$$

Then the distribution of $x1$ conditional on $x2=a$ is multivariate normal:

$$
p(x1|x2=a)\bar{\mu}
$$

