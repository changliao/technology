---
layout: post
title: 'Battle 5: VS Code Python failed with OpenBLAS blas_thread_init: RLIMIT_NPROC'
date: '2019-12-19T11:49:00.001-08:00'
author: Chang Liao
tags:
- Python
- HPC
- VSCode
modified_time: '2020-01-17T10:23:40.261-08:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-281818065295560327
blogger_orig_url: https://codedoesnotlie.blogspot.com/2019/12/battle-5-vs-code-python-failed-with.html
---

When I was trying to debug a Python script on cluster, I received the 
following error: 
"OpenBLAS blas_thread_init: RLIMIT_NPROC" 

So I decided to check why there is OpenBLAS, and quick search leads to numpy, 
which is a package I used in my script. I quit the program and tried again, no 
luck. 

I typed "top" to find out what is the problem. It showed up that there are 
around 10 python processes are running but I am not using any at all. 

So I used the "-c" option to find the path of each process. It turned out that 
all the processes are from the VS Code server. 
It appears some VS Code failed, but the process remains active in the 
background, and I have never realized that they are there. 

Then the question is how to kill them. I used to use "ps" to find running 
process, but "top" and "ps" are different. 
I found a solution to: 

[https://www.booleanworld.com/kill-process-linux/](https://www.booleanworld.com/kill-process-linux/) 

"pkill -u *" 
"pkill -9 node" 

Problem solved. 