Linux_MySQL_Nt

```
shell 指令

	service mysql start			//启动mysql服务， restart重启服务， stop停止服务

```



```
sql 语句
	
	CREATE DATABASE [IF NOT EXISTS] <数据库名>			建库
	
	use <db_name>			切换数据库
	show databases			显示所有数据库
	show tables				显示当前数据库所有表
	desc <tb_name>			查询表结构
	
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

