---
layout: post
title: 'Debug Python Without Debugger'
permalink: /posts/2023/02/14/debug_python_without_debugger/
date: '2023-02-14'
author: Chang Liao
tags:
- e3sm
- Python
- cime
---

During my work which attempts to add a new compset to the E3SM model, I got an error from the `create_case` script. However, the error does not provide much useful information as:

        Traceback (most recent call last):
          File "./create_newcase", line 18, in <module>
            _main_func()
          File "/qfs/people/liao313/workspace/fortran/e3sm/E3SM/cime/CIME/scripts/create_newcase.py", line 449, in _main_func
            ngpus_per_node=ngpus_per_node,
          File "/qfs/people/liao313/workspace/fortran/e3sm/E3SM/cime/CIME/case/case.py", line 2379, in create
            ngpus_per_node=ngpus_per_node,
          File "/qfs/people/liao313/workspace/fortran/e3sm/E3SM/cime/CIME/case/case.py", line 1300, in configure
            self._get_component_config_data(files)
          File "/qfs/people/liao313/workspace/fortran/e3sm/E3SM/cime/CIME/case/case.py", line 1104, in _get_component_config_data
            env_file.add_elements_by_group(compobj, attributes=attlist)
          File "/qfs/people/liao313/workspace/fortran/e3sm/E3SM/cime/CIME/XML/entry_id.py", line 460, in add_elements_by_group
            value = srcobj.get_default_value(src_node, attributes)
          File "/qfs/people/liao313/workspace/fortran/e3sm/E3SM/cime/CIME/XML/entry_id.py", line 22, in get_default_value
            value = self._get_value_match(node, attributes)
          File "/qfs/people/liao313/workspace/fortran/e3sm/E3SM/cime/CIME/XML/component.py", line 85, in _get_value_match
            if re.search(value, attributes[key]):
          File "/usr/lib64/python3.6/re.py", line 182, in search
            return _compile(pattern, flags).search(string)
          File "/usr/lib64/python3.6/re.py", line 301, in _compile
            p = sre_compile.compile(pattern, flags)
          File "/usr/lib64/python3.6/sre_compile.py", line 562, in compile
            p = sre_parse.parse(p, flags)
          File "/usr/lib64/python3.6/sre_parse.py", line 855, in parse
            p = _parse_sub(source, pattern, flags & SRE_FLAG_VERBOSE, 0)
          File "/usr/lib64/python3.6/sre_parse.py", line 416, in _parse_sub
            not nested and not items))
          File "/usr/lib64/python3.6/sre_parse.py", line 616, in _parse
            source.tell() - here + len(this))
        sre_constants.error: nothing to repeat at position 0


The `component.py` script at line 85 looks like this:

        if attributes is not None and key in attributes:                                       
            if re.search(value, attributes[key]):                
                logger.debug(
                    "Value {} and key {} match with value {}".format(
                        value, key, attributes[key]
                    )
                )
                match_count += 1
            else:                            
                match_count = 0
                break

The first glimpse shows that the `re.search(value, attributes[key])` contains an issue, but what exactly is the problem is unclear. 

I used to debug `CIME` within a Python IDE, but it is a painful process to setup because of the command line arguments. So I decided to use the classical `print` method. Besides, because the tool throw an exception during the execuation, I decided to use a simple `try catch` block to identify the issue.

        if attributes is not None and key in attributes:
            try:                                       
                if re.search(value, attributes[key]):                    
                    logger.debug(
                        "Value {} and key {} match with value {}".format(
                            value, key, attributes[key]
                        )
                    )
                    match_count += 1
                else:                            
                    match_count = 0
                    break
            exception:
                print('incorrect: ',value, attributes[key])

With some simple modification to the `component.py`, I got the output that I needed:

        incorrect:  *DROF%MOSART* 2000_DATM%QIA_ELM%SP_SICE_SOCN_DROF%MOSART_SGLC_SWAV_SIAC_SESP

So the error is basically caused by a regular expression search pattern issue. After removing the `*` in the pattern, the error went away.

