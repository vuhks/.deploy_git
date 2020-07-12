---
title: 永久免费主机euserv获得与使用
tags: [blog,linux,vps]
comments: false
date: 2020-07-12 18:19:45
abbrlink: euserv
categories: blogs
description: 偶然的机会（逛知乎）看到能白嫖euserv小鸡，看着这种好事就跟狗看见屎一样地兴奋，折腾了一下午
---

## 撸EUserv

> 根据网络上的教程一步一来的，这里先记录一下

参考这篇[EUserv 德国永久免费VPS申请与简单使用教程 – 仅有IPv6网络](https://www.daniao.org/8436.html)

1.申请免费主机

地址：[https://www.euserv.com/en/virtual-private-server/root-vserver/v2/vs2-free.php](https://www.daniao.org/wp-content/themes/begin/go.php?url=aHR0cHM6Ly93d3cuZXVzZXJ2LmNvbS9lbi92aXJ0dWFsLXByaXZhdGUtc2VydmVyL3Jvb3QtdnNlcnZlci92Mi92czItZnJlZS5waHA=)

选择“vServerVS2”下拉菜单中的“VS2-free”申请

没图

后面按步骤点击，先order，再go to checkout,在这一步需要register，最后proceed checkout

2.登陆用户中心

补充个人信息，商家会审核你的信息，我是13：00左右开始申请的，中间给我14:00左右发了一个邮件提醒我Your contact data is incomplete修改之后提醒我copleted，在15：00左右邮件通知我has been processed.英语不好，只知道是个完成时态。

3.重装系统

4.找root密码

configure-server date

5.ssh连接

这里出现一点问题

> 1.等root密码出来之后，给出的ipv6地址才能ping通
>
> 2.确认本地有ipv6地址，简单点的测试。(https:\\ip.sb)会有显示

到此申请的活干完了

## 使用

### 嵌套cloudflare使用ipv4访问



### 配置v2ray

### 搭建个人blog



