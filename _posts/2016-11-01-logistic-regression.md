---
layout: post
title: Logistic Regression
category: Machine Learning Algorithm
permalink: ml/logistic_regression/
---


## Logistic Regression

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

## Logistic Regression

$$ f(x) = P(y^{(i)}  | x^{(i)}) = \frac{1}{1+e^{-w^T x^{(i)}}} $$

$$ obj:Max \space Expectation = \prod_{i=1}^{n}P(y^{(i)} | x^{(i)})^{y^{(i)}}(1-P(y^{(i)}  | x^{(i)}))^{1-y^{(i)}} $$

the same as 

$$ obj:Min \space -Expectation = -\prod_{i=1}^{n}P(y^{(i)} | x^{(i)})^{y^{(i)}}(1-P(y^{(i)}  | x^{(i)}))^{1-y^{(i)}} $$

so that we can still use gradient descent, but we need do some transformation.

First, we do log on both sides.

$$
\begin{align}
 log \space -Expectation &= -log \prod_{i=1}^{n}P(y^{(i)} | x^{(i)})^{y^{(i)}}(1-P(y^{(i)}  | x^{(i)}))^{1-y^{(i)}} \\
 Obj &= -\sum_{i=1}^{n}{(y^{(i)}log(P(y^{(i)} | x^{(i)})) + (1-y^{(i)})log((1-P(y^{(i)} | x^{(i)}))) } \\
 & \stackrel{ set \space P(y^{(i)} | x^{(i)}) = p}=-\sum_{i=1}^{n}y^{(i)}(log(p)-log(1-p))-\sum_{i=1}^{n}log(1-p) \\
 &= -\sum_{i=1}^{n}y^{(i)}log\frac{p}{1-p}-\sum_{i=1}^{n}log(1-p) \\
 &= -\sum_{i=1}^{n}y^{(i)}w^Tx^{(i)}+\sum_{i=1}^{n}log(1+e^{w^Tx^{(i)}})
\end{align} 
 $$
 
Let's get the gradient of the object.

$$
\begin{align}
\frac{\partial{obj}}{\partial{w_j}} &= \sum_{i=1}^{n}\frac{1}{1+e^{w^Tx^{(i)}}}e^{w^Tx^{(i)}}x^{(i)}_j-\sum_{i=1}^{n}y^{(i)}x^{(i)}{j} \\
&= \sum_{i=1}^{n}px_j^{(i)}-\sum_{i=1}^{n}y^{(i)}x^{(i)}_j \\
&= \sum_{i=1}^{n}(p-y^{(i)})x^{(i)}_j
\end{align}
$$

However, equation 8 doesn't have closed-form solution.
