title: "Innodb存储引擎-1.1"
date: 2015-05-19 00:58:56
categories: Mysql
tags: innodb_storage_engine
---

## 数据库
物理操作系统文件或其他形式文件类型的集合(*可能是存放在内存中的文件*)。

## 数据库文件

* .frm文件：与表相关的元数据（meta）信息都存放在“.frm”文件中，包括表结构的定义信息等。不论是什么存储引擎，每一個表都会有一个以表名命名的“.frm”文件。所有的“.frm”文件都存放在所属数据库的文件夾下面。 
* MYD：是MyISAM 存储引擎专用，存放MyISAM 表的数据。每一個MyISAM 表都会有一個“.MYD”文件与之对应，存放在所属数据库的文件夾下，和“.frm”文件在一起。 
* MYI:是MyISAM存储引擎的，主要存放MyISAM表的索引相关信息。对于MyISAM存储來說，可以被cache 的內容主要就是來源于“.MYI”文件中。每一个MyISAM表对应一个“.MYI”文件，存放于位置和“.frm”以及“.MYD”一样。 
* ibd，ibdata：是存放Innodb 数据的文件，之所以有两种文件來存放Innodb 的数据（包括索引），是因为Innodb 的数据存储方式能够通过配置來决定是使用共享表空間存放存储数据，还是独享表空间存放存储数据。独享表空间存储方式使用“.ibd”文件來存放數据，且每个表一个“.ibd”文件，文件存放在和MyISAM数据相同的位置。 如果选用共享存储表空間來存放数据，则会使用ibdata 文件來存放，所有表共同使用一个（或者多个，可自行配置）ibdata 文件。

## 实例
* **Mysql被设计成的是一个单进程多线程的数据库，因此Mysql数据库实例在系统上的表现就是一个进程**
* Mysql数据库由后台线程以及一个共享内存区组成，共享内存可以被运行的后台线程所共享。*数据库实例才是真正用于操作数据库文件的*

## Mysql在linux系统中的使用命令

Mysql启动命令，&代表在后台启动
	`./mysqld_safe&`
	
ps 查看系统进行命令，这里可以看到Mysql在系统上的表现是一个进程（*此时的进程号是1197*）

`ps aux | grep mysql`

执行结果为

	root      1063  0.0  0.0 108300   372 ?        S    Apr24   0:00 /bin/sh /usr/bin/mysqld_safe --datadir=/var/lib/mysql --pid-file=/var/lib/mysql/localhost.localdomain.pid
	
    mysql     1197  0.0 13.9 1341208 65276 ?       Sl   Apr24   9:27 /usr/sbin/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=/usr/lib64/mysql/plugin --user=mysql --log-error=/var/lib/mysql/localhost.localdomain.err --pid-file=/var/lib/mysql/localhost.localdomain.pid

	
`ps -ef | grep mysqld`

执行结果为
	
	root      1063     1  0 Apr24 ?        00:00:00 /bin/sh /usr/bin/mysqld_safe --datadir=/var/lib/mysql --pid-file=/var/lib/mysql/localhost.localdomain.pid
    
    mysql     1197  1063  0 Apr24 ?        00:09:27 /usr/sbin/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=/usr/lib64/mysql/plugin --user=mysql --log-error=/var/lib/mysql/localhost.localdomain.err --pid-file=/var/lib/mysql/localhost.localdomain.pid
	
`mysql --help | grep my.cnf`

执行结果为（*表示如果没有指定Mysql*配置文件，Mysql会从这些位置去读取配置文件，如果多个地方有统一参数的配置，则Mysql以最后一个文件的配置参数为准，一般配置文件在/etc/my.cnf*）

	order of preference, my.cnf, $MYSQL_TCP_PORT,/etc/my.cnf /etc/mysql/my.cnf /usr/etc/my.cnf ~/.my.cnf
	
ps命令执行后的结果中可以看到datadir的参数，该参数表示数据库所在位置。也可以在Mysql终端使用

`SHOW VARIABLES LIKE 'datadir'\G`

	*************************** 1. row ***************************
	Variable_name: datadir
           Value: /var/lib/mysql/   
	1 row in set (0.00 sec)

接着在Mysql终端运行下面下面命令，可以看出data其实就是一个数据目录（*该目录的用户和权限必须得到保障只有Mysql用户和组可以访问，通常权限是mysql:mysql*）
`system ls -lh /var/lib/mysql/` 
	
	总用量 173M
	-rw-rw----. 1 mysql mysql   56 3月  24 16:08 auto.cnf
	drwx------. 2 mysql mysql 4.0K 5月  18 14:43 beebank
	-rw-rw----. 1 mysql mysql  76M 5月  18 20:01 ibdata1
	-rw-rw----. 1 mysql mysql  48M 5月  18 20:01 ib_logfile0
	-rw-rw----. 1 mysql mysql  48M 3月  24 16:04 ib_logfile1
	-rw-r-----. 1 mysql root  520K 4月  25 02:22 localhost.localdomain.err
	-rw-rw----. 1 mysql mysql    5 4月  25 02:22 localhost.localdomain.pid
	drwx--x--x. 2 mysql mysql 4.0K 3月  24 16:04 mysql
	srwxrwxrwx. 1 mysql mysql    0 4月  25 02:22 mysql.sock
	drwx------. 2 mysql mysql 4.0K 3月  24 16:04 performance_schema
	-rw-r--r--. 1 root  root   125 3月  24 16:04 RPM_UPGRADE_HISTORY
	-rw-r--r--. 1 mysql mysql  125 3月  24 16:04 RPM_UPGRADE_MARKER-LAST
	drwxr-xr-x. 2 mysql mysql 4.0K 3月  24 16:04 test
	drwx------. 2 mysql mysql 4.0K 5月  11 17:24 test_checklist_table


		