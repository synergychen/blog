---
layout: post
title: Run MATLAB Without GUI
date: 2014-02-04 15:48:16
categories: Matlab
---

> MATLAB is strong and fast for calculations, but slow when loading.

Truth is that we could run MATLAB files without open GUI. Here, we try to run `test.m` for example.

Only one command is needed here.

### Syntax/Usage

```matlab
/matlab [-nodesktop | -nojvm | -nosplash] [-r MATLAB_command]
```

### Commonly Used Values of Syntax

| Values | Descriptions |
| ------ | ------------ |
| -nodesktop | do not start matlab desktop |
| -nojvm | shut off java virtual machine. If figure plot is needed in your file, then do not use this value. |
| -nosplash | do not start splash screen during startup |
| -r | start MATLAB and execute MATLAB command or file |

Here in order to to run `test.m` file, we could do the following. Notice that we use `-r test` instead of `test.m`.

```matlab
#   if test.m contains only numerical calculation, then do (with -nojvm)
/Applications/MATLAB_R2012b.app/bin/matlab -nodesktop -nojvm -nosplash -r test
#   if test.m contains figures plotting, then do, then do (without -nojvm)
/Applications/MATLAB_R2012b.app/bin/matlab -nodesktop -nosplash -r test
```
