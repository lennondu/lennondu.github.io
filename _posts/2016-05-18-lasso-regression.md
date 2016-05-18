# Lasso Regression

$$obj: Error = \sum_{i=1}^{n}(y_i-w^T \cdot x_i)^2+\lambda \|\|w\|\|_1$$

Also, $Error = (y-X^T\cdot w)^T\cdot(y-X^T\cdot w)+\lambda \|\|w\|\|_1$

Due to the Lasso regularization, we can't get the gradient of the object function. Thus, we will use [**coordinate descent**](https://en.wikipedia.org/wiki/Coordinate_descent) instend of gradient descent.

### Solver: Coordinate Descent

We can't get the gradient of $\|x\|$ when $x=0$. Then we will use [subgradient](https://en.wikipedia.org/wiki/Subderivative) when $x=0$.

$$\frac{\partial{E}}{\partial{w_j}} = $$