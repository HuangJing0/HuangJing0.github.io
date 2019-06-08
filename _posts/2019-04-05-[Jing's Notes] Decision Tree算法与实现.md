---
layout:     post
title:      Jing's Notes - Decision Tree
subtitle:   算法原理与Python实现
date:       2019-04-05
author:     Jing
header-img: img/post-bg-CNN.jpg
catalog: true
export_on_save:
html: true
tags:
    - Machine Learning
---


> Minimizing your error while Regularizing your parameters.


## 1. Logistic Regression
#### 介绍
线性回归（linear regression）通常假设特证满足线性关系，根据给定的训练数据估计出未知的模型参数，得到一个线性模型，并利用此模型进行预测。在统计学中，线性回归是利用本质为最小二乘函数的线性回归方程对一个或多个自变量和因变量之间关系进行建模的一种回归分析，该函数是一个或多个称为回归系数的模型参数的线性组合。
#### 算法结构

<img src="https://raw.githubusercontent.com/HuangJing0/HuangJing0.github.io/master/img/post-LR1-structure.png">

#### 算法原理
##### 1.1. 单变量线性回归
因变量可能由一个或多个变量决定，现仅考虑单一变量对因变量的关系。以房屋面积x和房价y为例：

size in feets^2 (x) | price in 1000's (y) |
:-: | :-:
2014 | 460
1416 | 232
1534 | 315
852 | 178
...|...

假设我们有m个训练数据(training data)，$x$作为输入变量或特征变量，$y$作为输出变量或目标变量。首先定义线性的预测函数(predict function) $p(x)$ 和损失函数(loss function) $L(c_0,c_1)$:

$$p(x) = c_0 + c_1x,\quad L(c_0,c_1)=\sum_{i=1}^{m}(p(x^{(i)})-y^{(i)})^2.$$
则对应的最小二乘线性回归问题为:

$$\min_{c_0,c_1}: L(c_0,c_1)=\sum_{i=1}^{m}(p(x^{(i)})-y^{(i)})^2.$$

此问题的最优解$c_0, c_1$应满足:

$$\frac{\partial  L}{\partial c_j} = 0, \ j = 0,1.$$

可以解出:

$$c_1 = \frac{\sum_{i=1}^{m}x^{(i)}y^{(i)}-\frac{1}{m}\sum_{i=1}^{m}x^{(i)}\sum_{i=1}^{m}y^{(i)}}{\sum_{i=1}^{m}(x^{(i)})^2 - \frac{1}{m}(\sum_{i=1}^{m}x^{(i)})^2}, \ c_0 = \frac{1}{m}\sum_{i=1}^{m}y^{(i)} - c_1\frac{1}{m}\sum_{i=1}^{m}x^{(i)}.$$
