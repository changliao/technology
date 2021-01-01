---
layout: post
title: 'Battle 15: IDL batch extraction '
date: '2020-02-17T14:08:00.001-08:00'
author: Chang Liao
tags:
- ENVI
- IDL
modified_time: '2020-02-17T22:29:54.043-08:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-8553193769215053122
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/02/battle-15-idl-batch-extraction.html
---

I was using my own library to extract geotiff with shapefile, then the program 
stops after day 9. 

I restarted from day 9, it continues to run another 9 day. 

Initially I thought I didn’t release the file handle and reached the limit. 
It was not because I destroyed everything at each loop. 

Finally I realized that I changed the structure of the batch mode. 
So I moved batch command outside and everything work again! 