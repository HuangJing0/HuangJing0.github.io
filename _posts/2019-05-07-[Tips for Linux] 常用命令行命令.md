---
layout:     post
title:      Tips - 常用命令行命令
subtitle:   记录自己用到(记不住)的命令行命令
date:       2019-05-07
author:     Jing
header-img: img/post-bg-tips.jpg
catalog: true
export_on_save:
html: true
tags:
    - Tips
---

## 1. 文件截取前几行，后几行，中间几行
* 查看文件的前100行，可以使用head命令
  > head -100  filename

* 查看文件的后100行，可以使用tail命令
  > tail -100  filename
     tail -n 100  filename

* 查看文件中间一段，可以使用sed命令
  > sed -n '100,200p' filename  # 只查看文件的第100行到第200行

* 截取的文件可以用重定向输入到新的文件中：
   > head -100  filename >a.txt

## 2. 将两个txt文件合并成一个文件
* 用cat命令从文件中读入两个文件，将重定向到一个新的文件
  > cat file1.txt file2.txt > file.txt # 将file1.txt和file2.txt合并到file.txt

* 用cat命令读入一个文件，然后使用>>将文本流追加到另一个文件的末位
  > cat file1.txt >> file2.txt # 将file1.txt追加到file2.txt的末尾

## 3. github
* 检查电脑是否通过github仓库的sshkey认证
   > ssh -T git@github.com

* 对自己的github仓库进行下载和上传
   > git init  #这个命令会在当前目录下创建一个.git文件夹。
    git add ./  #这个命令会把当前路径下的所有文件，添加到待上传的文件列表中。
    git commit -m "xxxxx"  
    git remote add origin git@github.com:xuhongxin/deom.git  
    git pull origin master  #下载所有
    git push -u origin master  #上传所有

## 4. 删除文件
* 强制删除并提示
  > sudo rm -r 文件夹名

* 强制删除不提示: -r表示强制删除,-f表示不提示
  > sudo rm -rf 文件夹名

## 5. Ubuntu保存终端内容到日志
* 开始保存
  > sudo script screen.log

* 停止保存
  > exit

## 6. ubuntu 生成ssh key及查看
* 检查本地是否有SSH Key存在
  > ls -al ~/.ssh

* 生成新的SSH key
  > ssh-keygen -t rsa -C "your_email@example.com"
  ssh-add ~/.ssh/id_rsa
  cat /Users/xxx/.ssh/id_rsa.pub

## 7. vim 删除一整块，vim 删除一整行
    dd:删除游标所在的一整行(常用)
    ndd:n为数字。删除光标所在的向下n行，例如20dd则是删除光标所在的向下20行
    d1G:删除光标所在到第一行的所有数据
    dG:删除光标所在到最后一行的所有数据
    d$:删除光标所在处，到该行的最后一个字符
    d0:那个是数字0,删除光标所在到该行的最前面的一个字符
    x,X:x向后删除一个字符(相当于[del]按键),X向前删除一个字符(相当于[backspace]即退格键)
    nx:n为数字，连续向后删除n个字符
