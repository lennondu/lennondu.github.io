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

$$w_k=w_k-\alpha\times Grad(w_k) \space k\in (1,2,\ldots,p+1)$$
    
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

#### Code Example

Let's make some easy linear regression like $y = w_0+w_1x$.
{% highlight python linenos%}
    import numpy as np
    from matplotlib import pyplot as plt
    from __future__ import division
    from sklearn import linear_model
    
    # create x
    np.random.seed(10)
    x = np.random.choice(np.arange(100),50)
    x.shape = (x.shape[0],1) # as numpy doesn't explictly define a column vector, you'd better define by yourself.
    # add some gaussian noise
    noise = np.random.normal(0,1,x.shape[0]).reshape(x.shape[0],1)
    # y = 5+4*x
    y = 5+4*x
    y.shape = (y.shape[0],1)
    plt.plot(x,y)
    plt.show()
    ones = np.ones([x.shape[0],1])
    x = np.concatenate((ones,x),axis=1)
    
    # gradient method
    def gradient(X,y,w):
        return -X.T.dot(y-X.dot(w))/X.shape[0]

    def error(X,y,w):
        return (y-X.dot(w)).T.dot(y-X.dot(w))/(2*X.shape[0])
    
    def linear_regression(X,y,alpha=0.001,maxiter = 100):
        init_w = np.random.normal(0,1,X.shape[1])
        w = init_w
        w.shape = (w.shape[0],1)
        iter_num = 0
        errors = [error(X,y,w)]
        while iter_num <= maxiter :
            grad = gradient(X,y,w)
            grad.shape = (grad.shape[0],1)
            w -= alpha * grad
            errors.append(error(X,y,w))
            iter_num+=1
            print iter_num,errors[iter_num]
        return w,errors
    
    # analytic solution
    def analytic_solution(X,y):
        return np.linalg.inv(x.T.dot(x)).dot(x.T.dot(y))
    
    w_gd,errors = linear_regression(x,y,alpha = 0.0001,maxiter = 200)
    #w_gd = [2.037,4.045]
    w_as = analytic_solution(x,y)
    #w_as = [5,4]
    plt.plot(x[:,1],y,label = 'Original')
    plt.plot(x[:,1],x.dot(w_gd),label = "Grad")
    plt.plot(x[:,1],x.dot(w_as), label = "Analytic")
    plt.legend()
    plt.show()
{% endhighlight %}
