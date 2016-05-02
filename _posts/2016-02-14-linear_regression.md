---
layout: post
title: Linear Regression
category: Machine Learning Algorithm
permalink: ml/linear_regression
---

# Linear Regression

### 数学符号规范

$$
\begin{array}{c|l}
x_j &  第j维特征 \\
x & 一条样本的特征变量 x=(1,x_1,x_2,...,x_n)^T \\ 
x^{(i)} & 第i条样本 \\
x_j^{(i)} & 第i条样本的第j维特征 \\
y^{(i)} & 第i条样本的结果 \\
X & 所有样本的特征合集， X=[x^{(1)},x^{(2)},...,x^{(n)}] \space X\in \mathtt{R}^{n\times (p+1)} \\
y & 所有样本的标签合集， y=[y^{(1)},y^{(2)},...,y^{(n)}]^T \\
w & 参数向量 w=(w_0,w_1,...,w_p)^T \\
w_j & 第j维参数 \\
\end{array}
$$

# 线性回归

$$H(x) = X^T\cdot w$$

$$obj: Min\ Error=(y-X^T\cdot w)^T\bullet (y-X^T\cdot w)$$
同样 $Error = \sum^n_{i=1}(y^{(i)}-w^T\cdot x^{(i)})^2$

这是一个无约束条件下的最优化问题

### 解法一：梯度下降法(Gradient Based Descent Method)


$$Set\quad J(w)=\sum^n_{i=1}(y^{(i)}-w^T\cdot x^{(i)})^2$$

$$Grad(w_i)=\frac{\partial J}{\partial w_i}=-2\sum^n_{i=1}(w^T\cdot x^{(i)}-y^{(i)})\cdot x^{(i)}\quad i\in(0,1,2,\ldots,n)$$



Repeat until convergence{

$$w_i=w_i-\alpha\times Grad(w_i) i\in (1,2,\ldots,n)$$
    
}

$\alpha$表示学习率

### 解法二：解析解法(Close Form Solution)

$$ Grad(w_i)=-2X(y-X^T \cdot w) $$

$$Set\quad Grad(w_i)=0$$

Then

$$
\begin{align}
&-2X(y-X^T \cdot w) =0 \\
& X\cdot X^T \cdot w = X \cdot y \\
& w = (X \cdot X^T)^{-1} \cdot X \cdot y 
\end{align}
$$


