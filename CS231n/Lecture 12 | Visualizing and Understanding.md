# Visualizing and Understanding

## date: 11/11
writer: MingheLi

## Recap
1. semantic segmentation: sign labels to every pixel in the input image.
2. classification + localization: draw a box of object + classification of object. **fix number of objects**
3. object detection: **fixed category of labels but various number of objects**.
4. instance segmentation

## visualize the inside of networks
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

### Saliency Maps
1. relative simple idea: compute the gradient of the predicted class score with the respect to the pixels of the input image.
2. idea: for each pixel in the input image, if we wiggle it a little bit, how much will the classification score for the class change
