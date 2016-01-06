title: "sed的使用"
date: 2015-12-24 09:41:56
categories: Linux
tags: Linux
---


# sed使用场景

	1.获取指定行数
	sed -n '1,2p' test.txt（查看第1到2行的内容）
	sed -n '1,$p' test.txt（查看第1行到文件末尾的内容）
	sed -n '2,3!'p test.txt（查看不在第2到3行的内容）
	sed -n '4q;2,3p' test.txt（读取第2到3行的内容，速度更快）

	2.打印包含某字符的行
	sed -n '/hello/p' test.txt（查看包含hello的行）

	3.删除行
	sed '/^#/d' test.txt（删除空行）
	sed '/hello/d' test.txt（删除包含hello的行）
	sed '5,10s/[a-z]//g' test.txt（删除第5行到第10行中的小写字母）
	sed '5,$'d test.txt（删除第五行之后的内容）
	sed 's/[^0-9a-zA-Z]//g' test.txt（删除除数字和字母以外的字符）
	sed '/^#/d;G;G' test.txt（删除空行添加两个空行）
	sed 'n;n;n;d;'  test.txt（删除第4行的倍数行）

	4.选择特定的行，进行替换
	sed '/demo/! s/hello/haha/g' test.txt > test1.txt（找到不包含demo的行中的hello替换成haha）
	sed '/demo/! s#hello#haha#g' test.txt > test1.txt（避免替换/bin这种字符串的问题，把正则定界符换成#）
	sed 'y/demo/Demo/' test.txt

	5.把结果保存到文件
	sed '1,2d;w demo.txt' test.txt（将第1，2行删除后保存到demo.txt文件）

	6.添加字符
	sed "1,3a hello\ndemo" test.txt（在第一行到第三行后添加字符串“hello\ndemo”）

	7.替换
	sed '1,3c hello' test.txt（把第一行到第三行替换成hello）

	8.插入
	sed -i '$a haha_i' test.txt（在文件的末尾插入字符串“haha_i”）

# sed参数说明

	用法: sed [选项]... {脚本(如果没有其他脚本)} [输入文件]...

      -n, --quiet, --silent
                     加上-n参数后，则只有经过sed特殊处理的那一行(或者动作)才会被列出来
      -e 脚本, --expression=脚本
                     添加“脚本”到程序的运行列表
      -f 脚本文件, --file=脚本文件
                     添加“脚本文件”到程序的运行列表
      --follow-symlinks
                     follow symlinks when processing in place; hard links
                     will still be broken.
      -i[SUFFIX], --in-place[=SUFFIX]
                     直接修改读取的文件内容，不是输出到屏幕
      -c, --copy
                     取代／替换字符串
      -l N, --line-length=N
                     指定“l”命令的换行期望长度
      --posix
                     关闭所有 GNU 扩展
      -r, --regexp-extended 在脚本中使用扩展正则表达式
      -s, --separate
                     将输入文件视为各个独立的文件而不是一个长的连续输入
      -u, --unbuffered
                     从输入文件读取最少的数据，更频繁的刷新输出
          --help     打印帮助并退出
          --version  输出版本信息并退出

    如果没有 -e, --expression, -f 或 --file 选项，那么第一个非选项参数被视为
    sed脚本。其他非选项参数被视为输入文件，如果没有输入文件，那么程序将从标准
    输入读取数据。