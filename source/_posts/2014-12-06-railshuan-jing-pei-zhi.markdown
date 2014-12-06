---
layout: post
title: "rails环境配置"
date: 2014-12-06 17:33:48 +0800
comments: true
categories: 
---

<!-- # Rails

![Rails icon](http://upload.wikimedia.org/wikipedia/commons/9/9c/Ruby_on_Rails_logo.jpg) -->

##Rails安装

###Gem

RubyGems（简称 gems）是一个用于对 Ruby组件进行打包的 Ruby 打包系统。 它提供一个分发 Ruby 程序和库的标准格式，还提供一个管理程序包安装的工具(`gem`)。Rails也是一个Ruby写的RubyGem。

Ruby从1.9版本开始内建RubyGems。或者选择下载安装（[下载地址](http://rubygems.org/)）。

查看版本

```
$ gem -v
```

更新版本

```
$ gem update --system
```

查看已安装的gems

```
$ gem list
```

查看remote端的gems

```
$ gem list -r
```

安装gems

```
$ gem install cocoapods
```
安装特定版本的gems

```
$ gem install -v 0.33.1 cocoapods
```

升级gems

```
$ gem update cocoapods
```

升级所有已安装gems

```
$ gem update
```

卸载gems
 
```
$ gem uninstall cocoapods
```
gems环境信息

```
$ gem environment
```

查看gems源

```
$ gem sources -l
```

添加gems源

```
$ gem sources -a https://ruby.taobao.org/
```
移除gems源

```
$ gem sources --remove https://ruby.taobao.org/
```

####RVM管理多个gemset

rvm可以在某版本ruby下建立多个gemset独立空间来用来安装不同套件组合

```
$ rvm gemset create set1
```

```
$ rvm gemset create set2
```
查看已建立gemset列表

```
$ rvm gemset list
```

设置某个gemset为当前gems空间

```
$ rvm gemset user set1
```

清空某个gemset

```
$ rvm gemset empty set1
```
删除某个gemset

```
$ rvm gemset delete set1
```

###gem安装rails

安装rails

```
$ gem install rails
```

不需要文档的安装方式

```
$ gem install rails --no-ri --no-rdoc
```

rails版本

```
$ rails -v
```

##rails使用

[rails命令行](http://guides.ruby-china.org/command_line.html)


####官方网站
<http://rubyonrails.org/>

####Github
<https://github.com/rails/rails>

####参考资料
* <http://guides.ruby-china.org/command_line.html>
* <https://ruby-china.org/wiki/install_ruby_guide>
