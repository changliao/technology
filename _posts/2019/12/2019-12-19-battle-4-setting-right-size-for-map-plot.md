---
layout: post
title: 'Battle 4: setting the right size for map plot '
date: '2019-12-19T11:49:00.000-08:00'
author: Chang Liao
tags:
- Mapping
- IDL
- Plotting
modified_time: '2019-12-19T13:42:07.368-08:00'
thumbnail: https://1.bp.blogspot.com/-ENVgaC09eP0/XefyGjQPPjI/AAAAAAAA5wE/9ld635BzLcg0GCTXpoIMZy_uARNNkDnpACLcBGAsYHQ/s72-c/dem.jpg
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-5806970622190074727
blogger_orig_url: https://codedoesnotlie.blogspot.com/2019/12/battle-4-setting-right-size-for-map-plot.html
---

How to control the size of text so they look pleasantly for readers?

Here is a solution for map object:

charsize = cgdefcharsize()

main title: charsize  * 1.0
cgmap_grid: charsize  * 0.7
longitude: charsize  * 0.6
latitude: charsize  * 0.6
colorbar title: charsize  * 0.7
colorbar label: charsize  * 0.8

To illustrate:



![Figure 2](https://github.com/changliao/technology/blob/main/_figure/idl/dem.png?raw=true)


Later I will provide other examples for other type of plots. 