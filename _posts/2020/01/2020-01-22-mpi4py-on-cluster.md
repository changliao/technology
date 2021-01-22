---
layout: post
title: 'Mpi4py on cluster'
permalink: /posts/2020/01/22/mpi4py-on-hpc/
date: '2020-01-22'
author: Chang Liao
tags:
- mpi4py
- Python
- HPC
- MPI
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
* pip install mpi4py,  you should not use conda-forge channel because it will install mpi again.
* test with python -c "import mpi4py"

So earlier I had issues and there are several lessons:
You should load before installing mpi4py
Because we need to use system mpi, we need to load mpi after activate the environment.

Good luck!