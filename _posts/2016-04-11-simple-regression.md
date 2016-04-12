---
layout: post
title: simple regression
permalink: /ml/simple-regression
category: machine learning
---

# Simple Regression

Hypothesis: $H(x)=w_0+w_1x$

obj: $min \space E = \sum_1^n{(y_i-(w_0+w_1x_i))^2}$

## Method 1: form solution

This is just for simple regression, matrix form solution will show in mutiple regression.

Let $\frac{\partial{E}}{\partial{w_0}}=0$ and $\frac{\partial{E}}{\partial{w_1}}=0$

联立方程组
\begin{cases}
-2\sum_1^n(y_i-w_0-w_1x_i)=0\\-2\sum_1^nx_i(y_i-w_0-w_1x_i)=0
\end{cases}

可推导出
\begin{cases}
w_0=\frac{\sum_1^ny_i}{n}-w_1\frac{\sum_1^nx_i}{n}\\ \sum_1^nx_iy_i-w_0\sum_1^nx_i-w_1\sum_1^nx_i^2=0
\end{cases}

结果是
$$w_1 = \frac{n\sum_1^nx_iy_i-\sum_1^nx_i\sum_1^ny_i}{n\sum_1^nx_i^2-(\sum_1^nx_i)^2}$$
$$w_0=\frac{\sum_1^ny_i}{n}-w_1\frac{\sum_1^nx_i}{n}$$

## Method 2: Gradient Descent
$$\frac{\partial{E}}{\partial{w_0}}=-2\sum_1^n(y_i-w_0-w_1x_i)$$
$$\frac{\partial{E}}{\partial{w_1}}=-2\sum_1^nx_i(y_i-w_0-w_1x_i)$$

repeat until converge{
$$w_0 = w_0+η*2\sum_1^n(y_i-w_0-w_1x_i)  $$
$$w_1 = w_1 +η*2\sum_1^nx_i(y_i-w_0-w_1x_i)$$
}

η表示是学习率










