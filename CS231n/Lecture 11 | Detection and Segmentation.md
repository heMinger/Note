# Detection and Segmentation

# Date: 7/11/24
writer: MingheLi

## semantic segmentation
1. label each pixel in the image with a category label
2. idea1: slide window
3. idea2: fully convolutional network
4. downsampling + upsampling: Unet
- transpose convolution: upsampling
![image](https://github.com/user-attachments/assets/7a7a94fa-3f9c-45d5-a60e-f2c302f9ecfc)
5. summary:
- donwnsampling by strided convolution or polling
- upsampling by transpose convolution or various types of unpooling or upsamoling
- train this whole model end to end with back propagation using cross entropy loss over every pixel
## Classification + Localization
1. two FC layers:
- class scores: generate correct label
- box coordinate: (x, y, w, h)
2. two losses:
### human pose estimation
predict joint positions
- each position got a loss function
## Object Detection
**difference with classification + localization: not fix catogery number, don't know how many objects you expect to find in image. **
### Sliding Window
1. apply a CNN to many different crops of the image, CNN classifies each crop as object or background
2. region proposal
- selective search: find "blobby" image regions that are likely to contain objects.
- get proposal regions -> classify
3. 
