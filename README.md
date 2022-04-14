# Survey-On-CVPR2022-NeRF-Papers-chs

## NeRF: Representing Scenes as Neural Radiance Fields for View Synthesis

### 研究成果

一个神经网络，以同一个物体/场景在不同视角下的图像及其对应视角作为数据集，生成这个物体/场景在全新的视角下的新的图像. 

### 实现方式

![NeRF structure](/Assets/Images/NeRF%20structure.png)
需要训练的网络只有(a)到(b)的这一部分，这一部分的网络用于估计在给定的视角和位置下，一点的密度和颜色. 

在(c)中，本文从摄像机的视角发射数条光线，在光线的路径上对最终呈现的色彩进行积分，积分采用这样一个公式：
![NeRF Formula 1](/Assets/Images/NeRF%20Formula%201.png)
$\sigma_j$和$\delta_j$分别表示第$j$个采样点的密度和到上一个采样点的间隔，从而$T_i$就表示从光线源点（屏幕）到第$i$个采样点的光线衰减. 提出这个系数的目的是为了让离屏幕更近的点对色彩的影响更大，同时让光线在遇到第一个具有密度的采样点之前都不衰减. $(1-e^{-\sigma_i\delta_i})$这一项把一点对色彩的影响映射到[0,1)这个区间. $\mathbb{c_i}$是该采样点的颜色. 

(d)表示这个网络的损失函数就是图像上每条光线最终呈现的颜色与真实颜色之差的2-范数之和，神经网络训练的后向传播阶段将这个损失经过可微的(c)传回神经网络并修正网络的权重. 

### 网络优化

#### 位置编码

如果仅仅以三维空间中的坐标作为输入，容易对低频色彩的输入产生过拟合，所以本文将每个空间维度上的坐标分解成多个不同频率的编码，再将其作为神经网络的输入：
![NeRF Formula 2](/Assets/Images/NeRF%20Formula%202.png)

#### 分级采样

每次都在光线路径上完整采样效率低下，所以本文将采样过程分成了粗采样和精采样两个阶段，粗采样在光线路径上均匀采样但设置较大的间隔，随后再根据粗采样的结果选定精采样区间，以略过空白和被遮挡的空间. 最后的损失函数也相应变为粗采样得到的颜色与精采样得到的颜色之和. 

## Point-NeRF: Point-based Neural Radiance Fields

（待整理）

## FENeRF: Face Editing in Neural Radiance Fields

（待整理）

## NeRFusion: Fusing Radiance Fields for Large-Scale Scene Reconstruction

（待整理）

## GeoNeRF: Generalizing NeRF with Geometry Priors

（待整理）

## CLIP-NeRF: Text-and-Image Driven Manipulation of Neural Radiance Fields

（待整理）
