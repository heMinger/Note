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
### Adam
sort of like RMSProp with momentum
![image](https://github.com/user-attachments/assets/b42045aa-b158-4c22-ab19-6fde54f624c1)
1. Q: What happens at first timestep?
- second_moment set to 0 at first, so second_moment is very small, so x takes a large step.
2. Adam with bias, so we can limit the step size it takes at first.
![image](https://github.com/user-attachments/assets/ca48a46e-129f-4a86-80ca-64c626abc3e5)
3. exprical value
- beta1 = 0.9
- beta2 = 0.999
- learning rate = 1e-3 or 5e-4
### Learning Rate
1. start at a large learning rate and  decay over time
2. step decay: decay learning rate by half every few epochs.
3. exponential decay: $\alpha = \alpha _0 e^{-kt}$
4. $1/t$ decay: $\alpha = \alpha _0 /(1+kt)$
5. more common with SGD momentum and a little bit less common with other things like atom.
6. learning rate decay is the second order optimization, at first, you want to it go with the normal learning rate. You can keep an eye on it, if the loss wave, you could decay the learning rate.

### Model Ensembles
1. train multiple independent models. keep multiple snapshots of model during the course of training and use these as assembles.
2. at test time average results from all models
3. tips and tricks: instead of using actual parameter vector, keep a moving average of the parameter vector and use that at test time.
### Regularization
*improve them performance of single model*
1. add something to our model, to prevent it from fitting the training data too well, and attempts to make it perform beter on unseen data.
2. different methods
- ![image](https://github.com/user-attachments/assets/4420e1e9-6273-49a2-b85d-4653a24ca242)

3. *Dropout*
- for neural network
- in each forward pass, randomly set some neurons to zero.
- usually fully connected layer,
- and perhaps convolutional layers as well,  but in convolutional layers, sometimes just drop out some feature maps, some entire channels.
- why reasonable
(1) helps prevent co-adaptation of features. \
(2) kind of like doing model ensemble within a single model.
- at test time: multiply by dropout probability.
4.Data Augmentation
- randomly transform the image in some way during training
5.  
