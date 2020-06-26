---
title: onedrive同步任意文件夹
tags: [配置,windows]
date: 2020-05-29 16:19:20
abbrlink: onedrive
categories: windows
description: [onedrive同步默认同步只能同步onedrive文件夹下的文件，不能把任意路径的文件夹添加到onedrive文件夹下，特此寻找一种方法。 ]
---
onedrive同步默认同步只能同步onedrive文件夹下的文件，不能把任意路径的文件夹添加到onedrive文件夹下，特此寻找一种方法。  
参考的[ilxin.com](http://suo.im/61pOuI)  
基本语法
```
mklink [/d] | [h] | [/j] 目标地址 原始地址
```
其中，
```
    /d 创建目录符号链接，默认为文件符号链接
    /h 创建硬链接，而不是符号链接
    /j 创建目录链接

```
    
例如，将```E:\vuhks\blogs```路径下的文件夹备份的onedrive目录下
```
mklink /d "C:\xxx\onedrive\blogs" "E:\vuhks\blog"
```
主要注意的是：  
1. mklink 用管理员方式打开 CMD命令  
2. ```" "```要有，因为```/d```是符号链接  
3. 目标地址是onedrive的默认同步的onedrive文件路径，一般是安装onedrive时用户选择的路径  
4. 关联的blogs文件夹不能存在，因为这个命令会自己建一个blogs名的链接（相当于快捷方式）

在我看来，就是在onedrive的目录下建一个快捷方式，可以关联到你想要同步的路径下

成功后显示
```
    C:\xxx\onedrive\blogs <<==>> E:\vuhks\blog 创建的符号链接
```