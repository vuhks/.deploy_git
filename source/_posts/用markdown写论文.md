---
title: 用markdown写论文
tags: [markdown]
comments: false
date: 2020-07-10 11:28:05
abbrlink: markdown2
categories: md
description: 本文包含引用文献，引用图片，用pandoc生成docx格式
---
## 脚注

生成一个脚注1[^1].



[^1]: 这是 脚注 的 *内容*.

生成一个脚注2[^2].



[^2]:这里是**脚注2**的*内容*.

ps：脚注引用于脚注之间要有一个回车，不然在pandoc后不能正常生成脚注

## 文献引用

1. 导出文献引用的bib tex格式 复制到myref.bib

2. 引用格式加大括号的第一的字段

   ```
   ex.：这是对门限回归模型在年径流预测中的应用的引用[@1979门限回归模型在年径流预测中的应用]
   ```

3. pandoc 转换 
   ```powershell
   pandoc -filter pandoc-citeproc --bibligraphy=[myref的路径名]myref.bib --csl=[转换成对应文献格式的文件路径]chinese-gb7714-2006-numeric.csl xxx.md  -o xxx.docx
   ```

   ps：多个文献在同一位置的引用可以用 ' ; ' 分割。
## 图片引用

1. 使用fig：id的方式加入图的标记

2. 在文件首部加入，是引用时显示“图”，而非figure

```markdown
---
fignos-cleveref: true
fignos-plus-name: 图
fignos-caption-name: 图 
---
```

3. 对应的pandoc命令

```powershell
pandoc --filter pandoc-fignos xxx.md xxx.docx
```

ex.: 这是对图片{@fig:pic1}的引用

ps：会显示  图片1+文件名

```
![图片名](链接){#fig:pic1}
```