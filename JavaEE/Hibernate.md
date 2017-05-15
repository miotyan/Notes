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
