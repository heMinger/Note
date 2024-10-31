# Training Neural Networks II

# Date: 31/10
writer: MingheLi

## Overview
1. Fancier optimization
2. Regularization
3. Transfer Learning

## Optimization
### Problem with SGD
1. Q: What if loss changes quickly in one direction and slowly in another?
very slow progress along shallow dimension, jitter along steep direction.
2. local minima and saddle point
- zero gradient, and gradient get stucked.
- Saddle points much more common in high dimension.
- near the saddle points, gradient is small and progress become slow.
3. gradients come from minibatches so they can by noisy.

### SGD + Momentum
![image](https://github.com/user-attachments/assets/694d19f7-54db-41b7-b258-e33a7c1d37bb)

1.initialization: velocity usually init by zero
2. How does momentum help with the poorly conditioned coordinate?
add gradient to volecity at every time step, velocity could monotonically increse up to a point, where the volecity could be larger than the gradient. So that must make a faster progress along the poorly conditioned dimension.
3. noise get averaged out in gradient estimates, and SGD take a much smoothet path towards minimum.
4. actual step
  ![image](https://github.com/user-attachments/assets/04502626-beb6-4c1f-b761-009071c723b4)
5. Nesterov Momentum
- ![image](https://github.com/user-attachments/assets/c836b5d8-2194-44d1-8bab-0533d8a5a4ed)
- step in the direction of velocity that's incorporating information from thest multiple points.
- Annoying: usually we want update in terms of $x_t$, $\nabla f(x_t)$
- change:
![image](https://github.com/user-attachments/assets/f43e3885-a354-4ff0-a6dc-6c5acd8d22aa)
### AdaGrad
 ![image](https://github.com/user-attachments/assets/39c6e22b-c150-4550-91ea-2956aea88d58)
 - what happens to the step size over long time?
steps gets smaller and smaller. when convex, it's a feature; but when non-convex, as you come towards a saddle point, you might get stuck with a adagrad and no longer get any progress.

### RMSProp
variation of AdaGrad \
 ![image](https://github.com/user-attachments/assets/cd02ba80-65a9-41f2-86de-a37d82f8fc13)
