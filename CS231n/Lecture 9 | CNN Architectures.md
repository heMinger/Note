# CNN Architecture

## date: 4/11
writer: MingheLi

## LeNet-5
![image](https://github.com/user-attachments/assets/35526493-2122-40ce-8448-8daa08ea6b28)
## AlexNet
### architecture: conv layer -> pooling layer -> normlization -> ... -> FCN
2. Input 227\*227*3
3. CONV1:
- 96 11*11 filters at stride 4, pad 0
- output: 55*55\*96
- number of parameters: (11*11\*3 + 1) * 96
4. MAX POOL1
- 3*3 filters applied at stride 2
- output: 27*27\*96
- number of parameters: 0
5. NORM1
6. CONV2
- 256 5*5 filters at stride 1, pad 2
- (27 + 4 - 5) / 1 + 1 = 27
- output: 27*27\*256
- number of parameters: (5*5\*96 + 1) * 256
1. MAX POOL2
- 3*3 filters at stride 2
- (27-3)/2 + 1 = 13
- output: 13*13\*256
- number or paramers: 0
3. NORM2
4. CONV3
- 384 3*3 filters at stride 1, pad 1
- (13-3+2)/1 + 1=13
- output: 13*13\*384
- number of parameters: (3*3\*256+1)*384
5. CONV4
- 384 3*3 filters at stride 1, pad 1
- (13-3+2)/1+1=13
- output: 13*13\*384
- number of parameters: (3*3\*384+1)*384
6. CONV5
- 256 3*3 filters at stride 1, pad 1
- (13 - 3 + 2)/1 + 1=13
- output: 13*13\*256
- number of parameters: (3*3\*384+1)*256
7. MAX POOL3
- 3 * 3 filters at stride 2
- (13 - 3)/2+1 = 6
- output: 6*6\*256
- number of parameters: 0
8. FC6
9. FC7
10. FC8
### details
![image](https://github.com/user-attachments/assets/422ec556-94e8-4fda-aaf3-ecc40ff67fb1)
## VGGNet
1. **smaller filters, deeper networks. more non-linearities, fewer parameters.**
2. only 3*3 Conv stride 1, pad 1 and 2\*2 MAX POOl stride 2
3. Q: why use smaller filters?
- Stack of three 3*3 conv(stride 1) layers has same effective receptive field as one 7\*7 conv layer.
- deeper -> more non-linearities
- fewer parameters: $3 \* (3^2C^2)$ vs $7^2C^2$ for C channels per layer.
4. full network
![image](https://github.com/user-attachments/assets/6ddf648b-1640-42f3-b360-8a377ea52a4d)

## GoogLeNet
1. deeper network, with computational efficiency
2. details
![image](https://github.com/user-attachments/assets/3c916c2a-81f8-419a-b61d-ca37cd513fab)
3. Inception module
- motivation: want to design a good local network typology, satck a lot of typologies one on top of each other.
- ![image](https://github.com/user-attachments/assets/0ae6ffc3-2057-409a-a99b-ab81498f45d0)
- What's the problem with this?\
(1) computational complexity
![image](https://github.com/user-attachments/assets/e361f428-3c02-4060-aa19-06acd9c3f557)
![image](https://github.com/user-attachments/assets/369f27a3-854b-4487-9215-0cf3fd0de40c)
4. 1*1 Convolutions: preserve spatial dimensions, reduce depth
5. dimension reduction
- ![image](https://github.com/user-attachments/assets/d101da76-ce33-4a33-ba3e-b06b1f728f4b)
## ResNet
1. very deep networks using residual connections.
2. when we continue stacking deeper layers on a "plain" convolutional neural network, 56-layer networks perform worse than 20-layer network both on training dataset and test dateset, so it's not caused by over-fitting.
3. solution: Residual block
 ![image](https://github.com/user-attachments/assets/be8b094e-2d27-4ed2-9eaf-ecb950351426)
- it's hard to learn H(x), so we turn ti learn what is it that we need to add or subtract(F(x)) to our input(x) as we move on to the next layer. so, F(x) is residual, is what we learn and modify on x, to approximate H(x).
4. Full ResNet architecture:
- stack residual blocks
- every residual block has two 3*3 conv layers.
- periodically, double number of filters and downsample spatially using stride 2.
- additional conv layer at the beginning
- no FC layer at the end. only FC 1000
