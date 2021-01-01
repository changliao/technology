---
layout: post
title: 'Battle 30: Naming system'
date: '2020-06-30T12:28:00.001-07:00'
author: Chang Liao
tags:
- ELM
modified_time: '2020-06-30T12:28:18.776-07:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-3259267161008689176
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/06/battle-30-naming-system.html
---

A typicl ELM history file variable has the following structure:

if (use_cn) then
    this%qflx_evap_tot(begp:endp) = spval
     call hist_addfld1d (fname='QFLX_EVAP_TOT', units='mm H2O/s', &
        avgflag='A', long_name='qflx_evap_soi + qflx_evap_can + qflx_tran_veg', &
        ptr_patch=this%qflx_evap_tot, default='inactive', c2l_scale_type='urbanf')
end if

The question is: for a single variable, how do we control it in the post-process?

A Netcdf file only have a unique field name, so it is natural to use the field name for post-process.