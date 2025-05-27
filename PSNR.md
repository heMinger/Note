## 定义
PSNR(Peak Signal-to-Noise Ratio) 峰值信噪比，

$$
\text{MSE} = \frac{1}{WH} \sum_{i=1}^{W} \sum_{j=1}^{H} \left( I(i,j) - \hat{I}(i,j) \right)^2
$$
$$
\text{PSNR} = 10 \cdot \log_{10} \left( \frac{MAX_I^2}{\text{MSE}} \right)
$$

$$MAX_I^2$$ 代表了峰值信号，也就是signal, MSE代表了Error，对应PSNR中的signal-to-noise

$$
\text{PSNR} = 10 \cdot \log_{10} \left( \frac{MAX_I^2}{\text{MSE}} \right)
$$

## 分析
1. MSE越小，PSNR越大，表示图像越接近原始图像
2. 通常PSNR在30-50 dB区间，越高越好
3. 通常用来衡量两幅图像之间的差异大小，通常评估原始图像和重建图像之间的相似度
4. pixel-level: 基于MSE，进行逐像素比较，**不考虑结构、纹理、语义信息**
5. 不考虑人类视觉系统(HVS)的感知特性，对噪点敏感；但*对结构扭曲不敏感*

## 优缺点
1. 优点
- 实现简单、计算高效
- 可重复、可比较
- 通常利用benchmark

2. 缺点
- 不考虑视觉感知、不适合评估主观图像质量
- 对亮度漂移，微小的位置移动敏感
- 对像素的结构信息完全无视

## PSNR与MSE
|指标|MSE|PSRN|
|--|--|--|
|含义|平均像素误差平方|峰值信号与误差的对比度量|
|大小|越小越好|越大越好|
|比较性|不同图像范围下难以比较|可用于不同图像间的相对评估|

## 对比
|指标|类型|简介|
|--|--|--|
|PSNR| pixel-level| 逐点差异，不感知结构或语义|
|SSIM| structural| 考虑亮度、对比度、结构相似度，更符合人眼感知|
|LPIPS| perceptual| 基于深度特征感知相似度，更拟合主观感知|
|FID/KID| distribution-level| 多图像集之间的分布距离，用于生成模型评估|
