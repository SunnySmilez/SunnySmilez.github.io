title: "phptrace安装与使用"
date: 2015-05-21 01:12:11
categories: Other
tags: Other
---

## phptrace安装
* 下载[phpstrace](https://pecl.php.net/package/trace "phpstrace下载地址")，上传到服务器[不懂的同学参考这里](http:// "还没有完成")
* 使用命令`tar -zxf phptrace-{version}.tar.gz`进行解压（*phptrace-{version}.tar.gz就是你压缩包的位置*）
* `cd phptrace-{version}`（*进入解压后的文件夹*）
* `cd extension`
* `{php_bin_dir}/phpize`（*进入php的安装目录下的/bin/phpize的目录,一般的在/usr/local/php/bin/phpize*）
* `./configure --with-php-config={php_bin_dir}/php-config && make && make install`
* 注意查看执行的命令会出现extension_dir这里指的是你的拓展包文件被编译的位置
* `php -i | grep php.ini`查看你的php.ini的位置，进入编辑，添加extension `extension=trace.so`，需要保证你的so文件的位置和你系统extension默认加载位置一致
* `cd ../cmdtool && make`（*安装一个命令行操作工具，便于使用strace*）
* 记得重启php-fpm（*杀死 `killall php-fpm` 或者 `ps aux | grep php-fpm` 找到他们的进程号一个个的`kill -9 pid` 启动`/usr/local/php/bin/php-fpm` /usr/local/php是你的php安装目录*）
* 测试`php -r 'for ($i = 0; $i < 100; $i++) usleep(10000);' & ./phptrace -p $!`
输出结果为
		1431681727.341829      usleep  =>  NULL   wt: 0.011979 ct: 0.011980
		1431681727.341847      usleep(10000) at [Command line code:1]
		1431681727.353831      usleep  =>  NULL   wt: 0.011984 ct: 0.011983
		1431681727.353849      usleep(10000) at [Command line code:1]
		1431681727.365829      usleep  =>  NULL   wt: 0.011980 ct: 0.011981
		1431681727.365848      usleep(10000) at [Command line code:1]
		
## phptrace使用
请保持持续关注，正在不断更新中

[参考链接地址](https://github.com/Qihoo360/phptrace "phptrace github地址")