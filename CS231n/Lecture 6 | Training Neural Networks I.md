# Training Neural Networks I *

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
different choices of different nonlinearities and trade-offs between them.
1. sigmoid:
- $$sigma(x)=\frac{1}{1+e^{-x}}$$
- problem1: saturated neurons "kill" the gradients. when X is equal to a very negative or X is equal to large positive numbers, these are regions that sigmod function is flat, and it's going to kill off the gradient, and can't get a gradient flow coming back.
- problem2: sigmoid outputs are not zero centered. 'cause we can just decrase gradient in x or y horizental, so zero centerd can let us converge to the optimal (12')
- problem3: exp() is a bit compute expensive. 
2. tanh(x):
  ![{EE09E5A5-7993-434F-B88B-C55782A5FF30}](https://github.com/user-attachments/assets/d597b231-c9c8-42a4-95f5-16b57eea1b93)
- squash numbers to range [-1,1]
- zero centered (nice)
- still kills gradients when saturated :(
3.  relu (rectified linear unit): 
- $f(x)=max(0,x)$
- advantage1: does not saturate (in + region)
- advantage2: very computationally efficient
- advantage3: converges much faster than sigmoid/tanh in practice.
- advantage4: more biologically plausible than sigmoid.
- issue1: not zero-centered output
- issue2: an annoyance: killing the gradient in half of the regime. it's a problem but it's acceptable.
- experience: people like to initialize ReLU neueons with slightly positive biases (e.g. 0.01)
4. Leaky ReLU:
- $f(x)=max(0.01x,x)$
- advantage1: does not saturate
- advantage2: computationally efficient
- advantage3: coverges much faster than sigmoid/tanh in practice
- advantage4: will not "die"
5. Parametric Rectifier(PReLU) 
- $f(x)=max(\alpha x,x)$
- $\alpha$ is a parameter that we can backprop into and learn.
6. ELU (Exponential Linear Units):
-
$$
f(x)=
\begin{cases}
x, \quad x>0
\alpha (exp(x)-1),\quad x\leq 0\\
\end{cases}
$$
- all benefits of ReLU
- closer to zero mean outputs
- negative saturation regime compared with Leaky ReLU adds some robustness to noise
7. Maxout "Neuron"
- $max((\omega_1)^T + b_1, (\omega_2)^T + b_2)$
- generalize ReLU and Leaky ReLU. Because you're taking the max over these two linear functions.
- Linear Regime! Does not saturate! Does not die!
- problem: doubles the number of parameters/neuron
8. In practice (how to choose):
- Use ReLU. Be careful with learning rates.
- Try out Leaky ReLU/ Maxout/ ELU
- Try out tanh but don't expect much
- Don't use sigmoid. 

### Data Pre process
1. zero-centered data
2. normalized data
- don't do it for images. 'cause pixels already have relatively comparable scale and distribution.
- always use in more generalizational problem where you might have different features that are very different of very different scales.
3. PCA
- don't do it for images.
4. Whitening
- don't do it for images.
5. In practice for images: **center only** for both train and test data.
- sigmoid needs zero-mean input, but the center operation only satisty the input of first layer, and it's gonna be lots of nonzero mean problems later on. So it's not sufficient to solve the problem of sigmoid.
### Weight Initialization
1. Q: What happens when W=0 init is uesd?
A: every neurons have the same operation basically on top of inputs. all same outputs -> all same gradient back -> all update in the same way -> exactly all same neurons.
2. First Idea: small random numbers.
- okay for small networks, but problems with deeper networks. deeper network after few iteration, all activations become zero.
- Q: think about the backward pass. What do the gradients look like? \
multiplication of the upstream gradient by our weights.
3. big initialization -> saturate
4. Reasonable initialization:
- Xavier initialization
- 
```
W = np.random.randn(fan_in, fan_out) / np.sqrt(fan_in) # layer initialization
```
- the variance of input to be the same of the variance of output.
- when using the ReLU nonlinearity it breaks. because killing the half of the units,  it's halving the variance that you get out of this.

### Batch Normalization
- motivation: we want unit gaussian activation.
- 
![image](https://github.com/user-attachments/assets/8f6bb489-1220-4321-9135-5386312ebaf8)
- for each layer, we can have unit gaussian and hopefully during training this will preserve this.
- if **N** samples for this batch, each batch has dimension **D**
- ![image](https://github.com/user-attachments/assets/d5496a8b-640a-439b-a062-e63526d2b509)
- position: usually insert after fully connected or convolutional layers, and before nonlinearity.
- with a *convolutional layer*: (one mean + one standard deviation) per activation map, nomolize this across all of the examples in the batch.
- summary ![image](https://github.com/user-attachments/assets/b04cfd9f-f54e-4566-9a5a-ade4df6a30ea)
## Training Dynamics
### Babysitting the Learning Process 
