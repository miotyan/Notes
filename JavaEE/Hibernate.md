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
1. 创建 Hibernate 的配置文件 hibernate.cfg.xml
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
2. 创建持久化类(实体类)
> 持久化类是一个普通类，但是要遵循 JavaBean 的原则

3. 创建对象-关系映射文件(实体.hbm.xml)<br />
   将文件添加到配置文档中`<mapping resource="Students.hbm.xml" />`
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
  - 获得 session 对象
    - openSession
    - getCurrentSession
    > 使用 `getCurrentSession` 需要在 `hibernate.cfg.xml` 中进行配置：
      - 对于本地事务(jdbc事务)，添加 `<property name="hibernate.current_session_context_class">thread</property>`
      - 对于全局事务(jta事务)，添加 `<property name="hibernate.current_session_context_class">jta</property>`

    - openSession 与 getCurrentSession 的区别
      1. getCurrentSession 在事务提交或者回滚之后会自动关闭，而 openSession 需要手动关闭。如果使用 openSession 而没有手动关闭，多次之后会导致连接池溢出。
      2. openSession 每次创建新的 session 对象，getCurrentSession 使用现有的 session 对象。
5. 对象关系映射常用配置（hbm.xml 配置文件）
  - mapping 标签
  ```
  <hibernate-mapping
    schema="schemaName"                       //模式名
    catalog="catalogName"                     //目录名称
    default-cascade="cascade_style"           //级联风格
    default-access="field|property|ClassName" //访问策略
    default-lazy="true|false"                 //加载策略
    package="packagename"                     //默认包名
  />
  ```
  - class 标签
  ```
  <class
    name="ClassName"          //映射的类
    table="tableName"         //映射的数据库表
    batch-size="N"            //抓取策略
    where="condition"         //抓取条件
    entity-name="EntityName"  //同一实体类映射多张表
  />
  ```
  - id 标签
  ```
  <id                                     //表的主键
    name="propertyName"                   //映射的属性
    type="typeName"                       //数据类型
    column="column_name"                  //映射成数据库字段的名称
    length="length"                       //指定长度
    <generator class="generatorClass" />  //主键生成策略
  </id>
  ```
    - 主键生成策略

|标识符生成器|描述|
|--------|--------|
|increment|适用于代理主键。由 Hibernate 自动以递增方式生成|
|identity|适用于代理主键。由底层数据库生成标识符|
|sequence|适用于代理主键。Hibernate 根据底层数据库的序列生成标识符，要求底层数据库支持序列|
|native|适用于代理主键。根据底层数据库对自动生成标识符的方式，自动选择 identity、sequence 或 hilo|
|assigned|适用于自然主键。由 Java 应用程序负责生成标识符|

### Hibernate 单表操作
- 单一主键
  - assigned 手工赋值
  - native MySQL生成的标识符是 increment，Oracle 则是 sequence。
- 基本类型

|Hibernate 映射类型|Java 类型|备注|
|---|---|---|
|integer/int|java.lang.Integer/int||
|float|java.lang.Float/float||
|double|java.lang.Double/double||
|character|java.lang.Character/java.lang.String/char||
|string|java.lang.String||
|boolean/yes_no/true_false|java.lang.Boolean/Boolean||
|date|java.util.Date/java.sql.Date||
|time|java.util.Date/java.sql.Time||
|timestamp|java.util.Date/java.sql.Timestamp|时间戳|
|calendar|java.util.Calendar||
|calendar_date|java.util.Calendar|.|

- 对象类型

|Hibernate 映射类型|Java 类型|标准 SQL 类型|MYSQL 类型|备注|
|---|---|---|---|---|
|binary|byte[]|VARCHAR(或 BLOB)|BLOB|字节数组|
|text|java.lang.String|CLOB|TEXT|大文本数据|
|clob|java.sql.Clob|CLOB|TEXT|大文本数据|
|blob|java.sql.Blob|BLOB|BLOB|大二进制数据文件|
- 组件属性
> 实体类中的某个属性属于用户自定义的类的对象

  对象关系映射文件修改
```
<component name="address" class="Address">
  <property name="postcode" column="POSTCODE"></property>
  <property name="phone" column="PHONE"></property>
  <property name="address" column="ADDRESS"></property>
</component>
```
- 单表操作 CRUD(增删改查) 实例
  - save
  - update
  - delete
  - get/load (查询单个记录)<br />
  get 和 load 的区别：
    1. get 会在调用后立即向数据库发出 sql 语句，返回持久化对象。load 方法会在调用后返回一个代理对象。该代理对象只保存了实体对象的 id ，直到使用对象的非主键属性值时才会发出 sql 语句。
    2. 查询数据中不存在的数据时， get 方法返回 null ，load 方法抛出异常`org.hibernate.ObjectNotFoundExecption`

### 单向一对多映射
如何实现一对多映射：
  - 数据库中，可以通过添加主外键的关联，表现一对多的关系
  - 在 Hibernate 中，通过在一方持有多方的集合实现，即在“一”的一端中使用`<set>`元素表示持有“多”的一端的对象。

