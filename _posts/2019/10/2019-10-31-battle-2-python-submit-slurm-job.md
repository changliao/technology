---
layout: post
title: 'Battle 2: Python submit SLURM job'
date: '2019-10-31T11:15:00.001-07:00'
author: Chang Liao
tags:
- Bash
- Shell
- E3SM
- Python
- HPC
- VSCode
modified_time: '2019-10-31T12:59:27.337-07:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-7140057019162684391
blogger_orig_url: https://codedoesnotlie.blogspot.com/2019/10/battle-2-python-submit-slurm-job.html
---

Programmers are supposed to be lazy, like Emacs user wants to do everything within Emacs because it can be an operating system.

While I prefer to do everything within VS Code/Python because it can almost do everything I need for my programming tasks.

Recently I wrote a small Python package to deal with E3SM simulation system. I am happy with most part of the scripts, especially I have recently updated the structure of the cross-platform global variables (https://www.changliao.us/2019/10/develop-python-scripts-cross-platform.html).

But I also encountered some issue with the job submission step. Basically, the job submission step does not load the desired environmental variable, which I placed in the .bash_profile.

It is actually more complex than that because my workflow is a little bit of long:

I use Visual Studio Code to edit Python code directly using Remote Development (https://code.visualstudio.com/docs/remote/remote-overview)
The command (case.submit) (https://github.com/ESMCI/cime) which I intend to run seems to require some environment settings (ulimit -s unlimited, etc.)
So in order to run this command, I have several options: 
I can use os.system (https://docs.python.org/3/library/os.html#os.system)
I can use subprocess (https://docs.python.org/3/library/subprocess.html)

With the latter one is preferred, I can use subprocess.call(), subprocess.run(), or subprocess.popen() to do this.

The job crashed within a few second because of memory issue, which is again because the .bash_profile was not loaded.

The reason is that by default, the subprocess will generate a non-login, non-interactive shell to run the command. And this shell will not load the .bash_profile because ".bash_profile is executed for login shells, while .bashrc is executed for interactive non-login shells." (Link)

This is also similar to this question. The solution is also presented in the question. So I edited the .bashrc file to include the environmental variables. Then I can call the command using either:
p = subprocess.Popen(sCommand, shell= True, executable='/bin/interactive_bash' ), or
p = subprocess.Popen(['/bin/bash', '-i', '-c', sCommand])
Basically the above method created an interactive non-login shell so it will load the .bashrc file.

Problem solved.

Bouns: 
If you want to access terminal with .bash_profile loaded directly within VS Code, you can try this:
You can pass arguments to the shell when it is launched.
For example, to enable running bash as a login shell (which runs .bash_profile), pass in the -l argument (with double quotes):
Good luck!