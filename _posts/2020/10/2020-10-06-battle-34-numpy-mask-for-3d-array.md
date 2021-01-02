---
layout: post
title: 'Numpy mask for 3D array '
date: '2020-10-06T16:56:00.006-07:00'
author: Chang Liao
tags:
- Python
- Numpy
modified_time: '2020-10-06T21:42:03.597-07:00'
---

How to use np.where and mask on a 3D array?
If I use normal operation, I received an error like this:


![Figure 1](https://github.com/changliao/technology/blob/main/_figure/python/numpy3d.png?raw=true)


An easy way to fix this is to operate slice by slice:

pShape = sandpct.shapea
Data_out= np.full(pShape, 0, dtype=float)
for i in np.arange(0, pShape[0], 1):
    aData_out[i][aMask==1] += 5

aData_out[aData_out>100] = 100
pDatasets_in.close()