# Hibernate 学习
### 什么是 Hibernate
- Hibernate 是 Java 领域一款开源的 ORM 框架技术，对 JDBC 进行了**轻量级**的封装
- Hibernate 处于应用和数据库之间，称之为**持久化层**
- ORM : 对象关系映射
### 其他主流的 ORM框架 技术
1. MyBatis
2. Toplink
3. EJB

### 编写 Hibernate 例子
1. 创建 Hibernate 的配置文件
  ```
  <session-factory>
    <property name="connection.username">root</property>
    <property name="connection.password">root</property>
    <property name="connection.driver_class">com.mysql.jdbc.Driver</property>
    <property name="connection.url">jdbc:mysql:///hibernate?useUnicode=true&amp;characterEncoding=UTF-8</property>
    <property name="dialect">org.hibernate.dialect.MySQLDialect</property>
    <property name="show_sql">true</property>
    <property name="format_sql">true</property>
    <property name="hbm2ddl.auto">create</property>
    <mapping resource="Students.hbm.xml" />
  </session-factory>
  ```
2. 创建持久化类
> 持久化类是一个普通类，但是要遵循 JavaBean 的原则

3. 创建对象-关系映射文件
4. 使用 Junit 进行测试
  - `@Before` : 初始化方法
  - `@Test` ：测试方法
  - `@After` : 释放资源
5. 通过 Hibernate API 编写访问数据库的代码

### Hibernate 进阶
1. hibernate.cfg.xml 常用配置

| 属性名字 | 含义 |
|--------|--------|
|hibernate.show_sql|是否把 Hibernate 运行时的 SQL 语句输出到控制台，编码阶段便于测试|
|hibernate.format_sql|输出到控制台的 SQL 语句是否进行排版|
|hbm2ddl.auto|可以帮助由 Java 代码生成数据库脚本，进而生成具体的表结构。create/update/create-drop/validate|
|hibernate.default_schema|默认的数据库|
|hibernate.dialect|配置 hibernate 数据库方言，hibernate 可针对特殊的数据库进行优化。|
|注意|hibernate 的前缀可以省略，即 hibernate.show_sql 等于 show_sql|
2. session 简介
> session 可以简单理解为操作数据库的对象，session 与 connection 是多对一的关系，一个 connection 可以在不同时刻供多个 session 使用。session的方法有：save() update() delete() createQuery() （增删改查） 等。

3. transaction 简介
> hibernate 对数据的操作都是封装在事务中，并且默认是非自动提交的方式。所以用 session 保存对象时，如果不开启事务并且手工提交事务，对象不会真正保存在数据库中。
4. session 详解

5. 对象关系映射常用配置
