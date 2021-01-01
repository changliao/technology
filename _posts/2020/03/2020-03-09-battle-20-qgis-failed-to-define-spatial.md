---
layout: post
title: 'Battle 20: QGIS failed to define spatial reference'
date: '2020-03-09T10:46:00.002-07:00'
author: Chang Liao
tags:
- QGIS
- Python
- GDAL
modified_time: '2020-03-09T11:30:44.474-07:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-6929545925870082418
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/03/battle-20-qgis-failed-to-define-spatial.html
---

I need to convert a raster file to global scale. 
Earlier I manually resmapled it using Python SciPy, but the result is not very 
nice. 
Later on, I used the GDAL Python API, the results is great. 
However, when I tried to compared the two rasters, QGIS failed to define the 
projection. 

ArcGIS succeeded again. 