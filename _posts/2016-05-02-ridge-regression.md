---
layout: post
title: Ridge Regression
category: Machine Learning Algorithm
permalink: ml/ridge_regression
---

# Ridge Regression

Ridge regression is linear regression with regularization.

$$obj:Error= \sum_{i=1}^n(y^{(i)}-w^T\cdot x^{(i)})^2+\lambda||w||_2$$

Also, $Error=(y-X^T\cdot w)^T\cdot (y-X^T\cdot w)+\lambda||w||_2$

But there is one thing to be aware. We only penalty $w_i \quad i \in {0,1,2...p}$ when we do standarization for every feature. On the other hand, we will not penalty $w_0$.

### 解法一：梯度下降法(Gradient Descent Method)

$$
\begin{cases}
Grad(w_i)=-2\sum_{i=1}^n(y^{(i)}-w^T\cdot x^{(i)})x^{(i)}+2\lambda w_i \quad i\in{(1,2,3,p)}\\\
Grad(w_0)=-2\sum_{i=1}^n(y^{(i)}-w^T\cdot x^{(i)})x^{(i)}
\end{cases}
$$

Repeat until converage{
$$
\begin{align}
w_i &= w_i+2\sum_{i=1}^n(y^{(i)}-w^T\cdot x^{(i)})x^{(i)}-2\lambda w_i \quad i\in{(1,2,3,p)} \\
w_0 &= w_0 +2\sum_{i=1}^n(y^{(i)}-w^T\cdot x^{(i)})x^{(i)}
\end{align}
$$
}

### 解法二：解析法(Closed Form Solution)

$$Grad(w_i)=-2X(y-X^T\cdot w)+2\lambda w$$
$$set \quad Grad(w_i)=0$$

Then

$$
\begin{align}
& -2X(y-X^T\cdot w)+2\lambda w=0 \\
& (X\cdot X^T+\lambda I^{mod})w=X\cdot y \\
& w = (X\cdot X^T+\lambda I^{mod})^{-1}\cdot X \cdot y
\end{align}
$$

$$I^{mod}= \begin{pmatrix}
0 \quad 0 \quad 0 \quad \cdots \quad 0 \\
0 \quad 1 \quad 0 \quad \cdots \quad 0 \\
\vdots \quad \vdots \quad \vdots \quad \ddots \quad \vdots \\
0 \quad 0 \quad 0 \quad \cdots \quad 1
\end{pmatrix}
$$

In my view, ridge regression can be called as a machine learning algorithm.