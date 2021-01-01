---
layout: post
title: 'Battle 22: scatter plot with kde using matplotlib'
date: '2020-04-16T10:47:00.002-07:00'
author: Chang Liao
tags:
- Scatterplot
- Python
- KDE
- SNS
- Matplotlib
modified_time: '2020-04-16T10:47:59.467-07:00'
thumbnail: https://1.bp.blogspot.com/-WiPcJwr78Ww/XpiYIoQOpHI/AAAAAAAA8uo/5FhDkcjmWYcrGg9bCvQ1yUmOpKjwxh1QQCLcBGAsYHQ/s72-c/sur_slp-zwt_scatterplot.png
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-9002670781130601180
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/04/battle-22-scatter-plot-with-kde-using.html
---


How to produce a scatter alike plot using Matplotlib without using SNS or other packages?

![Figure 1](https://github.com/changliao/changliao.github.io/blob/main/_figure/sur_slp-zwt_scatterplot.png?raw=true)


Here are several issues we need to consider and corresponding solutions (later):
Setup the axes (there are 3 ax object here) positions;
Control the tick range and label;
Fix the overlap at intersection origin;
Choose a good color map for density plot;
Choose the counter alike density plot;
Setup KDE plot with shade;
Hide KDE plot tick label;
Set up KDE plot grid;
Set up KDE plot tick intervals;
Set up a vertical KDE plot;
Compatibility between density plot and KDE plot tick intervals.
This plot is inspired by sns.jointplot and python-graph-gallery.com.

Thank you.