---
layout: post
title: 'Battle 28: redesign the plot libary'
date: '2020-06-13T14:56:00.001-07:00'
author: Chang Liao
tags:
- Python
- Software
- Matplotlib
modified_time: '2020-06-13T14:56:39.059-07:00'

---


I have developed a Python library for various projects. This library has many different features including the plotting functions. But I am not satisfied with the current strategy/structure of some components. For example, I somehow wrote a list of functions for a similar purpose.
Now it is time to re-organize some functions.


![Figure 1](https://github.com/changliao/changliao.github.io/blob/main/_figures/python/pyes_plot.png?raw=true)

So there are several principles I will consider in the redesign:
I will not specify the temporal resolution, and it can be daily, monthly, or even hourly. This will be completely decided by the input datatime information. But user can specify the format using an optional argument;
There is no need to separate single and multiple data plot.
The zoom feature can be an individual function for now. Later on we can merge it at an optional feature.
3D plot needs additional simplification.