title: "siege压测工具的安装与使用"
date: 2015-12-17 14:18:08
categories: Other
tags: Other
---

# siege的安装
	wget http://soft.vpser.net/test/siege/siege-2.67.tar.gz（国内的一个镜像站地址）
	tar -zxvf siege-2.67.tar.gz
	cd siege-2.67
	./configure && make && make install
	/usr/local/bin/siege --help

[官网的下载地址](http://download.joedog.org/siege/siege-latest.tar.gz)（我下载的时候连接超时）
    [siege，github地址](https://github.com/JoeDog/siege)

# siege的使用
	50个用户（每次并发量，注意不是每秒并发量） 重复100次 共产生 50 * 100 = 5000个请求
    /usr/local/bin/siege -c 50 -r 100  hostname/path

    50个用户 重复100次 发送GET参数
    /usr/local/bin/siege -c 50 -r 100  hostname/path?name=zhangsan

    50个用户 重复100次 发送POST参数 (注意引号)
    /usr/local/bin/siege -c 50 -r 100  "hostname/path POST name=zhangsan"

    50个用户 重复100次 发送POST参数(从文件中读取)
    /usr/local/bin/siege -c 50 -r 100  "hostname/path POST < /tmp/post.xml"

	100个用户 重复100次 发送cookie参数
	/usr/local/bin/siege -c 100 -r 100 -H "Cookie:key=value" "hostname/path"

	压测多个地址
	siege -c 200 -r 10 -f url.txt
	url.txt的内容是:
		hostname/path
		hostname/path
		hostname/path

# siege命令结果分析
	Transactions:		            100 hits （完成100个请求)
    Availability:		            100.00 %（100%的成功率_）
    Elapsed time:		            10.97 secs（总共使用时间_）
    Data transferred:	            0.54 MB（总共传输数据_）
    Response time:		            0.17 secs（响应时间）
    Transaction rate:	            9.12 trans/sec（平均每秒完成的处理）
    Throughput:		                0.05 MB/sec（平均每秒传送的数据）
    Concurrency:		            1.58（实际最高并发数）
    Successful transactions:        100（成功处理次数）
    Failed transactions:	        0（失败处理次数）
    Longest transaction:	        3.09（每次传输花费的最长时间）
    Shortest transaction:	        0.03（每次传输花费的最短时间）

# siege参数说明
	Usage: siege [options]
           siege [options] URL
           siege -g URL
    Options:
      -V, --version           （版本信息）
      -h, --help              （帮助信息）
      -C, --config            （显示配置）
      -v, --verbose           （运行时能看到详细的运行信息）
      -g, --get               （显示http头信息，用户debug）
      -c, --concurrent=NUM    （一次请求的并发数目）
      -i, --internet          （随机模拟用户点击）
      -b, --benchmark         （基准测试，设置这个参数默认延迟时间为0）
      -t, --time=NUMm         （设置测试的时间比如--time=1H, 测试时间一个小时）
      -r, --reps=NUM          （压测次数）
      -f, --file=FILE         （指定任务文件）
      -R, --rc=FILE           （修改siegerc的文件位置，覆盖SIEGERC的环境变量）
      -l, --log               （运行完之后的结果log位置）
      -m, --mark="text"       （利用分隔符标记文件）
      -d, --delay=NUM         （每次压测延迟的时间）
      -H, --header="text"     （添加一个header头请求消息）
      -A, --user-agent="text" （设置User-Agent）
	  -T --content-type       （指定http请求中的content-type字段内容）