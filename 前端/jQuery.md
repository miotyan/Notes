# jQuery 学习

### 基础
- 向页面添加 jQuery 库
> jQuery 库位于一个 JavaScript 文件中，其中包含了所有的 jQuery 函数。

  ```
  <head>
  <script type="text/javascript" src="jquery.js"></script>
  </head>
  ```
- jQuery 语法<br>
  基础语法：`$(selector).action()`
  - 美元符号定义 jQuery
  - 选择符(selector) “查询”和“查找” HTML 元素
  - jQuery 的 action() 执行对元素的操作
- 文档就绪函数<br />
  为了防止文档在完全加载（就绪）之前运行 jQuery 代码, jQuery 函数都要放在下面的代码里
  ```
    $(document).ready(function(){

    --- jQuery functions go here ----

    });
  ```
- jQuery 选择器
  - 元素选择器
  <br />jQuery 使用 CSS 选择器来选取 HTML 元素。
    1. `$("p")` 选取 `<p>` 元素。
    2. `$("p.intro")` 选取所有 class="intro" 的 `<p>` 元素。
    3. `$("p#demo")` 选取所有 id="demo" 的 `<p>` 元素。
  - 属性选择器
  <br />jQuery 使用 XPath 表达式来选择带有给定属性的元素
    - `$("[href]")` 选取所有带有 href 属性的元素。
    - `$("[href='#']")` 选取所有带有 href 值等于 "#" 的元素。
    - `$("[href!='#']")` 选取所有带有 href 值不等于 "#" 的元素。
    - `$("[href$='.jpg']")` 选取所有 href 值以 ".jpg" 结尾的元素。
  - CSS 选择器
  <br />jQuery CSS 选择器可用于改变 HTML 元素的 CSS 属性。
    ```
    $("p").css("background-color","red"); //示例
    ```
  - 其他

|语法|描述|
|--|--|
|$(this)|当前 HTML 元素|
|$(ul li:first)|每个 `<ul>` 的第一个 `<li>` 元素|
|$("[href$='.jpg']")|所有带有以 ".jpg" 结尾的属性值的 href 属性|
|$("div#intro .head")	|id="intro" 的 <div> 元素中的所有 class="head" 的元素|

- jQuery 事件

|Event 函数|绑定函数至|
|---|---|
|$(document).ready(function)|将函数绑定到文档的就绪事件（当文档完成加载时）|
|$(selector).click(function)|触发或将函数绑定到被选元素的点击事件|
|$(selector).dblclick(function)|触发或将函数绑定到被选元素的双击事件|
|$(selector).focus(function)|触发或将函数绑定到被选元素的获得焦点事件|
|$(selector).mouseover(function)|触发或将函数绑定到被选元素的鼠标悬停事件|
