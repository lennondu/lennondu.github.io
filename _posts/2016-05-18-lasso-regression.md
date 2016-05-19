---
layout: post
title: Lasso Regression
category: Machine Learning Algorithm
permalink: ml/lasso_regression
---

# Lasso Regression

$$obj: Error = \sum_{i=1}^{n}(y^{(i)}-w^T \cdot x^{(i)})^2+\lambda \|\|w\|\|_1$$

Also, $Error = (y-X^T\cdot w)^T\cdot(y-X^T\cdot w)+\lambda \|\|w\|\|_1$

Due to the Lasso regularization, we can't get the gradient of the object function. Thus, we will use [**coordinate descent**](https://en.wikipedia.org/wiki/Coordinate_descent) instend of gradient descent.

### Solver: Coordinate Descent

We can't get the gradient of $\|x\|$ when $x=0$. Then we will use [subgradient](https://en.wikipedia.org/wiki/Subderivative) when $x=0$.

The subgradient of $\|x\|$ when $x=0$ is $[-1,1]$.

First, let's focus on the first part RSS.
$$\begin{align} 
\frac{\partial{RSS}}{\partial{w_j}} &=  -2\sum_{i=1}^nx^{(i)}_j(y^{(i)}-\sum_{k=0}^p{w_kx^{(i)}_k}) \\
&=-2\sum_{i=1}^{n}x^{(i)}_j(y^{(i)}-\sum_{k\neq j}w_kx^{(i)}_k)+2\sum_{i=1}^nw_j{x_j^{(i)}}^2 
\end{align}$$

Then, let's focus on the second part L1 norm.
$$\begin{align}
\frac{\partial{(L1)}}{\partial{w_j}} &= \begin{cases}
\lambda & when \space w_j>0 \\
[-\lambda,\lambda] & when \space w_j=0 \\
-\lambda & when \space w_j<0
\end{cases}
\end{align}$$

Finally, sum them up.

$$\begin{align}
\frac{\partial{E}}{\partial{w_j}} &= -2\sum_{i=1}^{n}x^{(i)}_j(y^{(i)}-\sum_{k\neq j}w_kx^{(i)}_k)+2w_j\sum_{i=1}^n{x_j^{(i)}}^2 +\begin{cases}
\lambda & when \space w_j>0 \\
[-\lambda,\lambda] & when \space w_j=0 \\
-\lambda & when \space w_j<0
\end{cases} 
\end{align}$$

In order to minize the error, we can set the gradient to zero.
Then, let's deal with every case.

$$set \space \sum_{i=1}^{n}x^{(i)}_j(y^{(i)}-\sum_{k\neq j}w_kx^{(i)}_k)=\rho_j \\
set \space \sum_{i=1}^n{x_j^{(i)}}^2=z_j
$$

#### Case 1: when $w_j>0$
$$\begin{align}
-2\rho_j+2w_jz_j+\lambda &= 0 \space when \space w_j>0 \\
w_j &= \frac{2\rho_j-\lambda}{2z_j} \space besides,\rho>\frac{\lambda}{2}
\end{align}$$

#### Case 2: when $w_j=0$
$$\frac{\partial{E}}{\partial{w_j}}=[-2\rho_j+2w_jz_j-\lambda,-2\rho_j+2w_jz_j+\lambda]$$

In order to set $\frac{\partial{E}}{\partial{w_j}}=0$, we need the range contain zero. So,
$$\begin{cases}
-2\rho_j+2w_jz_j-\lambda<=0 \\
-2\rho_j+2w_jz_j+\lambda>=0
\end{cases}$$

The result is that $\rho_j \in [-\frac{\lambda}{2},\frac{\lambda}{2}]$.

#### Case 3: when $w_j<0$
$$\begin{align}
-2\rho_j+2w_jz_j-\lambda &= 0 \space when \space w_j<0 \\
w_j &= \frac{2\rho_j+\lambda}{2z_j} \space besides,\rho<-\frac{\lambda}{2}
\end{align}$$


#### The Algorithm

repeat until converage{

for every feature
$$w_j=\begin{cases}
w_j = \frac{2\rho_j-\lambda}{2z_j} & when\space \rho>\frac{\lambda}{2} \\
w_j=0 & when \space \rho_j \in [-\frac{\lambda}{2},\frac{\lambda}{2}] \\
w_j = \frac{2\rho_j+\lambda}{2z_j} &when \space \rho<-\frac{\lambda}{2}
\end{cases}$$
}

### Summary

Lasso regularization are usually used for feature selection.