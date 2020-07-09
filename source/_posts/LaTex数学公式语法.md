---
title: LaTex数学公式语法
tags: [markdown]
date: 2020-06-19 14:41:32
mathjax: true
abbrlink: LaTex1
categories: markdown
description: 在Typora中插入数学公式
---

# 两种公式模式

在Typora中可以修改为LaTex公式插入，其中有两种模式行内（内联）公式和公式块。

## 行内

```"`LaTex"``
$ a^2+b^2=c^2 $
```
显示为$ a^2+b^2=c^2 $

## 公式块

```LaTex
$$ \Delta=\frac{b^2-4ac}{c^2} $$
```

$$ \Delta=\frac{b^2-4ac}{c^2} $$

# LaTex数学公式语法

参考自csdn的[LaTex数学公式语法](https://blog.csdn.net/guikunchen/article/details/88652407)

## 上标、下标

上标用^，下标用_
		a^2 X_1显示为：$a^2 X_1$

a^{xy} y_{ab}显示为：$a^{xy} y_{ab}$

### 复合型

用{}进行分割

X^{y^{g(x)}}显示为$X^{y^{g(x)}}$

## 方根\sqrt[]{}

\sqrt[3]{a^2+b^2+c^2} 显示为$\sqrt[3]{a^2+b^2+c^2}$

\sqrt{a^2+b^2+c^2} 显示为$\sqrt{a^2+b^2+c^2}$

方根语法为\sqrt[n]{}默认$n=2$

## 大括号

### 水平大括号\overbrace

$\overbrace{1,2,3,\cdots,100}^{100}$，其中用\cdots表示$\cdots$
### 三种大括号方法
```mathjax
方法一：

$$ f(x)=\left\{
\begin{aligned}
x & = & \cos(t) \\
y & = & \sin(t) \\
z & = & \frac xy
\end{aligned}
\right.
$$
```
$$ f(x)=\left\{
\begin{aligned}
x & = & \cos(t) \\
y & = & \sin(t) \\
z & = & \frac xy
\end{aligned}
\right.
$$
方法二：
```

$$ F^{HLLC}=\left\{
\begin{array}{rcl}
F_L       &      & {0      <      S_L}\\
F^*_L     &      & {S_L \leq 0 < S_M}\\
F^*_R     &      & {S_M \leq 0 < S_R}\\
F_R       &      & {S_R \leq 0}
\end{array} \right. $$
```
$$ F^{HLLC}=\left\{
\begin{array}{rcl}
F_L       &      & {0      <      S_L}\\
F^*_L     &      & {S_L \leq 0 < S_M}\\
F^*_R     &      & {S_M \leq 0 < S_R}\\
F_R       &      & {S_R \leq 0}
\end{array} \right. $$
方法三:
```

$$f(x)=
\begin{cases}
0& \text{x=0}\\
1& \text{x!=0}
\end{cases}$$
```
$$f(x)=
\begin{cases}
0& \text{x=0}\\
1& \text{x!=0}
\end{cases}$$




## 分数\frac{}{}

$\overline x=\frac {x_1+x_2+x_3}{3}$

## 积分\int_{a}^{b}{}

### 不定积分

$$\int{cosxdx}=sinx+c$$

### 定积分

$$\int_{a}^{b}f(x)dx=F(b)-F(a)$$

## 累加、累乘

$$\sum\limits_{a}^{b}$$

$$\prod\limits_{a}^{b}{f(x)}$$

## 向量

$$\vec a=\overrightarrow{AB}=-\overleftarrow{BA}$$

# LaTex数学符号常用表

## 数学模式重音符
![NKUag1.png](https://s1.ax1x.com/2020/06/19/NKUag1.png)
## 小写希腊字母
![NKU0u6.png](https://s1.ax1x.com/2020/06/19/NKU0u6.png)
## 大写希腊字母
![NKUU3R.png](https://s1.ax1x.com/2020/06/19/NKUU3R.png)
## 二元关系符
[![NKBz4S.th.png](https://s1.ax1x.com/2020/06/19/NKBz4S.png)
## 二元运算符
![NKUY4J.png](https://s1.ax1x.com/2020/06/19/NKUY4J.png)
## 大尺寸运算符
![NKUdjx.png](https://s1.ax1x.com/2020/06/19/NKUdjx.png)
## 箭头
![NKUgCd.png](https://s1.ax1x.com/2020/06/19/NKUgCd.png)
## 定界符
![NKUyUe.png](https://s1.ax1x.com/2020/06/19/NKUyUe.png)
## 大尺寸定界符
![NKUsED.png](https://s1.ax1x.com/2020/06/19/NKUsED.png)
## 其他符号

省略号\dots：$\dots$

省略号\cdots：$\cdots$

空格\quad：测$\quad$试

![NKU64H.png](https://s1.ax1x.com/2020/06/19/NKU64H.png)

