---
layout:     post
title:      Jing's Notes - CNN 学习小结(1)
subtitle:   背景和算法原理
date:       2019-04-02
author:     Jing
header-img: img/post-bg-CNN.jpg
catalog: true
export_on_save:
html: true
tags:
    - Machine Learning
    - Notes
    - CNN
---

> CNN 学习小记


# 卷积神经网络(CNN) --- 背景和算法原理
### 背景
Fukushima(1980)--- Neo-Congnitron;<br>
LeCun(1998)--- Convolutional Neural Networks(CNNs, or ConvNets)

CNNs和传统神经网络相似，都由神经元组成，神经元中有能进行学习的权重和偏差。每个神经元都有输入数据，与权重进行内积运算后传入激活函数运算。整体网络仍然由一个可导的评分函数推动，输入原始图像像素，输出不同类别的评分。而Loss函数同样出现在网络的最后一层。

不同之处在于CNN算法中使用图像作为输入数据，在此假设下对神经网络结构中增加了一些特有属性，使向前传播函数得以高效实现，并减少了网络结构中参数的数量。

由于图像通常有![](http://latex.codecogs.com/gif.latex?\\1000^2)个像素，即一个图像就有高达![](http://latex.codecogs.com/gif.latex?\\1000^2)个数据点/特征，相应的高维权重空间很难处理。而实际上，对于spatial patterns来说，并不是每一个数据点/特征都重要。这些数据点/特征会有大量的相同性质，因此如果对原始图像像素进行适当预处理，如只提取图像中spatial correlation或patterns，可以大大降低权重空间的维度。
### 算法结构
<img src="http://yuml.me/diagram/scruffy/class/[note: Image {bg:cornsilk}],[Input]<>1-orders 0..*>[Order], [Order]++*-*>[LineItem], [Order]-1>[DeliveryMethod], [Order]*-*>[Product], [Category]<->[Product], [DeliveryMethod]^[National], [DeliveryMethod]^[International]" >

### 算法原理
卷积神经网络(Convolutional Neural Network)的主要构成：
1. 卷积层(Convolutional Layer)
2. 池化层(Pooling Layer)
