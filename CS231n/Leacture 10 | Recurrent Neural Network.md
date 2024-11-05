# Recurrent Neural Network

# Date: 4/11-5/11
writer: Minghe Li

## TODO
1. min-char-rnn.py

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
## 
### sequence to sequence: many to one + one to many
1. many to one: encode input sequence in a single vector
2. one to many: produce output sequence from single input vector
### example: character-level language model
1. vocabulary: [h, e, l, o]
2. example training sequence: "hello"
3. ![image](https://github.com/user-attachments/assets/7874657d-f432-4b83-8bbb-6306b12ec51b)
- step time 1:\
(1) input chars: "h" \
(2) object: "e". \
(3) input layer: [1, 0, 0, 0]. (because vocabulary is [h, e, l, o]) \
(4) output layer: [1.0, 2.2, -3.0, 4.1]. -> "o" \
- step time 2: \
(1) input chars: "e" \
(2) object: "l". \
(3) input layer: [0, 1, 0, 0]. (because vocabulary is [h, e, l, o]) \
(4) output layer: [0.5, 0.3, -1.0, 1.2]. -> "o" \
- step time 3: \
(1) input chars: "l" \
(2) object: "l". \
(3) input layer: [0, 0, 1, 0]. (because vocabulary is [h, e, l, o]) \
(4) output layer: [0.1, 0.5, 1.9, -1.1]. -> "l" \
- step time 4: \
(1) input chars: "l" \
(2) object: "o". \
(3) input layer: [0, 0, 1, 0]. (because vocabulary is [h, e, l, o]) \
(4) output layer: [0.2, -1.5, -0.1, 2.2]. -> "o" \
4. test time: sample characters one at a time, feed back to model.
![image](https://github.com/user-attachments/assets/400f9717-1a57-485d-8de4-df6032542098)
- Q: **why might we sample, instead of just taking the character with the largest score?** \
In practice, we got distribution and sample. Sometimes we just take the argmax probability, and that will sometimes be a little bit more stable. But one advantage of sampling, in general, is that it lets you get diversity from models. Sometimes we might have the same input, maybe the same prefix, or in the case of image captioning, maybe the same image. But then if you smaple rather than taking the argmax, you'll see that sometimes these trained models are actually able to produce multiple different types of reasonable output sequences, depending on which samples they take at the first time steps. It's a benefit, cause we can get now more diversity in outputs.
```diff
- what does sample mean? our vocabulary? chars in our vocabulary?
```
- Q: at test time, could we feed in this softmax vector rather than a one hot vector?\
(1) In general, if you ask your model to do some different things at test time from traning time, it'll usually blow up. It'll usually give you garbage.\
(2) In practice, vocabularies might be very large. If you're thinking about generating words one at a time, your vocabulary is every word in the english language,, which could be tens of thousands of elements. So, in practice, we take this one hot vector, which is **sparse vector operations**, rather than dense factors.

### truncated Backpropagation through time
1. previous: if we train on Wikipedia, every time made a gradient step, make a forward pass through the entire text of all of wikipedia, and then make a backward pass through all of wikipedia, and then make a single gradient update. That would be super **slow**, and model would never converge. And it would take a ridiculous amount of **memory**.
2. approximation called truncated backpropagation through time.
- even though our input sequence is very long, when we're training the model,
- we'll step forward some number of steps, maybe 100,
- compute a loss only over this sub sequence of the data, and take back propagate through this sub sequence
- and now, when we repeat, we still have these hidden states that we computed from the first batch
- when we compute this next batch of data, we will carry those hidden states forwward in time,
- so the forward pass will be exactly the same.
```diff
- I'm not get it.
```
- In general, it's expensive to compute the gradients when we train on large dataset. So instead, we take small mini batches, and use mini batches of data to compute gradient stops.
### Image caption
1. CNN:
- produce a summary vector of the image.
- input: image
- output: FC4096
2. RNN
- take the summary vector generated by CNN, feed into the first time step, and produce words of the caption one at a time.
- special start toke, told RNN model that it's the start of a setence.
- for each step, $h=tanh(W_{xh}*x + W_{hh}\*h+W_{ih}\*v)$, where $W_{ih}*v$ is the image information.
- each time step, compute distribution over all scores in vocabulary, and sample from that distribution, and pass that word back as input at the next time step.
- after all these steps, we'll generate this complete sentence.
- and stop generation once we sample the special ends token.
### Image Captioning with Attention
![image](https://github.com/user-attachments/assets/ee0b32eb-d4a6-41c0-9562-318757db3c9d)
*compare with Image Caption*
1. CNN summarize the entire image, it produces some **grid of vectors** that give maybe one vector for each spatial location in the image, rather than produces a single vector.
2. forward part of RNN model: in addition to sampling the vocabulary at every time step, it also produces a **dirtribution over locations** in the image where it wants to look.
3. distribution over image locations can be seen as a kind of a tension of where the model should look during training.
4. distribution over image locations weill go back to the set of vectors to give a single summary vector. And summary vector gets fed, as an additional input at the next time step of neural network.
5. each time, hidden layer produce two outputs. One is our distribution over vocabulary words, and the orther is a distribution over image locations.
6. result: its attention is shiffting around different parts of the image for each word in the caption that it generates. (shown in below)
![image](https://github.com/user-attachments/assets/87a07cc3-fdfe-4a21-b355-90f793d26f30)
```diff
- so, the meaning of attention is just attention? is the area we focus of the image?
```
7.  
