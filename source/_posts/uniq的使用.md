title: "uniq的使用"
date: 2015-12-29 09:41:50
categories: Linux
tags: Linux
---

# uniq的使用场景

# uniq的参数说明

	用法：uniq [选项]... [文件]
    从输入文件或者标准输入中筛选相邻的匹配行并写入到输出文件或标准输出。

    不附加任何选项时匹配行将在首次出现处被合并。

    长选项必须使用的参数对于短选项时也是必需使用的。
      -c, --count		在每行前加上表示相应行目出现次数的前缀编号
      -d, --repeated	只输出重复的行
      -D, --all-repeated[=delimit-method	显示所有重复的行
    			delimit-method={none(default),prepend,separate}
    			以空行为界限
      -f, --skip-fields=N	比较时跳过前N 列
      -i, --ignore-case	在比较的时候不区分大小写
      -s, --skip-chars=N	比较时跳过前N 个字符
      -u, --unique		只显示唯一的行
      -z, --zero-terminated	使用'\0'作为行结束符，而不是新换行
      -w, --check-chars=N	对每行第N 个字符以后的内容不作对照
          --help		显示此帮助信息并退出
          --version		显示版本信息并退出

    若域中为先空字符(通常包括空格以及制表符)，然后非空字符，域中字符前的空字符将被跳过。

    提示：uniq 不会检查重复的行，除非它们是相邻的行。
    如果您想先对输入排序，使用没有uniq 的"sort -u"。
    同时，比较服从"LC_COLLATE" 变量所指定的规则。