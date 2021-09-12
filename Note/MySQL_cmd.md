**数据库常用命令**
<br>

**sql语法规范**

<br>"<>"内的内容为必填项，"[]"内的内容为选填项。
<br> [,....]的意思是“等等”，即前面的项可重复。
<br> 花括号{}和|表明此处为选择项，在所列出的各项中仅需选择一项

**完整性约束**
<br>列级
<br>主键约束：`PRIMARY KEY`
<br>检查，拒绝接受不满足条件的值: `checck(条件表达式)`
<br>外键约束：`foreign key`
<br>唯一性约束：`UNIQUE`
<br>非空值约束：`NOT NULL`
<br>设置字段默认值： `default<默认值>`

<br>**命令行指令**

<br>`mysqld --console `		&emsp;&emsp;&emsp;&emsp;	//启动命令
<br> `mysqladmin -uroot shutdown `&emsp;&emsp;&emsp;&emsp;      // 关闭命令
<br> `mysql -u root -p `&emsp;&emsp;&emsp;&emsp; // 登录到root用户
<br> `net start 服务名`  &emsp;&emsp;&emsp;&emsp;  //启动MySQL服务

<br> **MySQL语句**

<br>`exit` &emsp;&emsp;&emsp;&emsp;   //退出MySQL终端
<br>

`desc <表名>`		//查看表结构

`show databases;`&emsp;&emsp;&emsp;&emsp;  //查看数据库
<br>`use 数据库名;`&emsp;&emsp;&emsp;&emsp;  //改变当前数据库
<br>`show tables;`&emsp;&emsp;&emsp;&emsp;//  查看当前数据库表单
<br>`create database` &emsp;&emsp;&emsp;&emsp;// 数据库名; 创建数据库
<br>

`create table 表名(`<br>
`<字段> <数据类型 [(数据长度)]> [列级完整性约束条件],`<br>
`[,...]`<br>
`[表级完整性约束条件],`<br>
`[,...]`
`);` &emsp;&emsp;&emsp;&emsp;//创建表

<br>`drop database 数据库名;` &emsp;&emsp;&emsp;&emsp;//删除数据库
<br>`drop table 表名;`&emsp;&emsp;&emsp;&emsp; //删除表
<br>`alter table 表名 drop <字段>;`&emsp;&emsp;&emsp;&emsp; //删除表中的字段
<br>`alter table 表名 add <字段>[类型]长度];`&emsp;&emsp;&emsp;&emsp;// 增加字段

`alter table <表名> add constraint <约束名>[(复合主键字段1,复合主键字段2)]` 	//设置约束

<br>

`delete from 表名 where <条件语句>;`   				//删除表内记录

`truncate table 表名;`					//清楚表内所有记录 

`insert into <表名>(字段1,字段2...字段n)values(取值1,取值2,...取值n);`			//插入记录

`select <字段名1>[字段名2,...] from <表名>		[where 条件语句][limit n][offsetn]` 			//查询数据库指定字段的记录