```
<set name="" table="">
		<!-- 指定关联的外键列 -->
		<key column=""></key>
		<one-to-many class="" />
</set>
name 是"多"的名字
table 是"多"的表名
column 是外键列名
class 是"多"的实体类
```
  - set 元素的常用属性

|属性|含义和作用|必须|默认值|
|--|--|--|--|
|name|映射类属性的名称|Y||
|table|关联类的目标数据库表|N||
|lazy|指定关联对象是否使用延迟加载|N|proxy|
|inverse|标识双向关联中被动的一方|N|false|

### 单向多对一映射
在"多"的实体类添加"一"的属性和`get set`方法，然后在"多"的对象关系映射文件中配置多对一关联关系
```
<many-to-one name="" class="" column=""></many-to-one>
```
`name`是"一"的名字，`class`是"一"的实体类，`column`是"一"对应的数据库表主键
### 双向多对一映射
在这种关系中，既可以方便的由学生查找到对应的班级信息，也可以方便的由班级查找到其所包含的学生信息。
- 在双方的对象关系映射文件中都配置关联关系
- inverse 属性
  - `<set>`节点的 inverse 属性指定关联关系的控制方向，默认由"一"方来维护
  - 关联关系中，inverse="false" 则为主动方，由主动方负责维护关联关系
  - 在一对多关联中，只能设置"一"方的 inverse 为 true ，这将有利于性能的改善
- cascade 属性
  - 当设置了 cascade 属性不为 none 时，Hibernate 会自动持久化所关联的对象
  - cascade 属性的设置会带来性能上的变动，需谨慎设置

|属性值|含义和作用|
|---|---|
|all|对所有操作进行级联操作|
|save-update|执行保存和更新操作时进行级联操作|
|delete|执行删除时进行级联操作|
|none|对所有操作不进行级联操作|

### 多对多关联
- 在数据库底层通过添加中间表来指定关联关系
- 在双方的实体类中添加一个保存对方的集合（Set）
- 在双方的映射文件中使用`<set>`元素和`<many-to-many>`元素进行关联关系的配置<br>
  注意：<br>
    - 配置关联关系的表是中间表
    - `set`的`name`是当前实体类中保存的对方的集合名
    - `key`的`column`是当前实体的一方在中间表中的id
    - `many-to-many`中：
      - `class`是对方的实体类的全名
      - `column`是对方在中间表中的id
    - `<set>`可以使用 `inverse` 属性来控制由哪一方维护关联关系，当值为`true`时，由对方维护关联关系
    - `<set>`可以使用 `cascade` 属性来使保存对象到数据库的操作级联进行，即只需保存当前实体类的实例对象，即可自动保存关联的另一方的实例对象。

### HQL 数据查询语言
- HQL 语句形式<br />
   `select...` `from...` `where...` `group by...` `having...` `order by...`<br/>
   其中 `from` 是不可或缺的
- 注意事项
  - HQL 是面向对象的查询语言，对Java类和属性大小写敏感
  - HQL 对关键字不区分大小写
- `org.hibernate.Query` 接口
  1. `Query` 接口定义有执行查询的方法，并返回查询的结果。



### Hibernate 缓存
- 一级缓存<br />
  - 基本知识：
    1. 也称 "Session缓存"、"会话级缓存"
    2. 通过 Session 从数据库查询实体时会把实体在内存中存储起来，下一次查询同一实体时不再从数据库获取，而从内存中获取，这就是缓存
    3. 一级缓存的声明周期和 Session 相同， Session 销毁，它也销毁。
    4. 一级缓存中的数据可适用范围在当前会话之内
  - API:<br />
    一级缓存无法取消，系统强制执行，用两个方法管理
    - `evict()` 用于将某个对象从 Session 的一级缓存中清除
    - `clear()` 用于将一级缓存中所有对象清除
    - 用`session`对象调用：`session.evict(e);`
    - `query.list()` 无法使用一级缓存
    - `query.iterate()` 创建的迭代器则先在数据表查询主键，然后逐条根据主键在缓存中找到相应数据
- 二级缓存
> 二级缓存是所有 session 共用的缓存，在某个 session 中缓存后，可以在其他 session 中直接使用。二级缓存不是默认开启的，需要手动配置

  - 二级缓存配置步骤
    1. 添加二级缓存对应的 jar 包
    2. 在 hibernate 的配置文件中开启二级缓存，添加 Provider 类的描述<br />
      ```
      <!-- 开启二级缓存 -->
      <property name="hibernate.cache.use_second_level_cache">true</property>
      <!-- 注册二级缓存工厂 -->
	    <property name="cache.region.factory_class">org.hibernate.cache.ehcache.EhCacheRegionFactory</property>
      ```
    3. 添加二级缓存的属性配置文件<br />
       在 id 标签前面加上`<cache usage="read-only"/>`
    4. 在需要被缓存的表所对应的映射文件中添加`<cache />`标签
