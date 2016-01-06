title: "sort的使用"
date: 2015-12-29 09:32:36
categories: Linux
tags: Linux
---

# sort使用场景

	用法：sort [选项]... [文件]...
    　或：sort [选项]... --files0-from=F
    串联排序所有指定文件并将结果写到标准输出。

    长选项必须使用的参数对于短选项时也是必需使用的。
    排序选项：

      -b, --ignore-leading-blanks	忽略前导的空白区域
      -d, --dictionary-order	只考虑空白区域和字母字符
      -f, --ignore-case		忽略字母大小写
      -g, --general-numeric-sort	按照常规数值排序
      -i, --ignore-nonprinting	只排序可打印字符
      -M, --month-sort		比较 (未知) < "一月" < ... < "十二月"
    				在LC_ALL=C 时为(unknown) < `JAN' < ... < `DEC'
      -h, --human-numeric-sort    使用易读性数字(例如： 2K 1G)
      -n, --numeric-sort		根据字符串数值比较
      -R, --random-sort		根据随机hash 排序
          --random-source=文件	从指定文件中获得随机字节
      -r, --reverse			逆序输出排序结果
          --sort=WORD		按照WORD 指定的格式排序：
    					一般数字-g，高可读性-h，月份-M，数字-n，
    					随机-R，版本-V
      -V, --version-sort		在文本内进行自然版本排序

    其他选项：

          --batch-size=NMERGE	一次最多合并NMERGE 个输入；如果输入更多
    					则使用临时文件
      -c, --check, --check=diagnose-first	检查输入是否已排序，若已有序则不进行操作
      -C, --check=quiet, --check=silent	类似-c，但不报告第一个无序行
          --compress-program=程序	使用指定程序压缩临时文件；使用该程序
    					的-d 参数解压缩文件
          --files0-from=文件	从指定文件读取以NUL 终止的名称，如果该文件被
    					指定为"-"则从标准输入读文件名
      -k, --key=位置1[,位置2]	在位置1 开始一个key，在位置2 终止(默认为行尾)
      -m, --merge			合并已排序的文件，不再进行排序
      -o, --output=文件		将结果写入到文件而非标准输出
      -s, --stable			禁用last-resort 比较以稳定比较算法
      -S, --buffer-size=大小	指定主内存缓存大小
      -t, --field-separator=分隔符	使用指定的分隔符代替非空格到空格的转换
      -T, --temporary-directory=目录	使用指定目录而非$TMPDIR 或/tmp 作为
    					临时目录，可用多个选项指定多个目录
      -u, --unique		配合-c，严格校验排序；不配合-c，则只输出一次排序结果
      -z, --zero-terminated	以0 字节而非新行作为行尾标志
          --help		显示此帮助信息并退出
          --version		显示版本信息并退出

    POS 是F[.C][OPTS]，F 代表域编号，C 是域中字母的位置，F 和C 均从1开始计数
    如果没有有效的-t 或-b 选项存在，则从前导空格后开始计数字符。OPTS 是一个或多个
    由单个字母表示的顺序选项，以此覆盖此key 的全局顺序设置。如果没有指定key 则
    将其整个行。

    指定的大小可以使用以下单位之一：
    内存使用率% 1%，b 1、K 1024 (默认)，M、G、T、P、E、Z、Y 等依此类推。

    如果不指定文件，或者文件为"-"，则从标准输入读取数据。

# sort参数说明