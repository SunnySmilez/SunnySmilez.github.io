title: "join的使用"
date: 2015-12-26 10:17:46
categories: Linux
tags: Linux
---

# join的使用案例

1.文件内容
cat month_cn.txt

	1       一月
	2       二月
	3       三月
	4       四月
	5       五月
	6       六月
	7       七月
	8       八月
	9       九月
	10      十月
	11      十一月
	12      十二月
	13      十三月，故意的

2.文件内容
cat month_en.txt

	1       January
	2       February
	3       March
	4       April
	5       May
	6       June
	7       July
	8       August
	9       September
	10      October
	11      November
	12      December
	14      MonthUnknown

3.内连接（指定关联行数）
join month_cn.txt month_en.txt
join -j 1 month_cn.txt month_en.txt(`以第一行作为匹配字段`)
join -1 1 -2 1 month_cn.txt month_en.txt(`第一个文件的第一行和第二个文件的第一行进行匹配`)

	1 一月 January
    2 二月 February
    3 三月 March
    4 四月 April
    5 五月 May
    6 六月 June
    7 七月 July
    8 八月 August
    9 九月 September
    10 十月 October
    11 十一月 November
    12 十二月 December

4.左连接（以全面文件为主去匹配后面文件的内容）
join -a1 month_cn.txt month_en.txt

	1 一月 January
    2 二月 February
    3 三月 March
    4 四月 April
    5 五月 May
    6 六月 June
    7 七月 July
    8 八月 August
    9 九月 September
    10 十月 October
    11 十一月 November
    12 十二月 December
    13 十三月，故意的

5.右连接
join -a2 month_cn.txt month_en.txt

	1 一月 January
    2 二月 February
    3 三月 March
    4 四月 April
    5 五月 May
    6 六月 June
    7 七月 July
    8 八月 August
    9 九月 September
    10 十月 October
    11 十一月 November
    12 十二月 December
    14 MonthUnknown

6.全连接
join -a1 -a2 month_cn.txt month_en.txt

	1 一月 January
    2 二月 February
    3 三月 March
    4 四月 April
    5 五月 May
    6 六月 June
    7 七月 July
    8 八月 August
    9 九月 September
    10 十月 October
    11 十一月 November
    12 十二月 December
    13 十三月，故意的
    14 MonthUnknown

7.指定输出内容
join -o 1.1 1.2 2.2 month_cn.txt month_en.txt

	1 一月 January
    2 二月 February
    3 三月 March
    4 四月 April
    5 五月 May
    6 六月 June
    7 七月 July
    8 八月 August
    9 九月 September
    10 十月 October
    11 十一月 November
    12 十二月 December

8.前面文件存在，后面文件不存在的内容
join -v 1  month_cn.txt month_en.txt

	13 十三月，故意的



# join参数说明
	用法：join [选项]... 文件1 文件2(找出两个文件中，指定栏位内容相同的行，并加以合并，再输出到标准输出设备。)
    针对每一对具有相同内容的输入行，整合为一行写到标准输出，
    默认的内容连接区块是由第一个空白符代表的分界符号。当文件1
    或文件2 都被指定为"-"时，程序将从标准输入读取数据。

      -a  文件编号    	文件编号的值可以是1 或2，分别对应文件1 和 文件2。
                          	此选项用于根据指定文件编号输出不成对的行目。
      -e 字符    		将缺失的输入区块替换为指定字符
      -i, --ignore-case 	比较时忽略大小写
      -j 域 		等于"-1 域 -2 域"
      -o 格式 		按照指定格式构造输出行
      -t 字符 		使用指定字符作为输入和输出的分隔符
      -v 文件编号        	类似 -a 文件编号，但禁止组合输出行
      -1 域          	在文件1 的此域组合
      -2 域          	在文件2 的此域组合
      --check-order     	检查输入行是否正确排序，即使所有输入行均是成对的
      --nocheck-order   	不检查输入是否正确排序
          --help		显示此帮助信息并退出
          --version		显示版本信息并退出

    除非使用了"-t 字符串" 选项，否则前导空格分隔的域将被忽略，如果指定了字符串，
    则使用指定字符串分隔任意的域并从1 开始计数的域编号。可以指定的格式是由一个
    或多个逗号活空格所分隔的描述，其形式为"文件编号.域"或者"0"。默认的
    格式输出合并后的域、文件1 和文件2 剩下的域，均由该指定字符串分隔。