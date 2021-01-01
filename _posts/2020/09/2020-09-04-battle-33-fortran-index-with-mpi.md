---
layout: post
title: 'Battle 33: Fortran index with MPI'
date: '2020-09-04T10:33:00.003-07:00'
author: Chang Liao
tags:
- Fortran
- E3SM
- H2SC
modified_time: '2020-09-04T10:51:59.275-07:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-5341192713433776863
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/09/battle-33-fortran-index-with-mpi.html
---

Recently I made some changes to H2SC model I developed. After the modification, the model crashed after some time step.

In the beginning, the E3SM log file only provides some information about the MPI and PIO error, which is not what I have modified. 

I knew there are some issues within the code, and there are several possibilities.

First, I tried to check all the history files and restart files.

Later on, I was reminded to test the default model, It turns out the default one is working fine. So it is not related to the environmental settings.

Following the rabbit hole, I was able to identify the subroutine where the issue comes from: 

call DrainageH2SC



So I need to check all the steps within this subroutine. I used the simple print/write statement to output some variables in various locations.

During this process, I was again to identify several errors in the code. For example, 

dArea = grc_pp%area(g) * 1000.0 * 1000.0 !unit is km, convert to m

The grc_pp module unit is not the same with most other modules, a conversion is needed here.

Later on, in the log file I noticed something suspicious:

severe (408): fort: (3): Subscript #2 of the array HKSAT has value 0 which is less than the lower bound of 1

e3sm.exe 0000000001E6F05C soilhydrologymod_ 2376

This error information was never caught in earlier debug.

aDummy = hksat(c, jwt(c):nlevbed)

What happened is that the jwt(c) can become 0, which is possible based on another statement:
! allow jwt to equal zero when zwt is in top layer

Basically when the water table is at land surface, the jwt is set to 0. 
Because Fortran index starts at 1, this becomes an issue, so we handle this by changing jwt to 1 in this case.

The challenging part in this debug is that the crash information does not reveal the index issue clearly when only some node/thread is experiencing this issue. So the actual error may be buried within the large log file.

Ideally, the crash log file should have this information at the very beginning but somehow I missed it maybe.

The model now runs successfully.