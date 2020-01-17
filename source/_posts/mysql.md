---
title: mysql命令
date: 2019-07-12 16:53:23
tags: 命令
categories: mysql
---
这次记录理解学习mysql命令
<!-- more -->
```
create database xx;//创建数据库xx
show databases;查看数据库
drop database xx;删除数据库

use xx;//进入xx数据库
create table xxx (id int (32),username varchar(40),password varchar(32));创建表格式
show create tables;查看表
desc xxx;// 查看表结构
select database();//查看当前表在哪个库下 
drop xxx;//删除xxx表
alter table 原表命 rename 新表明
alter table xx change 字段名 字段名1 varchar(66);//修改字段
alter table xx modify 字段名 修改值;//修改字段值
alter table xx drop 字段名;//删除字段
alter table xx add 字段名 varchar(55) first;//插入字段到首行
alter table xx add 字段名 varchar(55) after 字段名1;//插入到字段名1后一行
show index from xx;//查看索引情况
alter table xx add index(字段);//给字段加入普通索引 
alter table xx add unique(字段);//给字段加入唯一索引 
alter table xx add fulltext(字段);//给字段加入全文索引 
alter table xx add primary key(字段);//给字段加入主键索引 

insert into bbs_user values(1,'成龙',123123,64,223,333324);//给bbs_user表下插入数据
insert into bbs_user(id , username , password , age , email , address ) values(2,'萨拉赫',123445,12,1231,123123),('库蒂尼奥' ，1231，13，1312，132123);//与上一条命令不同在于自动递增的id字段不用输入直接从username开始就行，也可插入多条数据，更灵活

select * from bbs_user;//查看bbs_user表下的数据
select count (*) from bbs_user;//查看bbs_user表下的数据个数
select * from bbs_user where id=2;//查看bbs_user表下id=2的数据
select * from bbs_user where id>2;//查看bbs_user表下id>2的数据
select username, address from bbs_user;//查看bbs_user表下username, address的数据
select * from bbs_user where id in<1,3,>;//查看bbs_user表下id为1，3，4，的数据
select * from bbs_user where username like '四%';//模糊查询，查bbs_user表username开头为四的数据
select * from bbs_user where username like '%四'%;//模糊查询，查bbs_user表username有四的数据
select * from bbs_user order by address;//使bbs_user表根据address字段升排序 
select * from bbs_user order by address desc;//使bbs_user表根据address字段降排序 
select * from bbs_user group by password;//将表按照password字段分组，（字段相同不显示）
select * from bbs_user limit 5,15;//检索记录行6到行15
select username , gname from shop_user inner join shop_goods on shop_user.gid = shop_goods.gid;//内联查询 ，查询两个表对应的数据（一二，二三，看一三）
select shop_user.username  from shop_user left join shop_goods on shop_user.gid = shop_goods.gid;//左联查询，以左表为基准
select shop_user.username from shop_user right join shop_goods on shop_user.gid = shop_goods.gid;//右联查询，以右表为基准
select *from shop_user where gid in(select gid from shop_goods);//查shop_user下有带shop_goods中gid中的值的所有数据
delete from bbs_user where username='李敖';//删除表中数据
update bbs_user set username='安安',address='88888' where id=1;//把id为1的数据的username字段改为安安，address字段改为88888
```
