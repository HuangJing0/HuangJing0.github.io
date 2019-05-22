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
##### 1. 单变量线性回归
因变量可能由一个或多个变量决定，现仅考虑单一变量对因变量的关系。以房屋面积x和房价y为例：

size in feets^2 (x) | price in 1000's (y) |
:-: | :-:
2014 | 460
1416 | 232
1534 | 315
852 | 178
...|...
假设我们有m个训练数据(training data)，x作为输入变量或特征变量，y作为输出变量或目标变量。首先定义线性的预测函数(predict function):

\[p(x) = \theta_0 + \theta_1x.\]
##### 2. 多变量线性回归


## 2. Lasso Regression

## 3. Ridge Regression

## 4. Elastic net

## 5. Polynomial Regression
