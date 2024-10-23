# Introduction to Neural Networks

## Date: 23/10/24
writer: heming \
note: I didn't save my notes, so it's all gone. It hurts but I won't rewrite it.

## backpropagation
compute the gradient we need for arbitrarily complex functions.
1. computational node
- add gate: **gradient distributor**: it took the upstream gradient and distribute it, pass the exact same thing to both of the branches that were connected.
- max gate: **gradient router**: one of these is going to get the full value of the gradient just passed back and routed to that variable, and then the other one have a gradient of zero.\
 take the upstream gradient and route it to one of the branches.\
make sense: the forward pass, only the value of the maximum got passed down to the rest of the computational graph. Only of one function effect the function computation at the end, so it makes sense that when we're passing our gradients back, we just want to adjust that specific value.
- multaplication gate: **gradient switcher**, scale the upstream gradient by the value of the other branch.
2. vectorized
![image](https://github.com/user-attachments/assets/99b207b4-3889-41fa-859a-8d7f825da357)

## Neural Networks
1. stack multiple of  matrix multiply and linear layer on top of each other with **non-linear functions** in-between.
![image](https://github.com/user-attachments/assets/0a1a253e-3252-43df-bb66-63f906fca3c0)

2. for a same class, W1 can be many different kinds of templates, and W2 is a weighted sum of all of these templates. so, benefits from the combination of different templates, we can recoganize the various forms of a particular class, red car and yellow car are both cars.
3. differents between h and W2: h is the value of scores for each of templates that you have in W1, h is like the score function, it's how much of each template in W1 is present. W2 is the weight of different templates, weight all of the intermeidate scores to get final score for the class.
4. the position of non-linearity: is right before h, so h is the value right after the non-linearity. h is the W1x with the max function $h=max(0, Wx)$
5. 
