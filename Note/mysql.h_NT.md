mysql.h_NT



常用对象

```
MYSQL mysql;  				//mysql标记对应某个数据库
MYSQL_ROW row;  			//row[i]可用于输出该行第i个字段的数据

MYSQL_FIELD *field;  		//用于定义一个存储字段信息的对象,field->name存储对应字段名称
    name - 列名
    orgname - 原始的列名（如果指定了别名）
    table - 表名
    orgtable - 原始的表名（如果指定了别名）
    max_length - 字段的最大宽度
    length - 在表定义中规定的字段宽度
    charsetnr - 字段的字符集号
    flags - 字段的位标志
    type - 用于字段的数据类型
    decimals - 整数字段，小数点后的位数
    
MYSQL_RES *res;				//用于定义一个存储数据库检索信息结果的对象。
```



常用函数

```
MYSQL *mysql_init( MYSQL *mysql );
//初始化mysql对象，成功返回指针地址，失败返回空指针


MYSQL *mysql_real_connect (
    MYSQL *mysql,   //初始化的MYSQL对象,与mysql_init()对应
    const char *host,   //主机地址
    const char *user,   //用户，例如：root
    const char *passwd,   //数据库的密码
    const char *db,   //要连接的数据库，例如：student
    unsigned int port,   //端口，可填0
    const char *unix_socket,   //一般为NULL
    unsigned long client_flag);  //一般为0
// 建立MySQL连接


int mysql_query( MYSQL *mysql, char * command );
//执行sql语句，查询成功返回0，失败返回非0，错误类型见说明文档


MYSQL_RES *mysql_store_result(MYSQL *mysql);
//获取查询结果，返回具有多个结果的MYSQL_RES结果集合。如果出现错误，返回NULL。
对于成功检索了数据的每个查询（SELECT、SHOW、DESCRIBE、EXPLAIN、CHECK TABLE等），必须调用mysql_store_result()或mysql_use_result() 。
对于其他查询，不需要调用mysql_store_result()或mysql_use_result()，但是如果在任何情况下均调用了mysql_store_result()，它也不会导致任何伤害或性能降低。


int mysql_num_rows( MYSQL_RES *result );
//获取结果行数

int mysql_num_fields( MYSQL_RES *result );
//获取结果字段数(列数， row的size)

MYSQL_ROW mysql_fetch_row(MYSQL_RES *result);
//从结果集中获取下一行，结束返回NULL。

MYSQL_FIELD* mysql_fetch_field(MYSQL_RES *result);
//用于获取下一个字段的所有描述，存于一个MYSQL_FIELD 指针对象

MYSQL_FIELD* mysql_fetch_field_direct(MYSQL_RES *result, int i); 
//指定字段序号(列号)，返回字段信息


```

