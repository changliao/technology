---
layout: post
title: 'Rename an E3SM case'
permalink: /posts/2022/10/12/rename_e3sm_case/
date: '2022-10-12'
author: Chang Liao
tags:
- e3sm
- Python
- cime
---

Renaming an E3SM case is desired when you want to retain the name for a rerun.

In general, there are two approaches to achieve this:

* Rename all the folders/subfolders, and then rename the files within these folders
* Create new folders/subfolders, and then move existing files into the newly created folders



There are different pros and cons in them

The first method:
Pros:

1. does not create new directories
2. keep all the existing file even we don't rename them

Cons:

1. Must rename folders first, when we can rename files in the right order

The second method:
Pros:

1. working on separated folders will avoid conflict
2. 

Cons:

1. moving file may cause performance slow down
2. may miss some files 

In pye3sm, I plan to implement the first method because it will keep all the files.

