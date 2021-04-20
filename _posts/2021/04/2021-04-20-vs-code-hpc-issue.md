---
layout: post
title: 'VS code on cluster issue'
permalink: /posts/2021/04/20/vs-code-hpc-issue/
date: '2021-04-20'
author: Chang Liao
tags:
- VSCode
- Python
- HPC
---

VS code extension sometimes crashes on HPC during remote development.

One quick fix is to remove the vs server folder. However, sometimes we ran into errors.

If you use top command, you will see "node" process running even after you exit VS code. This is an indicator something is wrong.

You can first kill all processes, or kill node manually.
After that, you can then remove the whole folder, reconnect, install all extension again.