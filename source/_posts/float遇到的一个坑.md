title: "float遇到的一个坑"
date: 2015-11-04 12:50:05
categories: Mysql
tags: Mysql
---
## 需求
* 数据库需要存储金钱的数值单位为元，保留两位小数，需要选择mysql数据类型

## 坑
* 使用了float进行存储，结果导致了，内部的金额计算会有部分错误

## 选择理由
* decimal用于存储精确的小数，支持精确计算（5.0以后），会影响列到空间消耗
* float使用4个字节存储
* 浮点类型存储同样返回的值，通常比decimal使用更少的空间
* float已经修复了内部浮点数bug计算（*设计当初模糊的印象，没有去查证，实际是错的*）

## 解决方案
* 使用decimal(15,2)进行存储

## 实验
* `CREATE TABLE `account_float` (mon｀ey float(15,2) not null default '0.00') ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;`
* `insert into account_float(money) values(1234456.56);`
* `CREATE TABLE `account_decimal` (money decimal(15,2) not null default '0.00') ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;`
* `insert into account_decimal(money) values(1234456.56);`
`
## 结论
* 金额等需要精确计算的数据一般都用decimal进行存储
* 导致记录错误的原因是：float和double会存在隐性类型转换，设置的float长度过长的话，mysql会自动将数据类型转换成double
* float和double的精度是由尾数的位数来决定的。浮点数在内存中是按科学计数法来存储的，其整数部分始终是一个隐含着的“1”，由于它是不变的，故不能对精度造成影响。