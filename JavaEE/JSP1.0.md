# JSP 学习 1.0
### JSP 指令
- page指令
  - 格式<%@ page 属性1="属性值1" 属性2="属性值2" %>
  - 属性 language：指定jsp页面的脚本语言，默认值： java
  - 属性 import： 导入使用到的类文件，默认值：无
  - 属性 contentType： 指定jsp页面的编码方式，默认值：text/html,ISO-8859-1 (不支持中文)
- include指令
- taglib指令
### JSP 注释
- html注释
  - `<!--注释-->`
  - 客户端可见
- jsp注释
  - `<%--注释--%>`
  - 客户端不可见
- jsp脚本注释
  - `//单行注释`
  - `/*多行注释*/`
  - 客户端不可见
### JSP 脚本
`<% Java代码  %>`
### JSP 声明
- `<%! Java代码  %>`
- 用来定变量和方法
### JSP 表达式
- `<%= 表达式 %>`
- 注意：表达式不以分号结束
### JSP内置对象
- out
out对象是 JspWriter 类的实例
- request
request是 HttpServletRequest 类的实例
- response
HttpServletResponse 类的实例
- session
session对象是 HttpSession 的实例
- application
application 对象是 ServletContext 接口的实例
- page
java.lang.Object 类的实例
- pageContext
pageContext 类的实例
- exception
exception 是 java.lang.Throwable 的对象
- config

### 请求分派与请求重定向的区别
- 请求重定向：客户端行为，`response.sendRedirect()` , 从本质上讲等同于两次请求，前一次的请求对象不会保存，地址栏的 URL 地址会改变
- 请求分派：服务器行为，`request.getRequestDispather().forward(req , resp) ;` 是一次请求，转发后请求对象会保存，地址栏的 URL 地址不会改变 。
