Linux_MySQL_Nt



mysql.h 位置 /usr/include/mysql/

静态库名 mysqlclient

静态库位置/usr/lib/mysql/

```
shell 指令

	service mysql start			//启动mysql服务， restart重启服务， stop停止服务
	mysql -V/version			//查看mysql版本

```



```
sql 语句
	
	CREATE DATABASE [IF NOT EXISTS] <数据库名>			建库
	
	use <db_name>			切换数据库
	show databases			显示所有数据库
	show tables				显示当前数据库所有表
	desc <tb_name>			查询表结构
	alter table tbname auto_increment=1;		重置自增值为1
	
	建表
        CREATE [TEMPORARY] TABLE [IF NOT EXISTS] table_name
        [(
        COLUMN_DEFINITION,
        ...
        )]
        [TABLE_OPTIONS]
        [SELECT_STATEMENT]
		其中 COLUMN_DEFINITION的语法十分丰富：
			column_name type [NOT NULL | NULL] [DEFAULT default_value] [AUTO_INCREMENT] 
	
	增加
	
		INSERT INTO <表名> ( <列名1> [ , … <列名n>] )
		VALUES (值1， [… , (值n) ]) ;
		
	
	删除
		
		DELETE FROM <表名> [WHERE 子句] [ORDER BY 子句] [LIMIT 子句]		删除记录
		
		DROP TABLE <tb_name>			删除表
		
		drop database <db_name>			删除库      
	
	修改
	
        UPDATE <表名> SET 字段 1=值 1 [,字段 2=值 2… ] [WHERE 子句 ]
        [ORDER BY 子句] [LIMIT 子句]
        
        <表名>：
        	用于指定要更新的表名称。
        SET 子句：
        	用于指定表中要修改的列名及其列值。其中，每个指定的列值可以是表达式，也可以是该列对应的默认值。如			果指定的是默认值，可用关键字 DEFAULT 表示列值。
        WHERE 子句：
        	可选项。用于限定表中要修改的行。若不指定，则修改表中所有的行。
        ORDER BY 子句：
        	可选项。用于限定表中的行被修改的次序。
        LIMIT 子句：
        	可选项。用于限定被修改的行数。
	
	查询
	
        SELECT
        {* | <字段列名>}
        [
        FROM <表 1>, <表 2>…
        [WHERE <表达式>
        [GROUP BY <group by definition>
        [HAVING <expression> [{<operator> <expression>}…]]
        [ORDER BY <order by definition>]
        [LIMIT[<offset>,] <row count>]
        ]
	
```



```
MySQL的数据类型

整型

    tinyint(m)		1个字节  	范围(-128~127)
    smallint(m)		2个字节  	范围(-32768~32767)
    mediumint(m)	3个字节  	范围(-8388608~8388607)
    int(m)			4个字节  	范围(-2147483648~2147483647)
    bigint(m)		8个字节  	范围(+-9.22*10的18次方)
    
浮点型(float和double)

	float(m,d)		单精度浮点型    8位精度(4字节)     m总个数，d小数位
	double(m,d)		双精度浮点型    16位精度(8字节)    m总个数，d小数位

定点数

    浮点型在数据库中存放的是近似值，而定点类型在数据库中存放的是精确值。 
    decimal(m,d) 参数m<65 是总个数，d<30且 d<m 是小数位。
   
字符串(char,varchar,_text)

	char(n)			固定长度，最多255个字符
    varchar(n)		固定长度，最多65535个字符
    tinytext		可变长度，最多255个字符
    text			可变长度，最多65535个字符
    mediumtext		可变长度，最多2的24次方-1个字符
    longtext		可变长度，最多2的32次方-1个字符
    
    char和varchar：

        1.char(n) 若存入字符数小于n，则以空格补于其后，查询之时再将空格去掉。所以char类型存储的字符串末尾		不能有空格，varchar不限于此。 

        2.char(n) 固定长度，char(4)不管是存入几个字符，都将占用4个字节，varchar是存入的实际字符数+1个		字节（n<=255）或2个字节(n>255)，所以varchar(4),存入3个字符将占用4个字节。 
        
        3.char类型的字符串检索速度要比varchar类型的快。
        
    varchar和text： 

        1.varchar可指定n，text不能指定，内部存储varchar是存入的实际字符数+1个字节（n<=255）或2个字节		 (n>255)，text是实际字符数+2个字节。 

        2.text类型不能有默认值。 

        3.varchar可直接创建索引，text创建索引要指定前多少个字符。varchar查询速度快于text,在都创建索引的		情况下，text的索引似乎不起作用。

二进制数据(_Blob)

    1._BLOB和_text存储方式不同，_TEXT以文本方式存储，英文存储区分大小写，而_Blob是以二进制方式存储，不分	 大小写。

    2._BLOB存储的数据只能整体读出。 

    3._TEXT可以指定字符集，_BLO不用指定字符集。
    
日期时间类型

    date		日期 '2008-12-2'
    time		时间 '12:25:36'
    datetime	日期时间 '2008-12-2 22:06:44'
    timestamp	自动存储记录修改时间
    
    若定义一个字段为timestamp，这个字段里的时间数据会随其他字段修改的时候自动刷新，所以这个数据类型的字段可	以存放这条记录最后被修改的时间。,
```

