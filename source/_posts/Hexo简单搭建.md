title: "Hexo简单搭建"
date: 2015-04-28 02:01:46
categories: Mysql 
tags: hexo
---

#用tab键出代码或者用反引号包围

	for(1) {
		if(1) {
			return true;
		}
	}

---
``There is a literal backtick (`) here.``
---

#大于号表示引用，要有空格

> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.

----
#表格样式，模拟写

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

#链接地址，在本地的about下面
See my [个人简介](/about) page for details.

**粗体**
*斜体*
_斜体_

#图片在本地的img下面
![Alt text](/img/me.jpg)
![Alt text](/img/me.jpg "Optional title")
![GitHub Mark](/img/me.jpg "GitHub Mark")

#链接地址
[不如](http://bruce-sha.github.io "不如的博客")

#参考文献，两种写法
I get 10 times more traffic from [Google] [1] than from
[Yahoo] [2] or [MSN] [3].
[1]: http://google.com/        "Google"
[2]: http://search.yahoo.com/  "Yahoo Search"
[3]: http://search.msn.com/    "MSN Search"

I get 10 times more traffic from [Google](http://google.com/ "Google")
than from [Yahoo](http://search.yahoo.com/ "Yahoo Search") or
[MSN](http://search.msn.com/ "MSN Search").

------------------------

[Google]: http://google.com/
[foo]: http://example.com/  "Optional Title Here"
