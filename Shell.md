# Shell

shell是一个用C语言编写的程序，它是用户使用linux的桥梁。

## Shell脚本

shell脚本(shell script)是一种为shell编写的脚本程序。

业界所说的shell通常指shell脚本，但是shell和shell script是两种不同的概念。

## Shell环境

Shell 编程跟 JavaScript、php 编程一样，只要有一个能编写代码的文本编辑器和一个能解释执行的脚本解释器就可以了。

Linux 的 Shell 种类众多，常见的有：

- Bourne Shell（/usr/bin/sh或/bin/sh）
- Bourne Again Shell（/bin/bash）
- C Shell（/usr/bin/csh）
- K Shell（/usr/bin/ksh）
- Shell for Root（/sbin/sh）
- ……

我们常用的Bash，也即大多数linux系统默认的bash是Bourne Again Shell。在一般情况下，人们并不区分Bourne Again Shell和Bourne Shell，所以，像**#!bin/sh**，它同样可以改为**#!bin/bash**。

**#！告诉系统其后路径指定的程序即是解释次脚本文件的shell程序**。

