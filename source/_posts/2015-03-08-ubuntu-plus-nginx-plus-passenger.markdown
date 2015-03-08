---
layout: post
title: "ubuntu+nginx+passenger"
date: 2015-03-08 12:15:08 +0800
comments: true
categories: 
---

##Ubuntu
通过`chef-solo`配置好某个Ubuntu server系统，然后通过`Vagrant`启动并登陆该server系统。升级该系统软件，并安装一些组件。

####系统升级

```
$ sudo apt-get update
```
####安装组件

```
$ sudo apt-get install build-essential zlib1g-dev libssl-dev libreadline-dev libyaml-dev libcurl4-openssl-dev curl git-core python-software-properties libsqlite3-0 libsqlite3-dev sqlite3
```

####安装PostgreSQL

```
$ sudo apt-get install postgresql postgresql-contrib libpq-dev
```

####安装ruby

```
$ \curl -L https://get.rvm.io | bash -s stable --ruby
```

```
$ rvm install 2.1.2
$ rvm 2.1.2 --default
```
####安装rails

```
$ gem install rails
```

##Nginx+Passenger

####安装passenger

```
$ gem install passenger
```

#####安装nginx

```
$ rvmsudo passenger-install-nginx-module
```

####安装nginx脚本

```
$ gpg --keyserver keyserver.ubuntu.com --recv-keys 561F9B9CAC40B2F7
```

```
$ gpg --armor --export 561F9B9CAC40B2F7 | sudo apt-key add -
```

```
$ sudo apt-get install apt-transport-https
```

```
$ sudo sh -c "echo 'deb https://oss-binaries.phusionpassenger.com/apt/passenger trusty main' >> /etc/apt/sources.list.d/passenger.list"
```

```
$ sudo chown root: /etc/apt/sources.list.d/passenger.list
```

```
$ sudo chmod 600 /etc/apt/sources.list.d/passenger.list
```

```
$ sudo apt-get update
```

```
$ sudo apt-get install nginx-full passenger
```

`/etc/nginx/sites-enabled/default`

```
$ sudo vi /etc/nginx/sites-enabled/default
```
	server {
    	listen 80 default;
    	server_name vicspdemo.com; # 这里填写你真实域名
    	root /home/vagrant/apps/spdemo/current/public;# 这里填写你的web启动位置
    	passenger_enabled on;
	}
	
`/etc/nginx/nginx.conf`

```
$ sudo vi /etc/nginx/nginx.conf
```
	##
    # Phusion Passenger config
    ##
    # Uncomment it if you installed passenger or passenger-enterprise
    ##
    passenger_root /usr/lib/ruby/vendor_ruby/phusion_passenger/locations.ini;
    passenger_ruby /home/vagrant/.rvm/wrappers/default/ruby;
    # passenger_root /usr/lib/ruby/vendor_ruby/phusion_passenger/locations.ini;
    # passenger_ruby /usr/bin/ruby;


####参考资料
* <https://ruby-china.org/topics/12967>
* <https://ruby-china.org/wiki/mac-nginx-passenger-rails>
* <https://gorails.com/deploy/ubuntu/14.04>