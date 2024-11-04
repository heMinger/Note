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
