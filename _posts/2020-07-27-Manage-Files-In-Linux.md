---
layout: post
title: 在Linux中管理文件
date: 2020-07-27
categories: Linux
tag: Linux
---

> Write in front: <br> 重新看书的时候发现我之前有些文件习惯性地放在了 /tmp 目录下，已经不知道被自动删除了什么东西了。

### 目录

```
在Linux中管理文件
 |
 |--目录
 |--文件系统
 |--访问文件
    |-- pwd 命令
    |-- cd 命令
    |-- touch 命令
    |-- mkdir 命令
    |-- ls 命令
 |--复制、移动和删除
    |-- cp 命令
    |-- mv 命令
    |-- rm 命令
 |--文件通配
 |--参考资料
```

<hr />

### 文件系统

Linux的文件系统像一棵倒着长的树，从树根延伸出目录和子目录。

以下是系统中比较重要的目录。

| 位置 | 用途 |
| :---- | :--- |
| /     | 根目录，位于文件系统的顶部 |
| /usr  | 储存安装的软件、共享的库 |
| /etc  | 储存系统的配置文件 |
| /var  | 储存系统的可变数据，如数据库、缓存目录日志文件等 |
| /run  | 储存启动的进程运行时的数据 |
| /home | 储存普通用户的个人数据和配置文件的主目录 |
| /root | 管理超级用户root的主目录 |
| /tmp  | 储存临时文件，若其中的文件30天内未被访问、修改，将被自动删除 |
| /boot | 储存启动过程所需的文件 |
| /dev  | 储存特殊的设备文件，供系统访问硬件 |

<hr />

### 访问文件

访问文件的路径包含绝对路径和相对路径。绝对路径以根目录( / )开头，相对路径的第一个字符则是正斜杠( / )之外的其他字符。

### **pwd** 命令

`pwd` 命令用于显示当前位置的完整路径。

```
$ pwd
```

### **cd** 命令

`cd` 命令用于更改目录。

```
$ cd <directory>
```

这里可以使用绝对路径到达任意目录。或者使用相对路径在当前目录下更改目录。

还有两个特殊的目录，分别是 `.` 和 `..` 。 `.` 是当前目录， `..` 是当前目录的父目录。

```
$ pwd
/dir1/dir2
$ cd .
$ pwd
/dir1/dir2
$ cd ..
$ pwd
/dir1
```

需要回到前一个目录时，可以使用 `cd -` 命令，即使前一个目录不是当前目录的子目录。

```
$ cd -
```

>Tips: <br> 以句点 **.** 开头的文件是隐藏文件。 

### **touch** 命令

`touch` 命令用于更新文件的时间戳为当前日期和时间，而不作其他修改。如果目标是当前不存在的文件，则会创建该文件，所以 `touch` 命令通常用于创建空文件。

```
$ touch <filename>
```

### **mkdir** 命令

`mkdir` 命令用于创建目录。

```
$ mkdir <directory>
```

创建目录时，若文件名已存在，或是在不存在的父目录中创建目录，将会生成错误。使用 `-p` 选项可以为缺失的父目录创建目录。

```
$ mkdir -p par1/par2/dir
```

>Tips: <br> 使用 `-p` 选项创建目录时务必注意拼写，若因拼写错误生成了不需要的父目录，将不会生成错误信息。

### **ls** 命令

`ls` 命令用于列出当前目录下的子目录和文件。

```
$ ls
```

`-l` 选项用于列出更为详细的信息。

```
$ ls -l
```

`-h` 选项用于将列出的信息转化为人类可读的形式，但必须与 `-l` 选项同时使用。

```
$ ls -lh
```

`-a` 选项用于显示当前目录下的所有的文件，包括隐藏文件。

```
$ ls -a
```

`-R` 选项用于列出当前目录下所有文件及所有子目录中的所有文件。

```
$ ls -R
```

`-S` 选项用于按大小排序文件，而 `-t` 选项用于按时间顺序排序文件。这两个选项一般和 `-l` 选项一同使用。`-r` 选项用于对 `-S` 选项或 `-t` 选项执行反向操作。

```
$ ls -lS #按从大到小顺序列出文件
$ ls -lt #按时间顺序列出文件
```

>Tips: <br> 只有单个字母的选项可以组合使用，而组合顺序并不重要。

`--full-time` 选项用于显示完整的时间戳。

```
$ ls --full-time
```

<hr />

### 复制、移动和删除

### **cp** 命令

`cp` 命令用于复制一个或多个文件，形成新的独立文件。

```
$ cp <file1> <file2>
```

通过 `cp` 命令复制多个文件时，最后一个参数必须为目录。

```
$ cp <file1> <file2> <dir>
```

>Tips: <br> 目标目录中的冲突文件可能会被覆盖。

复制非空目录时，需要使用 `-r` 递归选项。

```
$ cp -r <dir1> <dir2>
```

### **mv** 命令

`mv` 命令用于将文件放到新的目录中。在同一目录下使用时，会重命名文件。

```
$ mv <file1> <file2>
```

### **rm** 命令

`rm` 命令用于删除文件。

```
$ rm <file>
```

`rm` 命令的默认语法只能删除文件，要删除目录及其下的子目录和文件，需要使用 `-r` 递归选项。

```
$ rm -r <dir>
```

`-i` 选项将以交互的方式确认每个删除操作。

```
$ rm -i <file>
```

`-f` 选项与 `-i` 选项正好相反，它会强制删除文件而没有提示。

```
$ rm -f <file>
```

`rmdir` 仅用于删除空目录。

```
$ rmdir <dir>
```

<hr />

### 文件通配

这一节懒得写了……

文件通配大概就是通过元字符匹配或者寻找需要的文件或目录。书上有一张表，我懒得打下来了……因为我记不住……

不过反向理解，我不知道全名的文件大概可能也不会用，不如不找出来。

碎碎念到此结束，哪天真要用上了再来更新。

<hr />

### 参考资料

[1] 红帽系统管理