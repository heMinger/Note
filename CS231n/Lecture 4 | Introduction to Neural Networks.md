# Introduction to Neural Networks

## Date: 23/10/24
writer: heming
note: I didn't save my notes, so it's all gone. It hurts but I won't rewrite it.

## backpropagation
compute the gradient we need for arbitrarily complex functions.
1. computational node
- add gate: **gradient distributor**: it took the upstream gradient and distribute it, pass the exact same thing to both of the branches that were connected.
- max gate: **gradient router**: one of these is going to get the full value of the gradient just passed back and routed to that variable, and then the other one have a gradient of zero.\
 take the upstream gradient and route it to one of the branches.\
make sense: the forward pass, only the value of the maximum got passed down to the rest of the computational graph. Only of one function effect the function computation at the end, so it makes sense that when we're passing our gradients back, we just want to adjust that specific value.
- multaplication gate: **gradient switcher**, scale the upstream gradient by the value of the other branch.
2. 
