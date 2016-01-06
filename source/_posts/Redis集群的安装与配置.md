title: "Redis集群的安装与配置"
date: 2015-12-03 18:23:49
categories: Redis
tags: Redis
---

## Redis集群安装
* `wget 'http://download.redis.io/releases/redis-3.0.3.tar.gz'`(*下载redis-3.0.tar.gz*)
* `tar zxvf redis-3.0.tar.gz`(*解压安装包*)
* `cd redis-3.0.0-beta3`（*进入解压后的文件夹*）
* `yum install tcl`
* `make`
* `cp redis.conf redis.6380.conf`
* `vim redis.6380.conf`
* `src/redis-server redis.6380.conf &`
* `ps aux | grep redis`
* `src/redis-cli -h 172.16.9.111 -p 6379`
* `yum install ruby`
* `yum install rubygems`
* `gem install redis`
* `src/redis-trib.rb create --replicas 1 172.16.9.111:6380 172.16.9.111:6381 172.16.9.111:6382 172.16.9.104:6380 172.16.9.104:6381 172.16.9.104:6382`
* `src/redis-cli -p 6380`
* `src/redis-cli -c -p 6380`