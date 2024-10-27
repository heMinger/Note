# Convolutional Neural Network

## date: 27/10/24
writer: Minghe

## history

## Convolutional Neural Networks
Work from a functional perspective without any of the brian analogies.
1. Fully Connected Layer
stretch all the pixels out, then multiply it by a weight matri and get the activation.
![image](https://github.com/user-attachments/assets/bc51a2db-3c61-4a93-b27e-24a3c668d755)
2. Convolution Layer
- keep the structure of images, still 3-dimensional input.
- convolve the filter with the image.
- filters always extend the full depth of the input volume, just slide over the image spatially, for each depth, computing dot products.
3. convolve parameters:
- size of filter: F
- stride: number of pixels will skip in each step
- size of each output: (N-F)/stride + 1, input: N\*N, filter : F*F
- pad: zero pad the border so we can place a filter centerd at the upper right-hand pixel location. usually 0. 
- output: ((N+pad*2-F)/stride+1) \* ((N+pad\*2-F)/stride+1) \* number of filters. each filter will do dot product through the entire depth of input volume, and produce one number
4. shape of filter:
- input image: 32\*32*3; 10 5*5 filters
- actually, each filter gona do convole to all depth of input image, so each filter is 5\*5*3
5. number of parameters for a layer:
- input: 32\*32*3; filter: 10 of 5*5
- total is 10 * (5\*5*3 + 1)
- - - - - - - -
summary
![image](https://github.com/user-attachments/assets/52776b1d-21ec-4ebc-8d69-01ec879db50d)
6. 1*1 convolution layers
- input: 56*56\*64
- filters: 1*1 with 32
- output: 56*56\*32

7. pooling layer
- goal: make the representations smaller and more manageable, 'cause the depth of activation map increase, we should make the size of activation map smaller.
- operate over each activation map independently:
- downsampling: 224*224->112\*112
- output depth = input depth
- output size of pooling![image](https://github.com/user-attachments/assets/9f91f422-7f62-4a30-9042-0f63f3aa97be)
- experiences: max pool + no pad

## Summary
![image](https://github.com/user-attachments/assets/b644ba30-d71c-4d48-8150-887fbf743de8)
