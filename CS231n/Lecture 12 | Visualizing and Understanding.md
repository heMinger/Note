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
1. nearest neighbors
2. 
