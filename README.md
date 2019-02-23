# DCGAN-for-light-field-compressive-sensing
 The construction results show too much noise on single frame image when I complete the compressive sensing based on DCGAN model.

## 理论：
* 对抗生成网络动物园中的[DCGAN](https://github.com/Newmu/dcgan_code)和[CSGAN](https://github.com/po0ya/csgan)
* 压缩感知理论

## 网络结构：
* 首先对真实图像用高斯随机观测矩阵进行欠采样，得到一张低清图像。
* 后接GAN中的生成器配合优化器搭建生成网络，重构图像。

PS：根据压缩感知理论，当满足有限等距性质RIP后，便可以无失真恢复真实图像，高斯随机观测矩阵可以满足RIP。
使用神经网络求解压缩感知重建问题的优点在于，可以不用使用LASSO或者匹配追踪求出原始信号X的稀疏表示，直接恢复出真实图像。并且有cs数学理论的铺垫。

## 实验：
将一张光场图分解后生成的一张[子孔径图像](https://github.com/liangjiubujiu/DCGAN-for-light-field-compressive-sensing/blob/master/01.jpg)进行降采样，模拟根据较低采样率的图像，重建出高分辨率的图像的过程。

## 结果：

<img src="https://github.com/liangjiubujiu/DCGAN-for-light-field-compressive-sensing/blob/master/reconstruction.jpg" height="400" width="300" />
 
由于要将图片拉成列向量，m维向量信号需要有m·n规模的观测矩阵配合，n>m。如果m过大会爆内存，因此去图像小块进行重建。上方是重建图像，下方是真实图像，对比可知，重建出的图像噪声很大，减弱噪声的优化方法没有想出来。分析可能的原因：
* 训练数据只有一张子孔径图，神经网络退化成了单纯的迭代或者暴力求解。
* 生成网络本身是拟合真实数据的高维分布，因此测试结果存在自我发挥创造像素的功能。
