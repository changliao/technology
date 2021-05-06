---
layout: post
title: 'Object-oriented programming based flowline simplification '
permalink: /posts/2021/05/06/flowline-oop/
date: '2021-05-06'
author: Chang Liao
tags:
- Hydrology
- Flowline
- OOP
---

Recently, I have developed a set of modules within the HexWatershed python package.
These functions take a flowline vector file and process it so it can be used for the HexWatershed model.

In short, these functions resolve issues:
* disconnected line
* (nested) loop caused by lake, braided river
* reversed flow direction flowline

Besides, it re-constructs the stream index and order.

However, I haven't implemented them using the OOP approach. 
In this post, I will discuss what can be done to improve them.

Similar to HexWatershed C++ API, we could define vertex, edge, and cell to organize flowline. For example, a single LineString can be represented by a list of vertices. A cell can be represented by a list of close vertices or edges.

While this OOP approach can help with some processes, the benefits are not universal.

1. File format conversion will unlikely benefit from this
2. MultiLineString split into LineString will unlikely benefit from this as well
3. Connect disconnected line can use the vertex distance to find gap;
4. Find all vertices can use the flowline list;
5. Advanced split can use both flowline and vertex list;
6. Correct flow direction can use flowline list
7. Remove loop can use flowline topology
8. Merge can use edge info
9. Remove small river can use flowline/edge info

Overall, it is likely OOP will help with more complicated tasks.
