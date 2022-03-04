---
layout: post
title: 'Python module in VS code issue'
permalink: /posts/2022/03/04/python-module-vscode/
date: '2022-03-04'
author: Chang Liao
tags:
- VSCode
- Python
- GDAL
---

One of the issues I recently had is the import module error when testing the swaty python package.

Basically, it is impossible to import a module in a different folder if that folder is not in the PATH or PYTHONPATH.

Surprisingly, I am working on a different project and this is not an issue. So what is problem?

In general, I will avoid adding a python package that is under active development into the system wide environment variables such as the PATH or PYTHONPATH through .bash_profile or .bashrc. So how can you call another python package if it is not installed by pip or conda? Normally there are is another solution: you can temporally insert its path into the PATH so it won't affect system PATH.

The reason that I was able to do so without inserting is because there is a __pycache__ folder under the directory I was running the code. This folder is often generated during the installation process, possibly by the setup.py. This isn't surprising because I was releasing it to the pip and conda platforms. So even this package is NOT installed nor added to the path, the VSCode still thinks it is available for import.

Conclusion, for package development, to avoid inserting a package in many files, it is easier to add the package to the PYTHONPATH. However, whenever for package testing, it is preferred to use a different conda environment and install the package after removing it from the system path.


