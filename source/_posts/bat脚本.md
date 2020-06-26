---
title: bat脚本学习
date: 2020-06-21 15:47:30
abbrlink: bat1
categories: windows
tags: [学习,windows]
mathjax: false
description: 
---
来自(https://blog.csdn.net/liuker888/article/details/47355995)
> BAT脚本作为dos时代的批处理脚本，已经过时了，但是作为win系统里执行简单的脚本，简单的了解和使用可以减少重复性的劳动。

# 常用命令

## 1. echo 类似print

```powershell
echo   		 #显示当前echo的状态
echo.   	 #输出一个空白行
echo,  echo; echo+ echo[echo] echo/ echo\
echo on   	#从下一行开始打开回显
echo off  	#从从下一行开始关闭回显
@ 			#关闭本行回显                                 
@echo off 	#从本行开始关闭回显
```
## 2.errorlevel



```powershell
echo %errorlevel%
```

每个命令运行结束，可以用这个命令行查看返回值，默认为0，出错errorlevel为1.

## 3. dir

```powershell
dir			#显示当前目录中的文件和子目录，同ls  
dir /a		#显示当前目录中的文件和子目录，包括隐藏文件和系统文件
dir c:/a:d	#显示c盘目录中的目录
dir /a:-d	#显示当前目录中的文件                         
dir /b \p	#只显示文件名，分页显示  
dir *.exe /s#显示当前目录和子目录中所以exe的文件
/a #指定属性
	[:]d #目录
	[:]- #否定前缀
/b #使用空格式
/c #显示指定目录和所有子目录中的文件
```
注意：windows下文件的标准规范路径用的是\

## 4. cd

```powershell
cd#显示当前目录 pwd 
cd\ #进入根目录 
cd /d d:/sdk#同时改变盘符和目录
cd d:\ #改变盘符
```

## 5. md



```powershell
md d:\a\b\c
mkdir e:\a\c\d
```

新建目录一个目录，如果前一级目录不存在，将会自动创建

## 6. rd



```powershell
rd abc 		  #删除当前目录里的abc子目录，要求为空目录
rd /s /q temp #删除当前目录里的temp文件夹及其子文件家和文件，/q为安静模式 相当于rm -rf
```

## 7. del

```powershell
del d:\text.txt	#删除指定文件，不能是隐藏、系统、只读文件
del /q/a/f d:\temp\*.* #删除该文件夹里的所有文件，包括隐藏文件，不包括子目录
/q #表示安静模式
/f #强制删除只读文件
del /q/a/f/s d:\temmp\*.*#删除该文件夹，包括子目录
```

del是删除目标的子文件，rd是删除目标文件

## 8. ren重命名

```pow
ren d:\temp tmp #将tmep重命名为tmp
```



## 9. cls清屏

## 10. type显示文件内容

类似cat

```pow
type c:\boot.ini #显示指定文件的内容
type *.txt #显示当前目录所以txt文件的内容
chcp 65001 #将代码页改为utf-8，默认为GBK936
```



## 11. copy拷贝文件

```powershell
copy c:\test.txt d:\test.bak #复制文件并重命名
copy con test.txt #从屏幕上等待输入，按Ctrl+Z结束输入，输入内容存到test.txt
```

经测试，会覆盖到原文件内容，而且回车就结束了，Ctrl+Z会显示为字符，并不能结束

```powershell
copy 1.txt + 2.txt 3.txt 	#合并1.txt和2.txt的内容，保存为3.txt
copy 1.txt + 2.txt			#合并1.txt和2.txt的内容，默认保存到1.txt
copy test.txt + 			#复制文件到自己，实际上修改的文件的日期
```

 

## 12.  title 设置cmd命令的标题

## 13.  ver 显示系统版本

## 14.  label和vol 设置卷标

```powershell
vol 			#显示卷标
labelc: system 	#设置卷标为sysyem
```

## 15.pause暂停命令

## 16.  rem和:: 注释命令

```powershell
md rem 与mkdir相同
type :: 显示文本内容
```



## 17. date和time日期和时间

```powershell
date /t #显示当前日期
time /t #显示当前时间
不带参数时，默认为修改时间、日期
```

## 18. goto和：跳转命令

```powershell
:label #行首为“：”表示该行是标签行，标签行操作不执行
goto label #跳转到指定的标签行
```

标签行只是一个标签，也只能是一个标签，goto命令与:配合执行跳转命令。

## 19. find（外部命令）查找

```powershell
find "abc" c:test.txt #在test中查找含字符串abc的行，显示的是带有该字符串的行的内容，如果找不到，将errorlevel返回码置1
/i 忽略字符串大小写
/c 计数，显示含abc的行的行数，

```



## 20. more（外部命令）

```powershell
more c:\test.txt #逐屏显示文本文件内容
```



## 21. tree

显示指定目标文件目录结构

## 22. &

顺序执行多条命令，不管命令是否成功执行

## 23. &&

顺序执行多条命令，当碰到执行出错的命令后将不执行后面的命令

```powershell
find \"ok\" c:\test.txt && echo 成功	#如果找到了\"ok\"字样，就显示\"成功\"，找不到就不显示
```



## 24. ||

顺序执行多条命令，当碰到正确的命令后将不执行后面的命令

```powershell
find "ok" a.txt||echo 不成功 #如果找不到“ok”,就显示不成功，找到了就不显示
```



## 25. | 管道命令

管道命令：先执行前置命令，后对前置命令作为后置命令的目标

```powershell
dir *.*/s/a | find /c ".exe" #先执行dir命令，显示当前目录及所有子目录中的文件，包括隐藏、系统、只读文件，再从此结果中找到所有带.exe的文件的个数
```



## 26. \>和\>>输出重定向命令

\>清除文件内容中的原有内容后再写入

\>>追加内容到文件末尾，而不会清除原有的内容

主要讲本来显示在屏幕上的内容输出到指定的文件中，如果指定文件不搓澡，则会自动生成该文件。

```powershell
type c:\test.txt >prn #本该显示到屏幕上的test文本内容，输出转到打印机
echo hello word >con #本该显示到屏幕上的echo内容，输出转到打印机
copy c:\test.txt f:>nul#复制test.txt到f盘，是否成功输出到nul，即不显示是否成功的提示，如果f盘不存在，会显示系统找不到指定的驱动器
copy c:\test.txt f:>nul 2>nul #如果f盘不存在，也不会提示
echo ^^W ^> ^W #屏幕显示的是^W>W，这条命令告诉我们echo不能直接显示^和>,要想显示^和>，需要在前面加>。
echo ^^W ^> ^W >c:\test.txt #将echo内容重定向输出到test中
```



注意：^ 和 > 是控制命令，要把它们输出到文件，必须在前面加个 ^ 符号

## 27. <重定向输入指令

从文件中获得输入信息，而不是从屏幕中，一般用于date、time、label等需要等待屏幕输入的指令

```powershell
@echo off
echo 2020-6-22 >temp.txt
date <temp.txt
del temp.txt
#不用等待输入直接修改当前日期
```





## 28. %n批参数

命令行传递给批处理的参数

```powershell
%0		#批处理文件本身
%1 		#第一个参数
%9 		#第九个参数
%* 		#从第一个参数开始的所有参数
%~1 	#删除引号，扩充%1
%~f1	#将%1扩充到一个完全合格的路径名
%~d1	#仅将%1扩充到一个驱动区号
%~p1
%~n1
%~x1
%~s1
%~a1
%~t1
%~z1
%~$PATH:1
```



## 29. if
## 30. seltocal和endlocal
## 31. set
## 32. start
## 33. call
## 34. choice（外部命令）
## 35. assoc和ftype
## 36. pushd和popd
## 37. for
## 38. subst（外部命令）
## 39. xcopy