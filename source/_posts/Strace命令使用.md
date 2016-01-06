title: "Strace命令使用"
date: 2015-11-04 00:00:59
categories: Linux
tags: Linux
---
## 主要功能
* 会记录和解析命令进程的所有系统调用以及这个进程所接收到的所有的信号值，每一行都是一条系统调用，等号左边是系统调用的函数名及其参数，右边是该调用的返回值

## 我的应用场景
* `strace mysql`（*找不到配置文件的时候，可以使用它查看它打开文件的记录，了解到配置文件的路径.*）
* `ps aux | grep php-fpm`（*找出php-fpm的启动进程*） `strace -p 26999`（*26999为非root进程id*）（*在进行程序调试的时候不知道发生了什么错误，错误日志写在什么位置，或者程序在哪个未知位置执行终止了，都可以进行查看。*）
* `strace -o strace.txt -T -tt -e trace=all -p 3306`（*跟踪3306进程的所有系统调用（-e trace=all），并统计系统调用的花费时间，以及开始时间（并以可视化的时分秒格式显示），最后将记录结果存在strace.txt文件里面，当中断显示不全strace信息的时候*）

## 参数说明
		 -c			#统计每一系统调用的所执行的时间,次数和出错的次数等.
		 -C			#Like -c but also print regular output while processes are running
		 -d			#输出strace自身的关于标准错误的调试信息.
		 -f			#跟踪由fork调用所产生的子进程.
		 -ff			#如果提供-o filename,则所有进程的跟踪结果输出到相应的filename.pid中,pid是各进程的进程号. 此与-c不兼容
		 -h			#输出简要的帮助信息.
		 -i			#打印系统调用时候的入口指针.
		 -q			#禁止输出关于脱离的消息.
		 -r			#进入每一个系统调用时打印一个相对时间戳，一个系统调用的开始和下一个系统调用接替时，两者之间的时间.
		 -t			#在输出中的每一行前加上时间信息.
		 -tt			#时间信息精确到微妙
		 -ttt			#时间信息精确到微妙，而且时间表示为unix时间戳
		 -T			#显示每一调用所耗的时间.
		 -v			#Print unabbreviated versions of environment, stat, termios, etc.  calls
		 -V			#输出strace的版本信息.
		 -x			#打印所有非ascii字符串以十六进制字符串格式显示。
		 -xx			#所有字符串以十六进制形式输出.
		 -a column		#设置返回值的输出位置.默认 为40.
		 -e expr		#指定一个表达式,用来控制如何跟踪.格式如下:
	    [qualifier=][!]value1[,value2]...
	    qualifier只能是 trace,abbrev,verbose,raw,signal,read,write其中之一.value是用来限定的符号或数字.默认的 qualifier是 trace.感叹号是否定符号.例如: -eopen等价于 -e trace=open,表示只跟踪open调用.而-etrace!=open表示跟踪除了open以外的其他调用.有两个特殊的符号 all 和 none. 注意有些shell使用!来执行历史记录里的命令,所以要使用反斜杠
		 -e trace=set		#只跟踪指定的系统调用.例如:-e trace=open,close,rean,write表示只跟踪这四个系统调用.默认的为set=all.
		 -e trace=file		#只跟踪有关文件操作的系统调用.
		 -e trace=process	#只跟踪有关进程控制的系统调用.
		 -e trace=network	#跟踪与网络有关的所有系统调用.
		 -e strace=signal	#跟踪所有与系统信号有关的 系统调用
		 -e trace=ipc		#跟踪所有与进程通讯有关的系统调用
		 -e abbrev=set		#设定 strace输出的系统调用的结果集.-v等与abbrev=none.默认为abbrev=all.
		 -e raw=set		#将指 定的系统调用的参数以十六进制显示.
		 -e signal=set		#指定跟踪的系统信号.默认为all.如 signal=!SIGIO(或者signal=!io),表示不跟踪SIGIO信号.
		 -e read=set		#输出从指定文件中读出的数据.例如: -e read=3,5
		 -e write=set		#输出写入到指定文件中的数据.
		 -o filename		#将strace的输出写入文件filename
		 -O overhead		#设置追踪系统的总开销（microseconds）
		 -p pid			#跟踪指定的进程pid.
		 -s strsize		#指定输出的字符串的最大长度.默认为32.文件名一直全部输出.
		 -S sortby		#-c选项的输出以规定的标准显示为直方图
		 -u username		#以username 的UID和GID执行被跟踪的命令
