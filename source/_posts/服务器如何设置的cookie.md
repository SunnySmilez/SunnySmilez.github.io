title: "服务器如何设置的cookie"
date: 2015-12-18 15:05:40
categories: PHP
tags: PHP
---

## 一个joke
	<?php
		setcookie('key', 'value', time()+1000, '/', 'hostname');
		var_dump($_COOKIE);

	为什么不能打印出cookie？难道代码写错了么？你知道么？

## cookie设置流程
	1.首先调用setcookie函数的时候服务器端会在header头里面发送：set-cookie key=value，以此来告诉客户端我需要设置cookie
	2.客户端会通过一定的方法将cookie存储起来
	3.每次访问的时候都会在header里面的cookie带上信息：key=value

## 结论

* 当立马设置完cookie然后去拿cookie的时候当然拿不到cookie值key，因为它的当前请求中的cookie是不存在的，只有这次请求完之后，才会去设置号cookie然后请求的header信息中带上cookie

* 当然对于删除cookie和重置cookie都是同样的道理