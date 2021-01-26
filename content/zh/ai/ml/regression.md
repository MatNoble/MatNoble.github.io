+++
title = "线性回归"
date = "2021-01-24T00:20:33+00:00"
description = "多项式拟合"
categories = ["机器学习"]
tags = ["回归","梯度下降"]
keywords = ["线性回归","梯度下降","归一化","标准化","正则化","矩阵","MatNoble"]
toc = true
mathjax = true
series = ["AI"]
+++

## 多项式拟合

### 问题简述

拟合数据点 $\hat{y_j}$
$$
\hat{y_j} = \sum_{i=0}^{n-1} \omega_i * x_j^i
$$

 拟合 $m$ 个数据点，并写成向量的形式

$$
\hat{\boldsymbol{y}} = \mathbf{X} \cdot \boldsymbol{\omega}
$$

其中

$$
\mathbf{X} = 
\begin{bmatrix}
1 & x_1 & \cdots & x_1^{n-1}  \\\\ 
1 & x_2 & \cdots & x_2^{n-1}  \\\\
\vdots & \vdots & & \vdots \\\\
1 & x_m & \cdots & x_m^{n-1}
\end{bmatrix}
$$

### 程序设计
{{< notice note >}}
输入： $m$ 个相异的数据点 $(\boldsymbol{x}, \boldsymbol{y})$

输出： $\boldsymbol{\omega}$
{{< /notice >}}

#### 归一化 & 标准化

#### 梯度下降

#### AdaGrad

#### 正则化

1. $L2$ 正则化

2. $L1$ 正则化

[向量 p 范数](https://matnoble.me/math/linear-algebra/vector-and-matrix-norm/#p-%E8%8C%83%E6%95%B0)

{{< imgcap src="https://cdn.jsdelivr.net/gh/MatNoble/Images/linear-regression.gif" title="回归" >}}

{{< imgcap src="https://cdn.jsdelivr.net/gh/MatNoble/Images/20210126200259.png" title="回归" >}}

[GitHub 源码](https://github.com/MatNoble/MachineLearningNote/blob/main/regression.py)

问题：
数据归一化！

## 实践