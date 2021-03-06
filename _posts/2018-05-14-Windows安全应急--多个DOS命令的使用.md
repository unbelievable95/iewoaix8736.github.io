---
layout: post
title: "（一）Windows安全应急--多个DOS命令的使用"
date: 2018-05-13
description: "应急响应（Windows篇）"
tag: 应急响应（Windows篇）
---
---

**DOS命令学习笔记**<br/>
（注：以下演示截图可能跟命令不同）

---

### 目录
1. dir命令<br/>

2. copy和xcopy命令<br/>

3. del、deltree和rd命令<br/>

4. move命令<br/>

5. attrib命令<br/>

6. netstat命令<br/>

7. mstsc命令<br/>

8. 用户添加命令

---

### 1. dir命令

<h2>常用参数：</h2>

/A  -- 仅显示A参数表中指定的文件<br/>

/S  -- 显示指定目录及所有子目录中文件<br/>

/W  -- 以“横”方式排列显示<br/>

/P  -- 每显示满一屏停顿一下，待用户按任意键后再继续显示下一屏（在多文件的时候可以使用这一方法）<br/>



**下面进行命令演示**

```
dir /a
```

![images](/images/2018-05-13/dos01.png)


```
dir /s
```
/S 参数多了一个显示所有文件总数，感觉跟 /a 参数没多大区别


![images](/images/2018-05-13/dos02.png)


```
dir /w
```
文件横着排列，而不是竖着排


![images](/images/2018-05-13/dos03.png)


```
dir /p
```

在目录文件多的时候，可以使用这个命令来进行页条分析


![images](/images/2018-05-13/dos04.png)

---


### 2. copy和xcopy命令

**copy只能拷贝XX文件夹下的文件，不能拷贝XX文件夹下的文件夹**

**xcopy能拷贝XX文件夹下的所有文件，包括文件夹**


<h3>常用参数：</h3>

**（注：使用copy命令时不需要参数）**

/S --复制目录和子目录，除了空的

/E --复制目录和子目录，包括空的

/W --提示您在复制前按键

/C --即使有错误，也继续复制

/H 也复制隐藏和系统文件


<h3>演示一下</h3>

```
copy C:\ D:\ 
```
表示复制C盘的所有文件到D盘，不包括文件夹<br/>

使用copy命令复制“yanshi”文件夹内的文件到“yanshi02”文件夹内,<br/>

可以看到，只能复制文件，不能复制“演示1”，“演示2”文件夹


![images](/images/2018-05-13/dos05.png)


```
xcopy C:\ D:\
```

表示复制C盘的所有文件到D盘，包括文件夹<br/>

这里使用相同的命令复制文件，唯一不同的是，xcopy需要使用参数，这里使用 **/E /H**参数<br/>


![images](/images/2018-05-13/dos06.png)

---


### 3. del、deltree和rd命令

**del只能删除一个或者多个文件，不能删除文件夹**<br/>

**deltree是一个外部命令，他可以删除文件及文件夹，以及其子文件夹**<br/>

**rd删除空文件夹**<br/>


<h3>常用参数</h3>

/S --删除下级文件夹和所有文件<br/>

/q --安静模式，不提示<br/>


<h3>演示</h3>

```
del C:\ 
```
表示删除C盘里面的所有文件，但不会文件夹，加上“/s”参数会删除文件夹里面的文件<br/>

使用del命令，加“/S”参数的话,会删除目录下包括子目录的所有文件，不加只会删除目录下的文件，不会删除子目录内的文件<br/>

加上“/q”参数的话，就不会出现让你确认删除的提示，默认全部删除<br/>


![images](/images/2018-05-13/dos07.png)


```
deltree C:\
```
表示删除C盘里面的所有文件<br/>

使用这个命令的话，需要通过调用外部DOS执行程序“deltree.exe”

```
rb C:\123
注：删除C盘里面名字为“123”的空文件夹（需要空文件夹的绝对路径）
```
使用这个命令的，需要空文件夹的绝对路径，<br/>

比如“C:\123\321”， “321”才是空文件夹<br/>

那么命令就应该是:
```
rd C:\123\321
```
(注：演示02为空文件夹，同样，如果加“/s”参数的话，路径所在的文件夹将被删除，不是空文件夹也会被删)


![images](/images/2018-05-13/dos08.png)

---


### 4. move命令

**move命令可以移动一个或者多个文件，他跟copy很相似，区别在于，copy是复制，文件move是移动文件**<br/>


<h3>常用参数</h3>

/Y --移动目标文件夹内有相同名字的文件时，不会提示，默认覆盖<br/>

/-Y --与之相反，会提示


<h3>演示</h3>

```
move /y C:\1.txt D:\ 
```
注：移动C盘里面的1.txt文件到D盘,“/y”参数表示不提示


![images](/images/2018-05-13/dos09.png)

---


### 5. attrib命令

**attrib命令用于解决因病毒导致所有文件夹被隐藏的问题，它可以修改文件的属性**


<h3>常用参数</h3><br/>

"+"  --表示设置属性。<br/>

"-"  --表示清除属性。<br/>

R  --表示只读文件属性。<br/>

A  --表示存档文件属性。<br/>

S  --表示系统文件属性。<br/>

H  --表示隐藏文件属性。<br/>


<h3>使用方法</h3>

```
attrib -r -a -s -h C:\abc
```
“-”号表示清除属性，abc为文件夹名，这个命令也可以修改文件的属性，换成“+”则是设置属性

---


### 6. netstat命令

**netstat命令用于查看网络连接、接口等信息**<br/>


<h3>常用参数</h3>

-a 显示所有连接和侦听端口。

-c 每隔1秒就重新显示一遍，直到用户中断它。<br/>

-i 显示所有网络接口的信息，格式“netstat -i”。<br/>

-n 以网络IP地址代替名称，显示出网络连接情形。<br/>

-r显示核心路由表，格式同“route -e”。<br/>

-t 显示TCP协议的连接情况<br/>

-u 显示UDP协议的连接情况。<br/>

-v 显示正在进行的工作。<br/>

-p 显示建立相关连接的程序名和PID。<br/>

-b 显示在创建每个连接或侦听端口时涉及的可执行程序。<br/>

-e 显示以太网统计。此选项可以与 -s 选项结合使用。<br/>

-f 显示外部地址的完全限定域名(FQDN)。<br/>

-o 显示太网统计信息(timers)。<br/>

-s 显示每个协议的统计。<br/>

-x 显示 NetworkDirect 连接、侦听器和共享端点。<br/>

-y 显示所有连接的 TCP 连接模板。无法与其他选项结合使用<br/>


<h3>演示</h3>

```
netstat -an
```
可以多个参数一起使用


![images](/images/2018-05-13/dos10.png)

---


### 7. mstsc命令

**mstsc命令用于打开远程桌面连接**

<h3>常用参数</h3>

/admin --忽略最大连接数（强制连接可能会把别人挤掉）<br/>

```
开始运行 -> mstsc
```

---


### 8. 用户添加命令

**1. 查看本地用户**
```
net user
```

**2. 添加一个用户名为abc，密码为123的用户**
```
net user abc 123 /add
```

**3. 添加一个用户名为abc，密码为123的用户**
```
net user abc 123 /add
```

**4. 加入管理员组**
```
net localgroup administrator abc /add
```

**5. 激活禁用的用户**
```
net user abc /active:yes
```

**6. 删除用户名为abc的用户**
```
net user abc /del
```

---

**当然不止这些，后面学到还会继续更新......**
