---
layout: post
title: 'Battle 6: define a DOI for each model simulation'
date: '2019-12-19T13:40:00.001-08:00'
author: Chang Liao
tags:
- DOI
- case system
modified_time: '2019-12-19T14:01:40.114-08:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-6986081028096238617
blogger_orig_url: https://codedoesnotlie.blogspot.com/2019/12/battle-6-define-doi-for-each-model.html
---

Simulation management can be tough if you run hundreds of simulation.
The question is: how should we keep track of simulations within code?

In many Earth system model, a simulation is a case. Each case has different setup, or configuration.
A case name is usually used to identify the case. Similarly, each publication has a unique DOI (https://en.wikipedia.org/wiki/Digital_object_identifier). But this DOI is not simply a random name. For example, one of my recent publications has a DOI as: https://doi.org/10.1029/2019MS001792
Let's focus on the last string name "2019MS001792". It clearly contains the time information 2019. And it also has some index information.

So how should we define our case names? There are several factor we might consider:
Time, it matters when the case was created.
Model used.
Index.
Model parameters are generally complex to be included.
I plan to setup a simple template to mange all model simulation using the above method. For example, a "swat20191218001" case name can be used to represent a swat model case created on 20191218 with an index of 001.

When there is a calibration task, it is easier to define the cases using continuous indices while keeping the time the same (It is possible to create cases at different time). 