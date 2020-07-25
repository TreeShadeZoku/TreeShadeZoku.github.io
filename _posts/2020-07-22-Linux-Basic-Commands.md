---
layout: post
title: Linux基础命令
date: 2020-07-22
categories: Linux
tag: Linux
---

> Write in front: <br> 写一些东西督促自己把 Linux 里没学会的东西复习一遍。《红帽系统管理》的内容挺丰富的，希望能坚持到写完……或者写得差不多。

### 目录

```
Linux基础命令
 |
 |--目录
 |--在 Windows 环境下安装 Linux 虚拟机
 |--一些简单的命令
    |-- date 命令
    |-- file 命令
    |-- wc 命令
    |-- history 命令
    |-- ifconfig 命令
 |--编辑命令行
 |--个性化配置
    |--更换时区
    |--修改默认语言
 |--参考资料
```

<hr />

### 在 Windows 环境下安装 Linux 虚拟机

首先我并不是很想写这部分，不是因为觉得太简单看不起啥的，纯粹是因为我把具体过程忘了……但是大体上还是记得的，就随便写点简单的过程。由于我本人没有 Mac 电脑，没接触过这个环境，就不献丑了。

将要使用的软件是 **Vmware Workstation Pro** ，可以去[这个网址](https://www.vmware.com/cn/products/workstation-pro/workstation-pro-evaluation.html)下载：

```
https://www.vmware.com/cn/products/workstation-pro/workstation-pro-evaluation.html
```

选择 **for Windows** 版本就行，然后下载好了安装，中途应该没有什么问题，除了最后会遇到一个激活密钥。作为经济能力有限的学生，暂时买不起正版的话，出于学习和科研考虑，在网上随便搜一个密钥来用就行了。

下一步是选择 Linux 的发行版本( distribution )。 Linux 有许多的发行版，由于教材的缘故我这里使用的是 **CentOS 7.3** ，不过 Linux 发行版的命令大同小异，需要使用其他的发行版的工具时也有可选择的解决方法(比如在 Docker 中使用 Ubantu 的镜像)，所以发行版的选择其实并不是什么大问题。在网上找到 **CentOS 7.3** 的镜像并下载。

最后就是在 Vmware 里创建虚拟机。这个的详细过程我忘了……但是整个创建过程看起来很智能，除了不记得要避开哪些小坑之外应该都还好……也许吧。

<hr />

### 一些简单的命令

输入的命令通常由三部分组成：命令、选项、参数。

### **date** 命令

**date** 命令用于显示当前日期和时间。

```
$ date
```
这会以默认格式输出日期和时间。

使用加号( + )开头的参数可以指定 date 命令输出的格式。

```
$ date +%R
$ date +%r
$ date +%x
```

>Tips: <br> 不知道该如何使用命令的选项和参数时，可以使用 **--help** 选项查询。

### **file** 命令

**file** 命令用于扫描文件内容的开头并输出文件类型。

```
$ file <filename>
```

**head** 命令和 **tail** 命令用于显示文件的开头和结尾部分，默认情况下显示10行。

```
$ head <filename>
$ tail <filename>
```

[-n] 选项可以指定输出不同的行数。

```
$ head -n <number> <filename>
$ tail -n <number> <filename>
```

### **wc** 命令

**wc** 命令用于计算文件中的行、字和字符的数量。[-l] 选项用于仅显示行数。[-w] 选项用于仅显示字数。[-c] 选项用于仅显示字符数。

```
$ wc <filename>
$ wc -l <filename>
$ wc -w <filename>
$ wc -c <filename>
```

>Tips: <br> 使用 **↑** 箭头可以显示上一命令。使用 **Esc + .** 可以快速重新利用上一命令中的参数。

### **history** 命令

**history** 命令用于显示使用过的命令的历史记录。

```
$ history
```

### **ifconfig** 命令

**ifcongfig** 命令用于显示当前网络地址。

```
$ ifconfig
```

>Tips: <br> 使用 **Tab** 按键可以在输入了足够的内容的情况下补全命令。如果输入的内容较少、补全后有多种可能，那么将会输出可供选择的命令列表。

<hr />

### 编辑命令行

使用方向键可以在当前输入的命令内移动， bash 提供了更为强大的编辑命令。

**Ctrl + a** 跳到命令行开头 <br>
**Ctrl + e** 跳到命令行末尾 <br>
**Ctrl + u** 将光标到命令行开头的内容清除 <br>
**Ctrl + k** 将光标到命令行结尾的内容清除 <br>
**Ctrl + ←** 跳到命令行中前一字的开头 <br>
**Ctrl + →** 跳到命令行中下一字的开头 <br>

<hr />

### 个性化配置

虚拟机的一些默认配置(比如说时区和语言)可能不太合适，可以通过以下方式修改。

### 更换时区

```
$ cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

### 修改默认语言

这里将会使用到 **vi** 命令。关于 **vi** 命令是之后的内容了，它可以理解为一个文本编辑器。**vi** 和 **vim** 命令有很多强大的用法，现在只介绍最简单的，用来修改默认语言。

首先打开配置语言的文件。

```
$ vi /etc/locale.conf
```

按 **i** 键进入插入模式。然后修改其中关于语言的UTF-8编码。

```
LANG="zh_CN.UTF-8"
```

接下来按 **Esc** 退出插入模式，再按 **Shift + zz** 保存退出。

然后可能要重启虚拟机使配置生效。

<hr />

### 参考资料

[1] 红帽系统管理