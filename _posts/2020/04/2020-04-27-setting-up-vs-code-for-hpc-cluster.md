---
layout: post
title: 'Battle 23: VS Code for HPC cluster'
date: '2020-04-27T16:10:00.004-07:00'
author: Chang Liao
tags:
- VNC
- x11
- MayaVI
- Python
- VTK
- HPC
- VSCode
- Matplotlib
modified_time: '2020-05-01T11:32:02.234-07:00'
thumbnail: https://1.bp.blogspot.com/-l2Ld1AVdnVs/Xqdk2u1cYwI/AAAAAAAA9P8/v2q3NNnIm9ohcJnQPiko0kC-s7UOXuulwCLcBGAsYHQ/s72-c/vnc_maya.png
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-378367479968322478
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/04/setting-up-vs-code-for-hpc-cluster.html
---

VVS Code has become my go-to code editor since its release. Here I want to share some tips how I used it for HPC development.

Remote development with SSH.

This is a very nice feature if you want to write code directly on HPC cluster. There are many advantages:

Code is always backup because that is how HPC home directory is used for;
No need to transfer data between local and HPC scratch space;
Speed is fast. If you have experienced the X-window age, you should know most applications that use x11 are extremely slow. But VS Code with SSH is as fast as working locally.

For some languages, such as Python, we can debug directly remotely.


What's more, I found a way to enable graphics through x11, which was discussed by many users such as this one: https://discourse.julialang.org/t/plotting-while-working-with-vs-code-remote-ssh/34309


Later on, I was not satisfied with Matplotlib, and I started to use MayaVI PyVista, which used VTK. So we need a better way to enable graphic drivers on HPC.


It appears we cannot rely on SSH anymore, Instead, a VNC is a much better solution. 


![Figure 1](https://github.com/changliao/technology/blob/main/_figures/python/vnc_maya.png?raw=true)


![Figure 2](https://github.com/changliao/technology/blob/main/_figures/python/spyvista.png?raw=true)



Now we are ready for some advanced Python graphics more than just Matplotlib. 

We can basically have an interactive IDE without Jupyter Notebook, which I never used.