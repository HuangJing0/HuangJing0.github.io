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

**Remark** 除了最小二乘函数外，损失函数的其他定义。

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
  &= \left(X^TX\mathbf{c} + X^TX\mathbf{c} -2X^TY\right)\\
  &= 2\left(X^TX\mathbf{c} - X^TY\right)\\
  \end{align}$$

  * 得到normal equation: $X^TX\mathbf{c} - X^TY = 0$，解得: $\mathbf{c} = (X^TX)^{-1}X^TY$。

**Remark** 若矩阵$(X^TX)$不可逆，此时有两种情况:
* 特征变量有冗余，即有部分特征向量间线性相关(linear dependent);
* 太多特征变量，即$m\leq n$。

这时需要删除多余的特征量或者使用正则项。


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

## 2. Polynomial Regression
对于一些线性规划结果不理想的情况下，通过对某些特征变量进行联合得到新的特征变量，有时能得到更好的结果，这便是多项式回归(Polynomial Regression)。新的特征变量可以是已有特征变量的多项式:

$$p(x) = c_0 + c_1x + c_2x^2 + c_3x^3 + ...$$

要注意：结合实际情况决定需要使用的多项式的次数(degree)，如在房价问题中，若特征变量是房屋面积，则不应使用二阶多项式，否则将会出现房屋面积增加，房价减小的情况，这不符合实际。


## 3. Lasso Regression
##### 背景
以最小二乘为基础的线性回归模型虽然有很好的解析性，但由于以下两个原因没有很好的数据分析能力。
1. 预测精度: 最小二乘法虽是无偏估计，但当特征变量间线性相关(多重共线性)时，其方差会很大。若通过删除多余特征变量来解决此问题，就是以一定的有偏为代价来改进预测精度。
2. 解释能力: 当特征变量个数很多时，希望用一个较小的变量模型得到更好的结果。

针对以上问题，改进方法有: 删除多余的特征量或者使用正则项。这两种方法各有利弊:删除多余的特征量会导致模型的不稳定，观测数据的一个微小变动就导致需要选择一个新模型，但由于模型变量少了，提高了模型的解释能力；使用正则项是一个连续方法，在不抛弃任何一个变量的情况下，减小回归系数，使得模型相对稳定，但这使得模型更加复杂，解释能力差。

基于此，Lasso(Least Absolute Shrinkage and Selection Operator)作为一种变量选择技术，使用 **回归系数的$l_1$范数**，使得一些系数变小，一些绝对值较小的系数甚至直接变为$0$，也算是同时结合了删除多余的特征量和使用$l_2$正则项的优点。

##### 原理
Lasso回归(套索回归)作为一种用于估计稀疏参数的线性模型，尤为适用于参数数目缩减(故在压缩感知中应用广泛)。 **数学上，Lasso是在线性模型上加上了一个$l_1$正则项**:

$$L(\mathbf{c})=\sum_{i=1}^{m}(p(x^{(i)})-y^{(i)})^2 + \lambda\|\mathbf{c}\|_ {1}.$$

其中参数$\lambda$控制了稀疏参数估计的惩罚程度

##### 应用
**基于Lasso的特征选择**: 由于Lasso回归后的参数大部分为$0$，而那些不为$0$的参数对应的特征变量，可以作为其他的模型的特征。可以在不改变模型的准去率情况下减小特征维度。

最具现实意义的应用: 文本分类。文本的原始特征维度几乎是整个字典，而一个文本的单词量基本上在$100~1000$之间，这使得文本分类中的设计矩阵是一个极其稀疏的矩阵(实际测试中，其稀疏度可以达到$1%$以下)。这类问题中，$l_1$正则项十分有用。(相关内容参见)


## 4. Ridge Regression
**数学上，Ridge回归是在线性模型上加上了一个$l_2$正则项**:

$$L(\mathbf{c})=\sum_{i=1}^{m}(p(x^{(i)})-y^{(i)})^2 + \lambda\|\mathbf{c}\|_ {2}.$$
## 5. Elastic net
