title: "awk的使用"
date: 2015-12-24 09:42:03
categories: Linux
tags: Linux
---

# awk使用案例

	1.以每一行为输入，指定分隔符，输出指定域
		tail -n 10 test.txt | awk -F ' '  '{print $1",\t"$2}'（以空格为分隔符，输出第一个域与第二个域并以,和tab连接）

	2.在输出的首尾添加内容
	cat /etc/passwd |awk  -F ':'  'BEGIN {print "name,shell"}  {print $1","$7} END {print "blue,/bin/nosh"}'（显示/etc/passwd的账户和账户对应的shell,而账户与shell之间以逗号分割,而且在所有行添加列名name,shell,在最后一行添加"blue,/bin/nosh"）

	3.搜索
	awk -F ':' '/hello/{print $1}' test.txt（搜索test.txt中的包含hello的行,并以':'为分隔符，输出第一个域）

	4.awk的环境变量
	awk  -F ':'  '{print "filename:" FILENAME ",linenumber:" NR ",columns:" NF ",linecontent:"$0}' /etc/passwd（统计/etc/passwd:文件名，每行的行号，每行的列数，对应的完整行内容:）
	awk  -F ':'  '{printf("filename:%10s,linenumber:%s,columns:%s,linecontent:%s\n",FILENAME,NR,NF,$0)}' /etc/passwd

	5.awk编程
	awk '{count++;print $0;} END{print "user count is ", count}' /etc/passwd（统计用户总数）
	ls -l | awk 'BEGIN {size=0} {size=size+$5} END {print "size is "size}'（统计文件夹大小）

# awk参数说明

	用法: awk [POSIX 或 GNU 风格选项] -f 脚本文件 [--] 文件 ...
    用法: awk [POSIX 或 GNU 风格选项] [--] '程序' 文件 ...
    POSIX 选项:     		GNU 长选项:
    	-f 脚本文件		--file=脚本文件
    	-F fs			--field-separator=fs
    	-v var=val		--assign=var=val
    	-m[fr] val
    	-O			--optimize
    	-W compat		--compat
    	-W copyleft		--copyleft
    	-W copyright		--copyright
    	-W dump-variables[=file]	--dump-variables[=file]
    	-W exec=file		--exec=file
    	-W gen-po		--gen-po
    	-W help			--help
    	-W lint[=fatal]		--lint[=fatal]
    	-W lint-old		--lint-old
    	-W non-decimal-data	--non-decimal-data
    	-W profile[=file]	--profile[=file]
    	-W posix		--posix
    	-W re-interval		--re-interval
    	-W source=program-text	--source=program-text
    	-W traditional		--traditional
    	-W usage		--usage
    	-W use-lc-numeric	--use-lc-numeric
    	-W version		--version

    awk的环境变量
        ARGC               命令行参数个数
        ARGV               命令行参数排列
        ENVIRON            支持队列中系统环境变量的使用
        FILENAME           awk浏览的文件名
        FNR                浏览文件的记录数
        FS                 设置输入域分隔符，等价于命令行 -F选项
        NF                 浏览记录的域的个数
        NR                 已读的记录数
        OFS                输出域分隔符
        ORS                输出记录分隔符
        RS                 控制记录分隔符