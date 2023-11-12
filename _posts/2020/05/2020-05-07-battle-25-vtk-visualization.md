---
layout: post
title: 'Battle 25: VTK visualization'
date: '2020-05-07T09:34:00.001-07:00'
author: Chang Liao
tags:
- E3SM
- VTK
- Visualization
- 3D
modified_time: '2020-05-07T10:08:26.519-07:00'
thumbnail: https://1.bp.blogspot.com/-QgAynVphoAQ/XrRAa8OtU-I/AAAAAAAA9dc/4PJQeAQNbV8HQjt6IXEidEVYG1nRsAYSwCK4BGAsYHg/s72-c/row-major-3D.png
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-7404369665452647672
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/05/battle-25-vtk-visualization.html
---

n my recent posts, I discussed how to generate 3D plots using MayaVi and PyVista, both of them works but not as great as I expected.
MayaVi has issue with rendering using OpenCL
PyVista does not expose enough APIs to control the plot
So these are great tools to start with, but later on I decided to switch back to raw VTK.
I used another package called PyeVTK (https://github.com/paulo-herrera/PyEVTK), it basically help you to export data into the VTK format.

As we know, VTK supports the legacy (text-based) and new (xml-based) format.
In earlier days, I already developed two models to export data to the legacy format. 
One of them is in my Git: https://github.com/changliao1025/modelview

This time I decided to use the package which uses XML.
It is straightforward to follow the example. You need to be careful with the data section still because of the memory alignment with 3D datasets.



![Figure 1](https://github.com/changliao/technology/blob/main/_figures/programming/row_major_3D.png?raw=true)

After that, I was able to produce some results:



![Figure 1](https://github.com/changliao/technology/blob/main/_figures/vtk/artifact.png?raw=true)


However, there is some issue with Visit or ParaView, if the mesh cell are too close, there might be an artifact with the rendering. So I increased the distance slightly and the new results look great.



![Figure 1](https://github.com/changliao/technology/blob/main/_figures/vtk/wtd_vtk.png?raw=true)


With that, the python package I developed for E3SM can fully support VTK now.