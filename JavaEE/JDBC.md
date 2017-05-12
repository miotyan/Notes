# JDBC 学习
### JDBC 简介
> JDBC 全称 Java Data Base Connectivity (  Java数据库连接  )，可以为多种数据库提供统一的访问。

### JDBC 编程步骤
- 加载驱动程序
	- 加载 MySQL 驱动：` Class.forName("com.mysql.jdbc.Driver");`
	- 加载 Oracle 驱动：` Class.forName("oracle.jdbc.driver.OracleDriver")`
- 获得数据库连接
``` DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/db_name","root","root"); ```
- 创建  Statement 对象
`conn.createStatement();`


### 代码实例

```
package com;

import java.lang.Thread.State;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

import com.mysql.jdbc.Connection;

public class DButil {
	private static final String URL = "jdbc:mysql://127.0.0.1:3306/jdbcDemo1"; //jdbcDemo1 是数据库名
	private static final String USER = "root";
	private static final String PASSWORD = "root";

	public static void main(String[] args) throws Exception {
		// 1. 加载驱动程序
		Class.forName("com.mysql.jdbc.Driver");
		// 2. 获得数据库连接
		java.sql.Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);
		// 3. 操纵数据库
		Statement stmt = conn.createStatement();
		ResultSet rs = stmt.executeQuery("select user_name,age from goddess");  //注意 goddess 后面没有  ;  。
		while(rs.next()){
			System.out.println(rs.getString("user_name")+","+rs.getInt("age"));
		}
	}
}
```

