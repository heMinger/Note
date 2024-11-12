# Visualizing and Understanding

## date: 11/11
writer: MingheLi

## Recap
1. semantic segmentation: sign labels to every pixel in the input image.
2. classification + localization: draw a box of object + classification of object. **fix number of objects**
3. object detection: **fixed category of labels but various number of objects**.
4. instance segmentation

visualize the inside of networks
## Activations
### first layer
1. convolutional filters gets slide over input image, and take inner products
2. simply visualize the learned weights of filters as images themselves.
- for 11*11\*3 filters, just visualize that filter as a 11 * 11 image with 3 channels.
- intuition comes from template matching and inner products: the input which maximize the activation under a norm constraint on the input is exactly when those two vectors match up.
### medium layer
1. example: 16*7\*7: visualized as 16 7*7 gray image
### last layer
1. compute **nearest neighbors** according to 4096 dimensional vector which is computed by FCN.
2. **dimensionality reduction**:
- t-SNE(t-distributed stochastic neighbor embeddings): 
- apply t-SNE to the features from the last layer of our trained image net classifier(maybe 4096 dimensional vector for AlexNet)
- compress 4096-d down to 2-d coordinate
- take the original pixels of image and place that at the 2-d coordinate to visualize
------
- activation volume: outputs of convolutional layerm, which are maybe 3 dimensional chunk of numbers
- activation map: one slice of activation volume

### maximally activating patches
1. each neuron in convolutional layer only looking at the sub set of the image.
2. then, visualize the patches from the large data set of images corresponding to the maximal activations.
3. sort these patches by their activation at the particular layer.
4. (In my opinion) we just visulize which part of image that nn pay attention to.

### occlusion experiments
1. try to figure out which parts of the input images cause the network to make it's classification decision.
2. how
- block out some part of image, replace that part of image with the mean pixel value from the data set(occluded patch).
- run the occluded image through the network and record the predicted probability of the occluded image
- slide occluded patch over position in the input image and repeat same process.
- draw a heat map show what predicted probability output from network.
3. idea: when we block out some part of the image, if that causes the network score to change drastically, then probably that part of the input image was really important for the classification decision.

## Gradients
### Saliency Maps
1. relative simple idea: compute the gradient of the predicted class score with the respect to the pixels of the input image.
2. idea: for each pixel in the input image, if we wiggle it a little bit, how much will the classification score for the class change
### intermediate features via (guided) backprop
1. compute the gradient of some intermediate value in the network with the respect to the pixels of the image.

### Gradient Ascent
1. answer the question: remove this reliance on some input image, then just ask what type of input in general would cause this neuron to activate
2. we want to fix the weight of out trained network and synthesizing image by performing gradient ascent on the pixels of the image to try and maximize the score of some intermediate neuron of some class.
3. regularization term: prevent the pixels of our generated image from over fitting to the peculiarities of that particular network.
4. want a generated image of two properties:
- maximally activate some score or some neuron value
- image look like a natural image, have the kind of statistics that we typically see in natural images.(function of regularization term)

### fooling images/ adversarial examples
1. starts from an arbitraty image
2. pick an arbitraty class
3. modify the image to maximize the calss
4. repeat until netwrok is fooled
5. so the result is, network and recognize an elephant image as koala.

## Fun
### DeepDream: Amplify existing features
1. steps
- forward: compute activations at chosen layer.
- set gradient of chosen layer to its activation
- backword: compute gradient on image
- update image
2. influence: amplify existing features that we detected by the network in this image
- 'caz whatever features existed on that layer now we set the gradient equal to the feature, and we just tell the network to amplify whatever features you already saw in that image.
- gradient descent just to aprroximate the gradient.

random is creativity!!!

### feature inversion
1. take image -> run through the network -> get feature -> reconstruct image by feature. so that could give information about the image was captured in that feature vector.

### texture synthesis
1. nearest neighbor: generate pixels one at a time in scanline order, from neighborhood of already generated pixels and copy nearest neighbor from input.
2. neural texture synthesis: compute feature of image and use this features to computer a descriptor of the texture of this input image.
- **gram matrix**: pick out two different columns in the input volume, each column is C-dimensional vector, and take outer product between those two vectors to get C*C matrix.
(1) tells us about the co-occurrance of different features at two points in the image.\
(2) efficient to compute, and more efficient than variance matrix.
- reconstruct this gram matrix texture descriptor of the input image(random initialized.)

### Neural Style Transfer
combination of texture synthesis and feature inverison
1. problem: style transfer requires many forward/backward passes through VGG; very slow!
2. solution: train another neural network to perform style transfer for us!

## Summary
1. Activations: nearest neighbors, dimensionality reduction, maximal patches, occlusion
2. GradientsL saliency maps, class visualization, fooling images, feature inversion
3. fun: deepdream, style transfer
```diff
+ In some sense, some of these techinics just change the loss function of CNN or the gradient.
so, what else we could change or combine of CNN?
```
