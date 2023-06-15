# 1. Shell

shell是一个用C语言编写的程序，它是用户使用linux的桥梁。

## 1.1 Shell脚本

shell脚本(shell script)是一种为shell编写的脚本程序。

业界所说的shell通常指shell脚本，但是shell和shell script是两种不同的概念。

## 1.2 Shell环境

Shell 编程跟 JavaScript、php 编程一样，只要有一个能编写代码的文本编辑器和一个能解释执行的脚本解释器就可以了。

Linux 的 Shell 种类众多，常见的有：

- Bourne Shell（/usr/bin/sh或/bin/sh）
- Bourne Again Shell（/bin/bash）
- C Shell（/usr/bin/csh）
- K Shell（/usr/bin/ksh）
- Shell for Root（/sbin/sh）
- ……

我们常用的Bash，也即大多数linux系统默认的bash是Bourne Again Shell。在一般情况下，人们并不区分Bourne Again Shell和Bourne Shell，所以，像**#!bin/sh**，它同样可以改为**#!bin/bash**。

**#!告诉系统其后路径指定的程序即是解释次脚本文件的shell程序**。

# 2 Shell变量

## 2.1 命名规范

注意，**变量名和等号之间不能有空格**。同时，变量名的命名须遵循如下规则：

- 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。
- 中间不能有空格，可以使用下划线 **_**。
- 不能使用标点符号。
- 不能使用bash里的关键字（可用help命令查看保留关键字）。

## 2.2 变量操作

### 2.2.1 定义变量

```shell
my_name="willam"
```

### 2.2.2 使用变量

````shell
echo $my_name
echo ${my_name}
echo "${my_name}"
````

花括号是为了帮助编译器识别变量的边界

```shell
echo ${my_name}Script
```

推荐给所有的变量加上花括号,这是一个好的编程习惯.

### 2.2.3 只读变量

```shell
readonly my_url
my_url="https://www.google.com"
```

### 2.2.4 删除变量

```shell
unset variable_name
```

## 2.3 变量类型

运行shell时，会同时存在三种变量：

- **1) 局部变量**:局部变量在脚本或命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量。
- **2) 环境变量**:所有的程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候shell脚本也可以定义环境变量。
- **3) shell变量**:shell变量是由shell程序设置的特殊变量。shell变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了shell的正常运行

### 2.3.1 Shell字符串

字符串是shell编程中最常用最有用的数据类型（除了数字和字符串，也没啥其它类型好用了），字符串可以用单引号，也可以用双引号，也可以不用引号。

单引号字符串的限制:

- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
- 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。

双引号字符串的优点:

- 双引号里可以有变量
- 双引号里可以出现转义字符

**拼接字符串**

```bash
str="abc"
# 使用双引号拼接
greeting="hello, "$str" !"
greeting_1="hello, ${str} !"

echo $greeting $greeting_1

# 使用单引号拼接
greeting_2='hello, '$str' !'
greeting_3='hello, '${str} !'
echo $greeting_2 $greeting_3
```

输出结果为:

```bash
hello, runoob ! hello, runoob !
hello, runoob ! hello, ${your_name} !
```

**获取字符串长度**

```bash
string="abcd"
echo ${#string}		# 输出4
echo ${#string[0]}	# 输出4
```

**提取子字符串**

```bash
string="my name is willam"
echo ${string:1:4}
```

**查找子字符串**

```bash
string="my name is willam"
echo `expr index "$string" io`	# 输出4
```

### 2.3.2 Shell数组

bash支持一维数组(不支持多维数组),并且没有限定数组的大小.使用下标获取数组中的元素.

**定义数组**

```bash
数组名=(值1 值2 ... 值n)
```

也可以单独定义数组的各个分量

```
array_name[0]=value0
array_name[1]=value1
array_name[2]=value2
```

**读取数组**

```bash
value=$(array_name[n])
```

```bash
# 获取数组的所有元素
echo ${array_name[@]}
```

**获取数组长度**

```bash
# 获取数组元素的个数
length=${#array_name[@]}
# or
length=${#array_name[*]}
# 获取数组单个元素的长度
lengthn=${#array_name[n]}
```

### 2.3.3 Shell注释

单行注释:#

多行注释:

```bash
:<<EOF
content
content
content
......
EOF
```

```
:<<'
content
content
......
'
```

```
:<<!
content
content
......
!
```

# 3 Shell数组

Bash支持关联数组,可以使用任意的字符串、或者整数作为下标来访问数组。

关联数组使用**declare**命令来声明,关联数组的键是唯一的.

```bash
declare -A array_name
```

```bash
declare -A site=(["google"]="www.google.com" ["baidu"]="www.baidu.com" ["github"]="www.github.com")
# or
declare -A site
site["google"]="www.google.com"
site["baidu"]="www.baidu.com"
site["github"]="www.github.com"

echo "${site["baidu"]}"

# 在数组前面加一个!可以获取数组的所有键
echo "数组的键为: ${!site[*]}"
echo "数组的键为: ${!site[@]}"
```

# 4 Shell运算符

## 4.1 算术运算符

```bash
#!/bin/bash

a=10
b=20

val=`expr $a + $b`
echo "a + b : $val"

val=`expr $a - $b`
echo "a - b : $val"

val=`expr $a \* $b`
echo "a * b : $val"

val=`expr $b / $a`
echo "b / a : $val"

val=`expr $b % $a`
echo "b % a : $val"

if [ $a == $b ]
then 
	echo "a 等于 b"
fi

if [ $a != $b ]
then 
	echo "a 不等于 b"
fi
```

# 5 Shell echo命令

