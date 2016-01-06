title: "ab压测工具的安装与使用"
date: 2015-12-17 10:03:33
categories: Other
tags: Other
---

## 安装
	yum install httpd-tools

## 使用
	ab -kc 10 -n 10 http://hostname/path (*命令表示连接100，并发请求数是100次*)

## 命令执行结果分析
	Server Software:
	Server Hostname:        hostname(*服务器域名*)
	Server Port:            443(*服务器端口*)
	SSL/TLS Protocol:       TLSv1/SSLv3,ECDHE-RSA-AES128-GCM-SHA256,2048,128

	Document Path:          /path(*测试接口地址*)
	Document Length:        14904 bytes(*测试数据大小*)

	Concurrency Level:      10(*并发数*)
	Time taken for tests:   0.403 seconds(*整个测试持续时间*)
	Complete requests:      10(*完成的请求数量*)
	Failed requests:        0(*失败的请求*)
	Write errors:           0(*请求写入失败的次数*)
	Keep-Alive requests:    0(*保持联机连接的请求数量。只有在命令行中使用-k，才能看到该属性值*)
	Total transferred:      151120 bytes(*整个场景中的网络传输量*)
	HTML transferred:       149040 bytes(*整个场景中的HTML内容传输量*)
	`Requests per second:    24.84 [#/sec] (mean)(*表示当前测试的服务器每秒可以处理24.84个静态html的请求事务，后面的mean表示平均。这个数值表示当前机器的整体性能，值越大越好*)`
	`Time per request:       402.511 [ms] (mean)(*单个并发的延迟时间，后面的mean表示平均。隔离开当前并发，单独完成一个请求需要的平均时间*)`
	`Time per request:       40.251 [ms] (mean, across all concurrent requests)(*即上面的时间（Time per request）除以并发数 ,平均每个并发请求处理的时间*)`
	`Transfer rate:          366.64 [Kbytes/sec] received(*平均每秒网络上的流量，可以帮助排除是否存在网络流量过大导致响应时间延长的问题，也就是这些请求在单位时间从服务器获取的数据长度*)`

	Connection Times (ms)
	              min  mean[+/-sd] median   max
	Connect:       33   46  14.6     41      72
	Processing:    16  113 119.2     27     268
	Waiting:       10   37  79.1     12     262
	Total:         49  159 121.5     99     340

	Percentage of the requests served within a certain time (ms)
	  50%     99
	  66%    268
	  75%    282
	  80%    299
	  90%    340
	  95%    340
	  98%    340
	  99%    340
	 100%    340 (longest request)

## ab命令参数
	Usage:
	  ab [options] [http[s]://]hostname[:port]/path
    Options are:
	  -n requests     (*总的请求数目*)
      -c concurrency  (*一次请求并发数*)
      -t timelimit    (*测试进行的最大秒数*)
      -b windowsize   (*tcp连接的最大内存使用*)
      -p postfile     (*post的数据*)
      -u putfile      (*put的数据*)
      -T content-type (*header的类型，比如'application/x-www-form-urlencoded'默认为Default is 'text/plain'*)
      -v verbosity    (*设置显示信息的详细程度 – 4或更大值会显示头信息， 3或更大值可以显示响应代码(404, 200等), 2或更大值可以显示警告和其他信息*)
      -w              (*将结果用html的table打印出来，默认它是白色背景的两列宽度的一张表*)
      -i              (*执行HEAD请求，而不是GET*)
      -C attribute    (*添加一个cookie信息*)Add cookie, eg. 'Apache=1234. (repeatable)
      -H attribute    (*添加head属性例如eg. 'Accept-Encoding: gzip'*)
      -A attribute    (*Add Basic WWW Authentication, the attributes are a colon separated username and password*)
      -P attribute    (*Add Basic Proxy Authentication, the attributes are a colon separated username and password*)
      -X proxy:port   (*使用代理的端口*)
      -V              (*显示版本信息并退出*)
      -k              (*使用http的KeepAlive属性*)
      -d              (*Do not show percentiles served table*)
      -S              (*Do not show confidence estimators and warnings*)
      -g filename     (*Output collected data to gnuplot format file*)
      -e filename     (*Output CSV file with percentages served*)
      -r              (*忽略socket错误*)
      -h              (*Display usage information (this message)*)
      -Z ciphersuite  (*Specify SSL/TLS cipher suite (See openssl ciphers)*)
      -f protocol     (*特殊的协议例如SSL2, SSL3, TLS1, or ALL*)
