title: "PHPUnit安装和使用"
date: 2015-05-21 00:35:37
categories: Other
tags: Other
---

## PHPUnit 安装

* [PHPUnit官网](https://phpunit.de/ "PHPUnit官网")，直接点击下载PHPUnit4.6 *需要注意的是PHPUnit和PHP版本的匹配*，也可以通过（`wget https://phar.phpunit.de/phpunit.phar`）直接下载

* 通过scp直接上传文件到服务器
	* 将文件传到远程服务器(`scp local_file remote_username@remote_ip:remote_folder`)
	* 将目录传到远程服务器加r就好（`scp -r local_folder remote_username@remote_ip:remote_folder`*）
	* 将远程服务器文件下载到本地（`scp remote_username@remote_ip:remote_file local_file`*）
	* 同理下载远程目录加r即可（`scp -r remote_username@remote_ip:remote_file local_file`）
* 不管是你用wget直接在服务器下的还是先下载好传到服务器的，你都会发现一个叫<b>phpunit.phar的文件</b>，将他移动到/usr/local/bin目录下`mv phpunit.phar /usr/local/bin/phpunit`
* 赋予phpunit执行权限`chmod +x phpunit`
* 使用`/usr/local/bin/phpunit --version`查看是否安装好，执行结果如果是phpunit的版本号，则证明安装成功

关于PHPUnit详细内容请参考[PHPUnit文档](https://phpunit.de/manual/current/zh_cn/installation.html "PHPUnit中文官网")

## PHPUnit 使用
请保持姿态持续关注，正在更新中