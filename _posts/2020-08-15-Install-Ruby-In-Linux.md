---
layout: post
title: 在Linux中安装Ruby
date: 2020-08-02
categories: Ruby
tag: Ruby
---

> Write in front: <br> 本文可能包含大量我也不知道有没有用的命令。

### 目录

```
在Linux中安装Ruby
 |
 |--目录
 |--为什么要在Linux中使用Ruby
 |--下载Ruby源代码
 |--安装过程
 |--参考资料
```

<hr />

### 为什么要在Linux中使用Ruby

众所周知，我不懂编程，所以自然是不会去评价编程语言的好坏。学习 Ruby 的原因很简单，王老师发的书实在太多了，以至于可以（足够我）学习很长一段时间，所以既然学习资源这么充裕，当然是要学习一个。

事实上 Ruby 在 Windows 环境下也可以很方便地安装和使用（也许），但是之前上课时的一个小插曲实在是让我非常糟心————一个名为 tk 的库。

假如我没理解错的话（理解错了再回来改），这个库与 Ruby 程序的可视化有关，也就是在编写那个微型计算器的课程作业时必须使用到的一个库。然而这个库似乎在安装 Ruby 时并没有附带，反而还需要一些其他的集成开发环境。试图弄出可以顺利调用 tk 库的开发环境花了我几个月时间，最后还是失败了（好菜啊，好菜啊）。

之所以要花这么久，最后还是失败，究其原因是能借鉴的经验太少。有些电脑在安装 Ruby 结束之后就可以顺利调用 tk 库，而有些人则需要经过更多的过程，这似乎与每个人使用 Windows 系统的习惯有关，在一些博客中，我发现了有关默认路径的一些奇怪记录。

最后我只好选择尝试在 Linux 系统下安装 Ruby ，因为在 Linux 中软件包的安装似乎非常的智能，不需要太多（就几乎没有）人为选择的部分。

所以这篇文章也只是我在 Linux 下安装 Ruby 的一个尝试，其中可能使用了多余的命令，但是应该没有什么不利影响。

<hr />

### 下载Ruby源代码

可能有些 Linux 的发行版已经默认安装了 Ruby ，所以首先还是查看一下自己的虚拟机里是不是已经安装了。

```
$ ruby -v
```

假如显示的版本低于 2.3.0 ，最好选择重新安装。

不过 CentOS 里应该是没有默认安装 Ruby 的，所以我就没有经历重新安装这一步。

下载 Ruby 的源代码有两种方式。

第一种是通过 `wget` 命令直接下载。

```
$ wget ftp://ftp.ruby-lang.org/pub/ruby/ruby-2.7.1.tar.gz
```

但是这个网站应该是要挂 VPN 才能连上，对于一些缺乏条件的人可能不太方便。

第二种方法是手动下载源代码包。

在[这个网站](https://www.ruby-lang.org/en/downloads/)选择一个稳定的 Ruby 版本下载，我选择的是 2.7.1 版本。

```
https://www.ruby-lang.org/en/downloads/
```

下载好之后打开 XShell ，从文件夹中拖动源代码包到 XShell 里，通过 XShell 把源代码包发送到虚拟机里。

<hr />

### 安装过程

如果没有切换目录的话，那么这个源代码包应该是被发送到了根目录下。

```
$ ls
```

可以在其中看到被红色高亮显示的源代码包。

将源代码包解压。

```
$ tar zxvf ruby-2.7.1.tar.gz
```

解压完成后，再次使用 `ls` 命令可以在根目录下看到一个名为 `ruby-2.7.1` 的新目录。使用 `cd` 命令进入这一目录，然后按顺序执行命令。

```
$ cd ruby-2.7.1
$ ./configure
$ make
$ make test
$ make install
```

这时再次检查 Ruby 的版本，确认安装成功。

```
$ ruby -v
```

同时还可以查看一下 Ruby 附带的 gem 工具。

```
$ gem -v
```

`gem` 命令将会用于下载和 Ruby 有关的各种软件包。但由于某些众所周知的原因，在使用 `gem` 之前我们要进行换源处理。

换源，并删除源地址。

```
$ gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/ 
$ gem sources -l
```

安装 `ruby_dev` 软件包。

```
$ gem install ruby_dev
```

安装 TCL 环境。

```
$ yum install tcl-devel tk-devel
```

最后安装 `tk` 软件包。

```
$ gem install tk
```

这样应该可以顺利完成安装了。不过有一说一，能不能顺利使用还要看之后的效果。

<hr />

### 参考资料

[1] 红帽系统管理 <br>
[2] Ruby 基础教程