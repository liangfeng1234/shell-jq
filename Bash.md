# 内置变量

\$\$-当前进程ID

\$PPID-父进程ID

\$0-脚本的名字

\$0、\$1、\$2...\$n-第一个参数、第二个参数、第三个参数...第n个参数,(第十个及以后的参数需要用大括号括起来，例如\${10})

\$#-从命令行传入脚本的参数数量

\$*和\$@都表示位置参数，但是它们有一些区别

\$*-每个位置的参数被当成一个独立的单词来处理

"\$*"-所有位置的参数被当成一个独立的单词来处理

\$@-无论加不加引号，每个位置的参数都被当成一个独立的单词来处理

# Shell中空值、非空值和不存在的辨别
## 字符串变量加""和不加""的区别
```
a=""
$[-z $a]&&echo Null || echo NotNull
Null
```

```
a=""
$[-n $a]&&echo NotNull || echo Null
NotNull
```
如果$a不加双引号相当于该参数不存在，即只有-z或者-n一个参数，所以结果永远是前者。

## -n和-z的区别
-n代表判断一个变量是否不为空，-z代表判断一个变量是否为空

## 使用-n判断一个变量为空、非空或者不存在
```
a=""
$[-n "$a"]&&echo Null || echo NotNull

```

```
a=
$[-n "$a"]&&echo Null || echo NotNull

```

```
a="abc"
$[-n "$a"]&&echo Null || echo NotNull

```


## 使用-z判断一个变量为空、非空或者不存在
```
$[-z "$b"] && echo Null || echo NotNull

```

```
b=""
$[-z "$b"] && echo Null || echo NotNull

```

```
b="abc"
$[-z "$b"] && echo Null || echo NotNull

```

## =和==
```
a=""
$[ "$a" == "" ] && echo YES || echo NO
YES
$[ "$b" == "" ] && echo YES || echo NO
YES
```
使用=和==判断两个字符串相等的方式也不能判断其是不存在还是空值

## 如何判断空和不存在
```
a=""
$echo ${a-NotDefine}

$echo ${b-NotDefine}
NotDefine
```
${var-default}的意义是有值传值(包括空值),未定义传default字符串。