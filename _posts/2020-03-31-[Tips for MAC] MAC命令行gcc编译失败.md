---
layout:     post
title:      Tips - MAC命令行gcc编译失败
subtitle:   fatal error: _stdio.h: No such file or directory
date:       2020-03-31
author:     Jing
header-img: img/post-bg-tips.jpg
catalog: true
export_on_save:
html: true
tags:
    - C
---
gcc 编译文件时报错：

```PowerShell
/opt/local/lib/gcc8/gcc/x86_64-apple-darwin18/8.3.0/include-fixed/stdio.h:78:10: fatal error: _stdio.h: No such file or directory
 #include <_stdio.h>
          ^~~~~~~~~~
 ```


gcc 编译时默认读取'/usr/include'	但该文件夹不存在：

```
export C_INCLUDE_PATH=/Library/Developer/CommandLineTools/SDKs/MacOSX10.15.sdk/usr/include
```

```
export LIBRARY_PATH=/Library/Developer/CommandLineTools/SDKs/MacOSX10.15.sdk/usr/lib
```
