MySQL 学习
-----

### 配置 MySQL
- 安装目录下，bin 文件夹内的 MySQLInstanceConfig.exe 就是配置程序
- root 密码设置为 **root**
- 打开 my.ini 配置文件，将 default-character-set 和 character-set-server 的值修改为 utf8（不是 utf-8）
- 重启服务。可以手动也可以使用管理员CMD：`net stop mysql` ` net start mysql`
-------
### 使用 MySQL
- MySQL 参数

参数|描述
---|---
-D, --database=name|打开指定数据库
--delimiter = name|指定分隔符
-h, --host=name|服务器名称
-p, --password[=name]|密码
-P, --port=#|端口号
--prompt=name|设置提示符
-u, --user=name|用户名
-v, --version|输出版本信息并退出


- MySQL 登录与退出
	- 登录命令 
	
	```
	mysql -uroot -p
	```
	
	- 退出命令
	
	```
	exit
	quit
	\q		任意一个
	```

- 修改 MySQL 提示符
	- 连接客户端时通过参数指定
	
	```
	shell>mysql -uroot -proot --prompt
	```
	
	- 连接上客户端之后，通过 prompt 命令修改
	
	```
	mysql>prompt
	```
	
	- 提示符含义
	
	```
	\D		完整的日期
	\d		当前数据库
	\h		服务器名称
	\u		当前用户
	```
	
- MySQL 常用命令
	- 显示当前服务器版本: `SELECT VERSION();`
	- 显示当前日期时间: `SELECT NOW();`
	- 显示当前用户: `SELECT USER();`
- MySQL 语句规范 
	- 关键字与函数名称全部大写
	- 数据库名称、表名称、字段名称全部小写
	- SQL 语句必须以分号结尾
- 数据库操作
	- 创建数据库
	
	```
	CREATE { DATABASE | SCHEMA } [IF NOT EXISTS] db_name
	[DEFAULT] CHARACTER SET [=] charset_name;
	//IF NOT EXISTS表示如果不存在该数据库则创建，如果存在则发出警告（使用 SHOW WARNINGS; 可以查看警告）
	//SET 可以指定编码方式（创建后使用 SHOW CREATE DATABASE db_name; 可以查看编码方式）
	
	```
	- 查看数据库列表
	
	```
	SHOW { DATABASES | SCHEMAS } [LIKE 'pattern' | WHERE expr];
	```
	
	- 修改数据库编码方式
	
	```
	ALTER {DATABASE | SCHEMA} [db_name] [DEFAULT] CHARACTER SET [=] charset_name;
	```
	
	- 删除数据库
	
	```
	DROP { DATABASE | SCHEMA } [IF EXISTS] db_name;
	```
----
### 数据类型
	
- 整型
> UNSIGNED 设置无符号
	- TINYINT
	> 1 字节         
	- SMALLINT
	> 2 字节
	- MEDIUMINT
	> 3 字节
	- INT
	> 4 字节
	- BIGINT
	> 8 字节
- 浮点型
> UNSIGNED 设置无符号
	- FLOAT[(M,D)]
	> M 是数字总位数，D 是小数点后面的位数，如果省略 M 和 D ，根据硬件允许的限制来保存。单精度浮点数精确到大约 7 位小数位。
	- DOUBLE[(M,D)]

- 字符型
	-  CHAR[M]
	> 定长 0-255 字节
	- VARCHAR[M]
	> 变长 0-65525 字节
	- ENUM("value1","value2",....)
	>  1 或 2 个字节，取决于枚举值的个数（最多65535个值）
	- SET("value1","value2",...)
	> 1/2/4/8 个字节，取决于集合成员的数目（最多 64 个成员）
-----
### 数据表
- 打开数据库
```
USE db_name;       //打开数据库
SELECT DATABASE(); // 查看打开的数据库名称
```
- 创建数据表
```
CREATE TABLE [ IF NOT EXISTS] table_name(
    column_name data_type,     //字段定义以 , 分隔且最后一句不用逗号
    )
```
- 查看数据表
```
SHOW TABLES [FORM db_name] //查看数据表
[LIKE 'pattern' | WHERE expr]
```
```
SHOW COLUMNS FROM tb_name; //查看数据表结构
```
- 数据表操作
	-  插入记录
	
	```
	INSERT [INTO] tb_name [(col_name,....)] VALUES(value1,...);
	```
	
	- 自动编号 `AUTO_INCREMENT`
	> 必须与主键组合使用。默认情况下，起始值为1，每次增量为1。
	
	- 主键约束 `PRIMARY KEY`
	- 唯一约束 `UNIQUE KEY`
	> 唯一约束的字段可以为空值（NULL），每张表可以存在多个唯一约束。
	- 默认约束
	> 当插入记录时，如果没有明确为字段赋值，则自动赋予默认值。
	
-------
### 约束
- 外键的要求
	- 父表和子表必须使用相同的存储引擎，禁止使用临时表。
	- 数据表的存储引擎只能为 InnoDB 。
	> 编辑数据表的默认存储引擎：
	> MySQL 配置文件内修改： `default-storage-engine=INNODB`
	-  外键列和参照列必须具有相似的数据类型。其中数字的长度或是否用符号位必须相同，而字符的长度则可以不同。
	- 外键列接参照列必须创建索引，如果外键列没有索引，MySQL 自动创建索引。
	