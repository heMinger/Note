## 《Perceptual Losses for Real-Time Style Transfer and Super-Resolution》
[[paper](https://arxiv.org/pdf/1603.08155)]
Justin Johnson; ..

## Abstract
1. previous methods
- feed-forward CNNs using a **per-pixel** loss between the output and ground-truth images.
- **pereptual** loss based on high-level features extracted from pretrained networks.
2. proposal
- perceptual loss functions + feed-forward networks 
  
$\color{red}{\textit questions}$
1. generative model? (我执着于判断这是不是生成式模型是因为CycleGAN说它是生成式模型)

## Introduction
1. method1: feed-forward netword + per-pixel loss
- cons: fast, efficient at test-time, and requiring only a forward pass through the trained network.
- pros: do not capture perceptual differences between output and ground-truth images.
2. method2: perceptual loss functions based on differences between high-level image feature representations extracted from pretrained CNNs.
- cons: cable to generate high-quality images
- pros: slow, inference requires solving an optimizing problem. need to GD a white noise image.
3. this paper
- combine the benefits of these two approaches
- train **feed-forward transformation networks** for **image transformation** tasks.
- using perceptual loss functions

## Related Work
### Feed-forward image transformation
1. get inspiration and use, in-network downsampling + upsampling
- downsampling: reduce the spatial extent of feature maps
- upsampling: produce the final output image
2. 

$\color{red}{\textit questions}$
1. downsampling+upsampling $\ne$ generative  ??

### Perceptual optimization
1. optimization
- to generate images where the objective is perceptual
- similar optimization techniques can be used to generate high-confidence fooling images.
2. invert features
- by minimize a feature reconstruction loss
3. feed-forward nn to invert convolutional features
- quickly approximating a solution to the optimization problem
- difference: not per-pixel reconstruction loss instead directly optimize the feature reconstruction loss

### Style Transfer
1. previous
- computationally expensive
- since each step of the optimization problem requires a forward and backward pass through the pretrained network
2. solution: feed-forward network, quickly approximate solutions to previous optimization problem.

### Image super-resolution
1. recent achievement
- excellent performance on
- single-image super-resolution
- using a three-layer cnn
- trained with a per-pixel Euclidean loss.
