---
layout: post
title: 'Battle 31: A flexible model configuration system'
date: '2020-07-03T22:37:00.000-07:00'
author: Chang Liao
tags:
modified_time: '2020-07-03T22:37:07.574-07:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-6338002019791293945
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/07/battle-31-flexible-model-configuration.html
---
CIME is a rather flexible case management system.
When we design a system configuration subsystem, we want it to be flexible so we can set up a system without providing all the information.
To do so, the case system should use a default configuration if possible.