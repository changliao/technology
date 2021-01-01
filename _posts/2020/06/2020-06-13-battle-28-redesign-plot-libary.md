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
thumbnail: https://1.bp.blogspot.com/-WXogke5-J3k/XuQGJox3-eI/AAAAAAAADYA/Ln1EJIaMLOQ5jH6EQKF9XRhXDbgZt8vmACK4BGAsYHg/s72-c/tsplot.png
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-6423765435967231520
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/06/battle-28-redesign-plot-libary.html
---


I have developed a Python library for various projects. This library has many different features including the plotting functions. But I am not satisfied with the current strategy/structure of some components. For example, I somehow wrote a list of functions for a similar purpose.
Now it is time to re-organize some functions.


![Figure 1](https://github.com/changliao/changliao.github.io/blob/main/_figure/pyes_plot.png?raw=true)

So there are several principles I will consider in the redesign:
I will not specify the temporal resolution, and it can be daily, monthly, or even hourly. This will be completely decided by the input datatime information. But user can specify the format using an optional argument;
There is no need to separate single and multiple data plot.
The zoom feature can be an individual function for now. Later on we can merge it at an optional feature.
3D plot needs additional simplification.