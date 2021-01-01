---
layout: post
title: 'Battle 3: IDL cgmap grid frame'
date: '2019-11-17T22:35:00.001-08:00'
author: Chang Liao
tags:
- QGIS
- IDLCoyote
- IDL
- Python
- GIS
- ArcGIS
modified_time: '2019-11-17T22:36:19.506-08:00'
thumbnail: https://1.bp.blogspot.com/-2pxooJ55bRc/XdI7ifW1vEI/AAAAAAAA5hA/gkwWF7YR8McYkdojD_mBewbynVwyl8MwwCLcBGAsYHQ/s72-c/dem.jpg
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-5621882378293482355
blogger_orig_url: https://codedoesnotlie.blogspot.com/2019/11/battle-3-idl-cgmap-grid-frame.html
---

IDL is so far my go-to programming language in terms of map visualization.

Recently, I picked up an old function I wrote years ago to use it in my current projects, but there was some issue with the cgmap_grid map input:


map = OBJ_NEW('cgMap', 'UTM', ELLIPSOID = 'GRS 1980', Zone = 6, $
     Position = position_map, XRANGE = XRANGE, yrange = yrange)


Basically, when I first developed this function, I didn't use a generalized map structure.
So the question how should I define a map structure for any raster file.

I found a solution fast: cggeomap
pMapCoord = cgGeoMap(sFilename_geotiff,$

    geotiff = pGeotag)

The source code is pretty simple and easy. However, it missed the position and ranges. So I tried to add them back and tested it.
I noticed that the grid does not has labels! Initially I thought maybe the increment is too large, so I set it to 0.01. It gave an error.

At this point, as a developer, I started to debug. I followed the function inside and checked the boundary. What surprised me was that the range is -180 to 180! But my data is only a small watershed!

cgGeoMap 
offers a keyword to display the data directly, so I gave a try. It works fine with the label. So what is the problem?

I noticed the map structure changed within cgmap_grid, but I am not sure how. I was convinced that the boundary was wrong.

At last, I suddenly realized that why don't I check the original code as I have modified a lot. I followed inside again and the boundary was -180 to 180!
So it was not about the boundary.

I got back to the cgGeoMap, and tested a few more increment and it worked.
So what is needed is:

pMapCoord -> SetProperty, Position=position_map
Below is the result converted from eps:

![Figure 1](https://github.com/changliao/changliao.github.io/blob/main/_figure/dem_grid.png?raw=true)


Why I bother to use IDL instead of other tools like Python, ArcMap?
First, I don't have access to Windows often, and working with GUI is always a pain.
Second, Python does not have good package to support all map projection labels.