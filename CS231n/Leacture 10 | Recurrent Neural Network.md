# Recurrent Neural Network

# Date: 4/11
writer: Minghe Li

## cool pitch about cool things that RNN can do
1. previous networks: vanilla feed forward network. recieve some fixed size input, like image an or vector. That image is fed through some set of hidden layers, and produce a single output.
2. we want: input more flexibility.
3. RNN can do:
![image](https://github.com/user-attachments/assets/8beb8648-b1f7-4bb1-8510-74bfc8c03390)
- for example: many to many, RNN can translate English to Franch, where length of English and Franch are both variable.
- and also useful for fixed size  input and output problem.

## what is it
1. recurrent core cell
- take some input x, feed that input into the RNN.
- internal hidden state, will be updated every time that the RNN reads a new input. and internal hidden state will be then fed back to the model the next time it reads an input.
- output, every time step.
- ![image](https://github.com/user-attachments/assets/e774435d-bc1b-4105-81b2-1265ee550504)
2. functional form of this recurrence relation
- recurrence relation refers to the green part(RNN) in the picture above
- ![image](https://github.com/user-attachments/assets/5d177ee8-7f9e-4862-9e91-e0b5f7cf1de1)
- notice: the same function and the same set of parameters are used at every time step.
3. vanilla Recurrent Neural Network
- $h_t = tanh(W_{hh}h_{t-1}+W_{xh}x_t)$
- $y_t=W_{hy}h_t$
- I guess maybe $W_{hh}$ and $W_{xh}$ is some pre-set parameters. so the above fomular just linear combine $h_{t-1}$ and $x_t$, and squash them through a tanh to get some non-linearity.
- $y_t$ is the output, model transfer the hidden state and produce maybe some class score predictions.
4. Understanding RNN using computational graphs. many to many
- unrolling this computational graph for multiple time step.
- ![image](https://github.com/user-attachments/assets/304c57b9-8cd9-442e-aa43-b7245711a870)
- $h_0$: initial hidden state. usually initialized to zeros for most context.
- $x_t$: input
- $W$: reuse the same $W$ matrix at every time of the computation.
- $f_W$: every time, takes unique $x_t$ and unique current hidden state $h_{t-1}$, but same $w$, to produce $h_t$
-$y_t$: every time step, **$h_t$** might feed into **some other little neural network** that can produce a $y_t$.
- $L_t$: loss between $y_t$ and ground truth.
- L: final loss for the entire traning step: sum of individual losses $L_k$.
- back propagation: loss from the final loss into these time steps. -> each time steps will compute a local gradient on the weights, w, which will call then be summed to give us our final gradient for the weights, w. 
```diff
final gradient for W will be the **sum** of all of those individual per time step gradients.
- I thought it is product
```
- 
