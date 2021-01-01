---
layout: post
title: 'Battle 14: IDL cgplots over cgimage'
date: '2020-02-15T15:27:00.001-08:00'
author: Chang Liao
tags:
- IDLCoyote
- IDL
modified_time: '2020-02-15T16:41:22.433-08:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-7254499808333688961
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/02/battle-14-idl-cgplots-over-cgimage.html
---

How can I draw a circle on top of a cgimage in IDL? 
This question is similar to this question: 

[https://comp.lang.idl-pvwave.narkive.com/alL9vVeZ/plotting-a-horizontal-line-over-a-cgimage](https://comp.lang.idl-pvwave.narkive.com/alL9vVeZ/plotting-a-horizontal-line-over-a-cgimage) 

Generally, the cgimage coordinate system is not the same with device, so a 
conversion is needed to do so: 

 cgImage, googleImage[0:2,*,*], Position = position, /noerase, $ 
      /Keep_Aspect, OPOS=outputPosition 
 print,outputPosition 
 dummy_x = 0.5 * (outputPosition[0] + outputPosition[2]) 
 dummy_y = 0.5 * (outputPosition[1] + outputPosition[3]) 
 cgPlotS, dummy_x, dummy_y, PSYM='filledstar', SYMSIZE=3.0, 
COLOR='red',/normal 

Fixed. 