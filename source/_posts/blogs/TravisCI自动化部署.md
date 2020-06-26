---
title: 使用Travis CI自动化部署Hexo
tags: [Hexo,blog,CI]
comments: false
date: 2020-06-27 00:33:34
abbrlink: travis1
categories: blogs
description: 之前就看到过这篇文章，但是觉得太麻烦，而且会把自己的md文档暴露，就没弄。最近重装了一下系统，发现重新部署hexo会有很多东西忘记，所以想把源码push到github上。

---

来自是参考这篇(https://www.jianshu.com/p/93918de6fa2c) ，按部就班的操作的，操作下来还是发现了一些问题，主要是对Git的命令了解导致的。

# Travis CI的使用

在登陆[Travis CI官网](https://link.jianshu.com/?t=https://travis-ci.org/)，选择Github源码仓库，一直到配置github的Access Token上是没有问题的。在配置.travis.yml时出了很多问题，下面是现在能回想的几个问题。

1. push到仓库时该文件上不去，后来也不知道怎么回事能上去了。在解决该问题的时候又重新学习了git的一系列命令

```powershell
git remote -v
git remote add origin [ssh地址]
git branch -a
git branch -r
git branch [newbranch]
git checkout [branch]
git add .
git commit -m "[commit]"
git push origin [branch]
```

经过不知道是什么的尝试之后，push成功了，其中做过删库操作，我觉得是这个操作解决的

2. 修改过几次.travis.yml文件（~~瞎改~~）

由于我是用yarn安装的hexo和一些插件，怕后面源码跟tr搭建的环境无法匹配，就修改了install的一些命令，发现修改后出错了，出错的地方就是yarn的语法错误，所以我删掉了

```
install:
	-npm install
```

发现语法没错了。但我不知道用npm与yarn有什么区别，应该是没有的，我不修改应该也是不会出问题的。但我之前看过yarn比npm的优点，记得文件目录是不太一样的，具体记不太清了。

3. branch的问题

   这个不知道原博主是怎么操作的，可能由于我对git的命令不熟悉，导致我本地的文件目录弄混了，不知道哪是哪了，后来就直接用master分支了，这其中就又涉及到了删除本地与远程分支的问题。看了一下教程，最后还是删库解决的。真是错误百出啊。

# 隐私问题

   我的博客中有一些加密的文章，我直接上传源码的行为很蠢，所以现在想做的是把带有加密的md文件从源码中删除，自己从本地deploy。

   已解决：push的时候忽略文件，直接修改.gitignoire文件，加入想忽略的目录

   这衍生出的一个问题是，修改hexo/source/_post/中的目录结构后，影响hexo的生成吗？测试结果是不影响，具体的逻辑不知道。

  可能出现的问题：
   1. 自动化部署的时候会不会降我自己部署的文章给删掉？这个还没测试。
   2. 如果删掉，怎么解决？能不能修改.travis.yml文件，或者给Travis增加一些限制，不让它动我的某些文档

