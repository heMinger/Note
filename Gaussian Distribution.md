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
    1. independent → Cov(x,y)=0

$$
x,y:independent \Rightarrow Cov(x,y)=0
$$

## Isotropic Gaussina

An isotropic Gaussian is one where the covariance matrix Σ can be represented in this form:

$\Sigma=\sigma ^ 2I$
