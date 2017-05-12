# JSP学习 2.0
# Javabeans
> Javabeans 就是符合某种特定的规范的 Java 类。使用 Javabeans 的好处是解决代码重复编写，减少代码冗余，功能分区明确，提高了代码的维护性。

### Javabeans设计原则

- 公有类
- 无参的公有构造方法
- 属性私有
- getter和setter方法

### JSP动作元素

> 动作元素为请求处理阶段提供信息。动作元素遵循 XML 元素的语法，有一个包含元素名的开始标签，可以有属性，可选的内容、与开始标签匹配的结束标签。

JSP动作元素包含 5 类

- 第一类是与存取 Javabeans 有关的
     ```
     <jsp:uesBean> <jsp:setProperty> <jsp:getProperty>
     ```
- 第二类是 JSP1.2 就开始有的基本元素
     ```
     <jsp:include> <jsp:forward> <jsp:param>
     <jsp:plugin> <jsp:params> <jsp:fallback>
     ```
- 第三类是 JSP2.0 新增加的元素，主要与 JSP Document 有关
    ```
    <jsp:root> <jsp:declaration> <jsp:scriptlet>
    <jsp:expression> <jsp:text> <jsp:output>
    ```
- 第四类是 JSP2.0 新增加的动作元素，主要是用来动态生成 XML 元素标签的值
    ```
    <jsp:attribute> <jsp:body> <jsp:element>
    ```
- 第五类是 JSP2.0 新增加的动作元素，主要是用在 Tag File 中，有两个元素
    ```
    <jsp:invoke> <jsp:dobody>
    ```  
###  在 JSP 中使用 Javabeans

1. 像使用普通 Java 类一样，创建 Javabean 实例。
2. 在 JSP 页面中通常使用 JSP 动作标签来使用 Javabean。
    1. useBeans 动作
    
    `<jsp:useBean id="标示符" class="Java类名" scope="作用范围" />`

    2. setProperty 动作
    > 设置对象的属性值
    
    ```
    <jsp:setProperty name="Javabean实例名" property="*" />(跟表单关联)
    <jsp:setProperty name="Javabean实例名" property="Javabean属性名" />(跟表单关联)
    <jsp:setProperty name="Javabean实例名" property="Javabean属性名" value="BeanValue" />(手工设置)
    <jsp:setProperty name="Javabean实例名" property="propertyName" param="request对象中的参数名" />(跟request参数关联）
    ```
    
    3. getProperty 动作
    > 获取对象的属性值
    
    ```
    <jsp:getProperty name="Javabean实例名" property="属性名" />
    ```
### Javabean的四个作用域范围

> 说明：使用 useBean 的 scope 属性可以用来指定 Javabean 的作用范围

- page：仅在当前页面有效
- request：可以通过HttpRequest.getAttribute() 方法取得 Javabean 对象
- session：可以通过HttpSession.getAttribute() 方法取得 Javabean 对象
- application：可以通过application.getAttribute() 方法取得 Javabean 对象


### Model1 模型

![Model1](http://note.youdao.com/yws/api/personal/file/A24B52000C8B4D7B9F8E83C320404E00?method=download&shareKey=69ac5c29d80c01ff7ec7e2b52c8ab067)


---

# JSP 状态管理

> http 协议无法保存用户状态，我们称为 http 无状态协议。为了解决这个问题，我们需要一些机制来保存用户状态： Session 和 Cookie

### Cookie

> Cookie 是 web 服务器保存在客户端的一系列文本信息，可以判断用户登录状态、“购物车”处理。

- 创建 Cookie 对象

    ` Cookie newCookie = new Cookie( String key, Object value );`
    
- 写入 Cookie 对象

    ` response.addCookie( newCookie );`

- 读取 Cookie 对象

    ` Cookie[] cookies = request.getCookies();`

- Cookie 其他的常用方法

    ```
    void setMaxAge( int expiry )  //设置 cookie 的有效期，以秒为单位
    void setValue( String value ) //在 cookie 创建后，对 cookie 进行赋值
    String getName()              //获取 cookie 的名称
    String getValue()             //获取 cookie 的值
    int getMaxAge()               //获取 cookie 的有效时间，以秒为单位
    ```
- 当 cookie 内保存的是中文字符时，需要进行转码，否则服务器报错。
    
    - URLDecoder 工具类可以实现转码,它位于 `java.net` 包中
    
    ```
    String username = URLEncoder.encode(request.getParameter("username"),"utf-8"); 
    username = URLDecoder.decode(c.getValue(),"utf-8");
    ```
### Session 与 Cookie 对比


session | cookie
---|---
在**服务器端**保存信息 | 在**客户端**保存信息
session中保存的是 **Object** 类型 | cookie 保存的是 **String** 类型
随会话的结束而将其存储的数据销毁 | cookie 可以**长期**保存在客户端
保存重要的信息 | 保存不重要的信息

---
# JSP 指令与动作元素

### include 指令
语法：` <%@ include file="URL" %>`
### include 动作
语法：` <jsp:include page="URL" flush="true|flase" /> `
- page 属性指包含的页面
- flush 属性指页面是否从缓冲区读取

### include 动作与 include 指令比较
项目| include 指令 | jsp:include 动作
------|------|--------
发生作用的时间| 页面转换期间（即编译期间）|请求期间
包含的内容|文件的实际内容|页面的输出
转换成的servlet|主页面和包含页面转换为一个Servlet|主页面和包含页面转换为独立的servlet
编译时间|较慢--资源必须解析|较快
执行时间|稍快|较慢--每次资源必须被解析

### forward 动作
语法： `<jsp:forward page="URL" /> ` 

等同于` request.getRequestDispatcher("URL").forward(request,response); `

### param 动作
语法： `<jsp:param name="参数名" value="参数值" > `

常与`<jsp:forward>`一起使用，作为其子标签
