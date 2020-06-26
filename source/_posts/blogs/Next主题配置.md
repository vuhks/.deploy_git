---
title: Next主题配置
tag: [blogs,Hexo]
date: 2020-5-28 01:16:59
abbrlink: hexo-next1
categories: blogs
description: [通过修改next主题文件```_config.yml```来实现]
---
# 修改next主题文件```_config.yml```
[参考https://theme-next.js.org/docs/getting-started/](https://theme-next.js.org/docs/getting-started/)
## 添加CDN连接
修改```mediunzoom :true```然后使用默认配置
## next方案选择
在```scheme ```关键字来更改方案
默认方案是mise
```
schme: Muse
```
## 启用暗黑模式
主题NexT会根据系统模式自动切换至黑暗模式
```
darkmode: true
```
## 修改站点语言
```
language: zh-CN
```
## 配置头像
侧边栏显示头像
```
avatar:
  # Replace the default image and set the url here.
  url: /images/avatar.gif
  # If true, the avatar will be dispalyed in circle.
  rounded: false
  # If true, the avatar will be rotated with the cursor.
  rotated: true
```