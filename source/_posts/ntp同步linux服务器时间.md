title: "ntp同步linux服务器时间"
date: 2015-05-21 01:42:31
categories: Other
tags: Other
---
# linux时区及服务器时间调整
* 首先使用`date`查看服务器时间和时区运行结果为`2015年 5月21日 星期四 01时43分23秒 CST`
* 如果发现时区不对请进行时区更改（例子为更改为上海时区）
		vim /etc/sysconfig/clock:
		ZONE="Asia/Shanghai"
* 删除之前的时区，使用上海时区	
		rm /etc/localtime
		ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
* 同步时间
		ntpdate -u asia.pool.ntp.org