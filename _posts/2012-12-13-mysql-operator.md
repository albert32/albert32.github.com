---
layout: post
title: "mysql操作命令"
description: ""
category: database 
tags: [ mysql]
published: true
---

#关于
打算这几天把mysql技术内幕看完，顺便做些读书笔记，以备后用。

1.数据库管理

*.新建用户 

	cteate user 'albert'@'localhost' identified by '123456'; // username=albert,passwd=123456
    grant all on *.* to 'albert'@'localhost';

*.登录数据库

	mysql -h host -u username -p
    
*.查看数据库和表信息

	show databases；
    show tables；
    use   databasename  //select database
    
2.创建数据库

	create database name；
    
3.导入数据

*.纯数值的数据

	使用load data local 命令，local功能默认禁止
    mysql --local-infile databasename  -uusername  -p;
    load  data local infile 'data.txt' into table tablename;

*.导入sql语句

	1.mysql databasename < data.sql
    2.进入mysql .  source  data.sql;
    
4.限制查询结果数据行个数

	limit number//limit lines offset:跳过前lines记录返回之后的offset个数据记录
    eg：select first_name last_name birth from president order by birth limit 5;
    








