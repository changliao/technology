---
layout: post
title: 'Battle 11: Mpi4py on cluster'
date: '2020-01-22T17:57:00.000-08:00'
author: Chang Liao
tags:
- mpi4py
- Python
- HPC
- MPI
modified_time: '2020-04-03T09:22:36.299-07:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-3359843679142732252
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/01/battle-11-mpi4py-on-cluster.html
---

One of my Python scripts is taking too long to run, which exceeds the short queue.
I decided to use MPI, and mpi4py seems to be a good choice.
But there are many issue when I first used it.

After many attempts, I found at least one way to use it.

Some ideas are from here: https://researchcomputing.princeton.edu/mpi4py

* ssh into the cluster
* load anaconda into system
* create a conda environment for this task mpienv
* activate the environment
* load compiler, I used gcc
* load openmpi
* export MPICC="$(which mpicc)"
* pip install mpi4py,  you should not use conde-forge channel because it will install mpi again.
* test with python -c "import mpi4py"

So earlier I had issues and there are several lessons:
You should load before installing mpi4py
Because we need to use system mpi, we need to load mpi after activate the cnvironment.

Good luck!