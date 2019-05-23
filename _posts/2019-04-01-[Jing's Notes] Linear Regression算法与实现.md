---
layout:     post
title:      Jing's Notes - Linear Regression 算法与实现
subtitle:   算法原理与Python实现
date:       2019-04-01
author:     Jing
header-img: img/post-bg-CNN.jpg
catalog: true
export_on_save:
html: true
tags:
    - Machine Learning
    - Notes
    - Linear Regression
---


> Regressions


## 1. Linear Regression
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

##### 1.2. 多变量线性回归
当然大部分的情况下，因变量不可能只与单一特征有关，我们需要考虑多变量(multiple variables)问题。现假设有$n$个特征，记$x_j^{(i)}$为第$i$个训练数据的第$j$个特征。此时相应的预测函数 $p(x)$和损失函数 $L(c_0,c_1,...,c_n)$如下:

$$p(x) = c_0 + c_1x_1 + c_2x_2 + ... + c_nx_n,\quad L(c_0,c_1,...,c_n)=\sum_{i=1}^{m}(p(x^{(i)})-y^{(i)})^2.$$

而对于最优化问题$\min_{c_0,c_1,...,c_n}: L(c_0,c_1,...,c_n),$ 使用正规方程法(normal equation)可以解析地求出最优解为:
$$ \mathbf{c} = (c_0,c_1,...,c_n)^T = (X^TX)^{-1}X^TY,$$

$$X =
 \begin{vmatrix} 1 & x_1^{(1)} & ...& x_n^{(1)} \\
   1 & x_1^{(2)} & ...& x_n^{(2)} \\
    & &  ...& \\
   1 & x_1^{(m)} & ...& x_n^{(m)}\\
  \end{vmatrix}
  , Y = (y^{(1)},y^{(2)},...,y^{(m)})^T.$$

**具体求解过程**: 同单变量的情况一样，我们需要求解 $c$ 使得$\nabla L = 0$。
  * 将$L(c_0,c_1,...,c_n)$写成矩阵形式:
  $$L(\mathbf{c})=\sum_{i=1}^{m}(p(x^{(i)})-y^{(i)})^2=(X\mathbf{c} - Y)^T(Xc - Y);$$
  * 对$\mathbf{c}$求导得:

  $$\begin{align}
  \nabla L &= \nabla\left((X\mathbf{c} - Y)^T(Xc - Y)\right)\\
  &= \nabla\left(\mathbf{c}^TX^TX\mathbf{c} -\mathbf{c}^TX^TY - Y^TX\mathbf{c}+ Y^TY\right)\\
  &= \nabla tr\left(\mathbf{c}^TX^TX\mathbf{c} -\mathbf{c}^TX^TY - Y^TX\mathbf{c}+ Y^TY\right)\\
  &= \nabla \left(tr\mathbf{c}^TX^TX\mathbf{c} -2trY^TX\mathbf{c}\right)\\
  &= \left(X^TX\mathbf{c} + X^TX\mathbf{c} -2Y^TX\right)\\
  &= 2\left(X^TX\mathbf{c} - Y^TX\right)\\
  \end{align}$$


##### 1.3. 梯度下降法(Gradient Descent)
在大部分情况下，最优化问题无法求得解析解，需要使用数值优化方法求解。梯度下降法就是其中一类经典方法，通过迭代
$$c := c -\alpha \nabla L$$

从而使得$L$取得最小值。这里$\alpha$为学习步长(Learning rate)。

梯度下降法的收敛(具体数值上表现为，目标函数每次迭代减小值很小,如小于$10^{-3}$)取决于迭代次数和learning rate。

**迭代次数**:
1. 太少，算法没有收敛就停止。
2. 太多，浪费资源。

**learning rate**:
1. 太小，算法收敛速度慢。
2. 太大，迭代过程中可能会错过(jump over)最优解。

**Remark**: 在多变量问题中，不同特征变量间由于单位不同，可能在数值上相差较大，这里需要进行去量纲化，这个过程也叫 **数据规范化(Feature Scaling)** 。对数据做此处理后能够减少梯度下降法的迭代次数，提高算法收敛速度。使用平均值(mean value)是一种常见的数据规范化方法: 求出特征变量的均值(mean)和标准差(std)，则规范化后的特征变量为 $x = \frac{(x-mean)}{std}$。

## 2. Lasso Regression

## 3. Ridge Regression

## 4. Elastic net

## 5. Polynomial Regression
对于一些线性规划结果不理想的情况下，通过对某些特征变量进行联合得到新的特征变量，有时能得到更好的结果，这便是多项式回归(Polynomial Regression)。新的特征变量可以是已有特征变量的多项式:

$$p(x) = c_0 + c_1x + c_2x^2 + c_3x^3 + ...$$

要注意：结合实际情况决定需要使用的多项式的次数(degree)，如在房价问题中，若特征变量是房屋面积，则不应使用二阶多项式，否则将会出现房屋面积增加，房价减小的情况，这不符合实际。
