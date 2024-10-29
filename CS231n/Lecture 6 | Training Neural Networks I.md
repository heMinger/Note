# Training Neural Networks I

## Date: 29/10
writer: Minghe Li

## Overview
1. One time setup
activation functions, preprocessing, weight initialization, regularization, gradient checking
2. Trainin dynamics
babysitting the learning process, parameter updates, hyperparameter optimization
3. Evaluation
model ensumbles

## one time setup
### Activation Functions
different choices of different nonlinearities and trade-offs between them.\
1. sigmoid:
- $$sigma(x)=\frac{1}{1+e^{-x}}$$
- problem1: saturated neurons "kill" the gradients. when X is equal to a very negative or X is equal to large positive numbers, these are regions that sigmod function is flat, and it's going to kill off the gradient, and can't get a gradient flow coming back.
- problem2: sigmoid outputs are not zero centered. 'cause we can just decrase gradient in x or y horizental, so zero centerd can let us converge to the optimal (12')
- problem3: exp() is a bit compute expensive. 
2. tanh(x):\
  ![{EE09E5A5-7993-434F-B88B-C55782A5FF30}](https://github.com/user-attachments/assets/d597b231-c9c8-42a4-95f5-16b57eea1b93)
- squash numbers to range [-1,1]
- zero centered (nice)
- still kills gradients when saturated :(
3.  relu (rectified linear unit): \
- $f(x)=max(0,x)$
- advantage1: does not saturate (in + region)
- advantage2: very computationally efficient
- advantage3: converges much faster than sigmoid/tanh in practice.
- advantage4: more biologically plausible than sigmoid.
- issue1: not zero-centered output
- issue2: an annoyance: killing the gradient in half of the regime.
