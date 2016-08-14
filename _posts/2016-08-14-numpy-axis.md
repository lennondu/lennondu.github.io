---
layout: post
title: Numpy axis
category: python
permalink: python/numpy_axis
---

# Numpy axis

This article aims to illustrate the axis in numpy's function by some examples.

General Defination(numpy.sum as example):

axis : None or int or tuple of ints, optional

Axis or axes along which a sum is performed. The default, axis=None, will sum all of the elements of the input array.  If axis is negative it counts from the last to the first axis. If axis is a tuple of ints, a sum is performed on all of the axes specified in the tuple instead of a single axis or all the axes as before.

First, for 2-D array, axis=0 or -2 means vertical, axis=1 or -1 means horizontal. If we use tuple, it will sum all the axes.
{% highlight ruby %}
    data = np.array([
           [0,1,2],
           [3,4,5],
           [6,7,8]
           ])
    data.sum(axis=0)
    #array([ 9, 12, 15])
    data.sum(axis=1)
    #array([ 3, 12, 21])
    data.sum(axis=(0,1))
    #36
    data.sum(axis=(0,-1))
    #36
    data.sum(axis=(-2,1))
    #36
{%endhightlight%}
As for 3-D array, it is similar but more complex. Test it by yourself.




