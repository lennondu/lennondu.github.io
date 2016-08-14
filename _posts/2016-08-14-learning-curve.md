---
layout: post
title: Learning Curve
category: Machine Learning Algorithm
permalink: ml/learning_curve
---
# Learning Curve

Learning curve in machince learning is a representation of errors vs. size of data.

## Errors vs. Size of Data

Usually we plot $Error_{train}$ and $Error_{cross\_validation}$.

The normal one is like this.
<img src='http://7xqtok.com1.z0.glb.clouddn.com/normal.png'>

High bias one is like this. As you can see, train error is relatively high. The cross validation error has stopped to decrease even the size of data increase. It seems that more data doesn't help to improve the result. 
<img src='http://7xqtok.com1.z0.glb.clouddn.com/high_bias.png'>

High variance one is like this. It's obvious that there is a gap between train error and cross validation error. Besides, it seems that if we get more data, the cross validation will go down.
<img src='http://7xqtok.com1.z0.glb.clouddn.com/high_variance.png'>
