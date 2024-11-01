# Deep Learning Software
## Date: 1/11
writer: Minghe Li
## Overview
1. CPU vs GPU
2. Deep Learning Frameworks
- Caffe / Caffe2
- Theano / TensorFlow
- Torch / PyTorch
## CPU vs GPU
1. GPU built for rendering in graphics.
2. CPU with fewer cores, but each core is much faster and much more capable -> great at sequential tasks.
3. GPU with more cores, but each core is much slower and "dumber" -> great at parallel tasks.
4. CPU数据到GPU cost a lot

## Deep Learning Frameworks
![image](https://github.com/user-attachments/assets/79c2234a-8003-483a-b149-84838936bca5)
**point of deep learning frameworks**
1. easily build big computational graphs
2. easily compute gradients in computational graphs
3. run it all efficiently on GPU(wrap cuDNN, cuBLAS, etc)
### Caffe 
