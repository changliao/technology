---
layout: post
title: 'Battle 12: MPI QA'
date: '2020-02-04T10:26:00.000-08:00'
author: Chang Liao
tags:
modified_time: '2020-02-04T10:26:28.568-08:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-9139494811394679418
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/02/battle-12-mpi-qa.html
---

I don't alway have to deal with MPI myself, but I recently used it for several 
projects. 
I have several questions to share:

* Does master (rank=0) always the last to finish? 
* Should code wait for all slaves to actually receive the broadcast message? 