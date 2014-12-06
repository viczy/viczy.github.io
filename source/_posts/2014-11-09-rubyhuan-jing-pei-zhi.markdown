---
layout: post
title: "Ruby环境配置"
date: 2014-11-09 13:21:34 +0800
comments: true
categories: 
---
<!-- # ruby

![Ruby icon](http://learn-rails.com/images/ruby.png) -->

## ruby安装

ruby安装方式有下面几种

* 原始码编译安装，下载相应版本的安装包安装（[下载地址](https://www.ruby-lang.org/zh_cn/downloads/)）
* 第三方工具安装
* 少数的套件管理工具支持ruby

考虑到多版本的管理，这里使用第二种方式（第三方工具）安装。第三方工具安装有RVM和Rbenv可选

###RVM

rvm可以通过brew安装（[brew的介绍与安装](http://brew.sh/index_zh-tw.html)），在安装前需要先安装装git版本控制

```
$ brew install git
$ brew install readline
$ brew link readline
```
然后安装rvm

```
$ \curl -L https://get.rvm.io | bash -s stable --ruby
```
查看rvm的版本，来验证rvm是否已安装

```
$ rvm -v
```
当你的rvm不是最新版本，可以升级你的rvm版本

```
$ rvm get stable
```

接下来就可以通过rvm来安装ruby，下面将安装版本2.1.2的ruby，并将2.1.2版本作为当前预设版本

```
$ rvm install 2.1.2
$ rvm 2.1.2 --default
```
查看ruby版本号，可以确认当前预设ruby的版本

```
$ ruby -v
```
如果还需要安装其他的版本的ruby，可以先查看可以安装的ruby版本，并选择你需要安装的版本

```
$ rvm list known
```
当安装了多个版本ruby后，查看已经安装了ruby

```
$ rvm list
```
这时如果你希望改变ruby的预设版本可以通过`rvm xxx -default` 来更新预设版本，这样的话每次打开个terminal窗口都会使用该版本的ruby。除了预设版本之外，如果你只在当前的terminal窗口使用某版本的ruby

```
$ rvm use 1.9.3
```

切换到系统内建的ruby版本

```
$ rvm system
```

###rbenv

* [rbenv](https://github.com/sstephenson/rbenv)
* [rbenv使用](https://ruby-china.org/wiki/rbenv-guide)


## ruby使用

###交互式运行Ruby
要以交互式的运行ruby，只需要输入

```
$ ruby
```
然后输入你的ruby程序，以文件结束符结束（Ctrl+D）。

不多这样的方式操作比较麻烦，irb相对而言会是个更好地选择，irb是一个Ruby Shell。

```
$ irb
```
###运行Ruby程序文件

```
$ ruby rubydemo.rb
```

###Ruby查看文档

```
$ ri puts
```

####官方网站
* 中文<https://www.ruby-lang.org/zh_tw/>
* 英文<https://www.ruby-lang.org/en/>

####Github
<https://github.com/ruby/ruby>

