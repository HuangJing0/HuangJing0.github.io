---
layout:     post
title:      C Program - MAC命令行gcc编译失败
subtitle:   _stdio.h No such file or directory
date:       2020-03-31
author:     Jing
header-img: img/post-bg-ProC.png
catalog: true
export_on_save:
html: true
tags:
    - C
---


嫌弃Xcode的代码高亮，卸载XCode转投vscode的怀抱之后，gcc 编译文件时报错：


	fatal error: _stdio.h: No such file or directory
	#include <_stdio.h>



原因：gcc 编译时找不到C的运行库，默认的目录/usr/include不存在；

解决：cmd+空格搜索到该头文件路径后，用环境变量导出头文件目录和库目录,添加到文件 ./.bash_profile 中：

```
export C_INCLUDE_PATH=/Library/Developer/CommandLineTools/SDKs/MacOSX10.15.sdk/usr/include
```

```
export LIBRARY_PATH=/Library/Developer/CommandLineTools/SDKs/MacOSX10.15.sdk/usr/lib
```
