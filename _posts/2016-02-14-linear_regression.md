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
X & 所有样本的特征合集， X=[x^{(1)},x^{(2)},...,x^{(n)}]^T \space X\in \mathtt{R}^{n\times (p+1)} \\
y & 所有样本的标签合集， y=[y^{(1)},y^{(2)},...,y^{(n)}]^T \\
w & 参数向量 w=(w_0,w_1,...,w_p)^T \\
w_j & 第j维参数 \\
\end{array}
$$

# 线性回归

$$H(x) = X\cdot w$$

$$obj: Min\ Error=(y-X\cdot w)^T\bullet (y-X\cdot w)$$
同样 $Error = \sum^n_{i=1}(y^{(i)}-w^T\cdot x^{(i)})^2$

这是一个无约束条件下的最优化问题

### 解法一：梯度下降法(Gradient Based Descent Method)


$$Set\quad J(w)=\sum^n_{i=1}(y^{(i)}-w^T\cdot x^{(i)})^2$$

$$Grad(w_k)=\frac{\partial J}{\partial w_k}=-2\sum^n_{i=1}(w^T\cdot x^{(i)}-y^{(i)})\cdot x^{(i)}_{k}\quad k\in(1,2,\ldots,p+1)$$



Repeat until convergence{

$$w_k=w_k-\alpha\times Grad(w_k) k\in (1,2,\ldots,p+1)$$
    
}

$\alpha$表示学习率

### 解法二：解析解法(Close Form Solution)

$$ 
\begin{align}
Grad(w)&=\frac{\partial{(y-X\cdot w)^T\cdot (y-X\cdot w)}}{\partial{w}} \\
Grad(w)&=\frac{\partial{(y-X\cdot w)^T\cdot (y-X\cdot w)}}{\partial{(y-X\cdot w)}}\frac{\partial{(y-X\cdot w)}}{\partial{w}} \\
Grad(w)&= 2(y-X\cdot w)\cdot X^T \\
Grad(w)&=-2X^T \cdot(y-X \cdot w) 
\end{align}
$$

$$Set\quad Grad(w_i)=0$$

Then

$$
\begin{align}
&-2X^T(y-X \cdot w) =0 \\
& X^T\cdot X \cdot w = X^T \cdot y \\
& w = (X^T \cdot X)^{-1} \cdot X^T \cdot y 
\end{align}
$$


