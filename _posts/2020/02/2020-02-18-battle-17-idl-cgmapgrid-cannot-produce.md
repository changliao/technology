---
layout: post
title: 'Battle 17: IDL cgmap_grid cannot produce label'
date: '2020-02-18T09:38:00.002-08:00'
author: Chang Liao
tags:
- IDLCoyote
- IDL
modified_time: '2020-02-18T09:38:48.035-08:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-1986077021173969906
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/02/battle-17-idl-cgmapgrid-cannot-produce.html
---

There is a limit the increment of this function that it may take a long time 
to generate the label. 


The function use global latitude and longitude to setup: 
;n_lats = 1 + fix((latmax-lat0)/float(latdelta)) chang 
 n_lats = 1 + long((latmax-lat0)/float(latdelta)) 


Later on, when the script draw all the label, the loop is like this: 

FOR i=0,n_lats-1 DO BEGIN
So, a small increment will lead to long run time. 