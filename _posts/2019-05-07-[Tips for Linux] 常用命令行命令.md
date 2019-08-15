---
layout:     post
title:      Tips - 常用命令行命令
subtitle:   
date:       2019-05-07
author:     Jing
header-img: img/post-bg-tips.jpg
catalog: true
export_on_save:
html: true
tags:
    - Tips
---

## 文件截取前几行，后几行，中间几行命令
如果你只想看文件的前100行，可以使用head命令，如
> head -100  filename

如果你想查看文件的后100行，可以使用tail命令，如：
> tail -100  filename 或 tail -n 100  filename

查看文件中间一段，你可以使用sed命令，如：
> sed -n '100,200p' filename 

这样你就可以只查看文件的第100行到第200行。

截取的文件可以用重定向输入到新的文件中：
> head -100  filename >a.txt

## 将两个txt文件合并成一个文件
用cat命令从文件中读入两个文件，然后将重定向到一个新的文件：

>$ cat file1.txt file2.txt > file.txt # 将file1.txt和file2.txt合并到file.txt

使用cat命令读入一个文件，然后使用>>将文本流追加到另一个文件的末位：

> $ cat file1.txt >> file2.txt # 将file1.txt追加到file2.txt的末尾
