title: "shell常识"
date: 2015-12-22 09:53:00
categories: Linux
tags: Linux
---

# path环境变量
	环境变量是一个以‘:’分割的目录列表，可以在列表指定的目录下找到所要执行的命令
	echo $PATH（查看目前执行shell寻找的目录）
	:（表示查找的优先级）
    PATH=$PATH:$HOME/bin（将家目录下的bin添加到环境变量）
    echo $PATH（查看环境变量）

	环境变量永久生效的方式：
	1.vim /etc/profile
	2.export PATH=/usr/local/bin;source /etc/profile

# ls -l
	‘-’表示参数是可有可无的

# #! /bin/sh 的含义
	告知系统需要使用/bin/sh的shell来执行脚本，类似的还有很多shell比如#! /bin/awk ;#! /bin/csh

# ';'和'&'的作用
	‘;’用来分隔同一行里的多个命令
	‘&’如果是在命令的末尾shell会在后台执行该命令

# 'set -x'与'set +x'
	关闭和打开追踪功能
