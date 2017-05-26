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

### jQuery 效果
- 隐藏/显示
  ```
  $(selector).hide(speed,callback); //speed 参数规定隐藏/显示的速度，可以取以下值："slow"、"fast" 或毫秒。
  $(selector).show(speed,callback); //callback 参数是隐藏或显示完成后所执行的函数名称。
  $(selector).toggle(speed,callback);//用来切换 show() 和 hide() 方法
  ```
- 淡入淡出-Fading 方法
  - fadeIn() : `$(selector).fadeIn(speed,callback);`<br />
    用于淡入已隐藏的元素
  - fadeOut() : `$(selector).fadeOut(speed,callback);`<br />
    用于淡出可见元素
  - fadeToggle() : `$(selector).fadeToggle(speed,callback);`<br />
    在 fadeIn() 与 fadeOut() 方法之间进行切换
  - fadeTo() : `$(selector).fadeTo(speed,opacity,callback);`<br />
    允许渐变为给定的不透明度（值介于 0 与 1 之间）
- 滑动
  - slideDown()
    - 用于向下滑动元素
    - 语法:`$(selector).slideDown(speed,callback);`
  - slideUp()
    - 用于向上滑动元素
    - 语法:`$(selector).slideUp(speed,callback);`
  - slideToggle()
    - 在 slideDown() 与 slideUp() 方法之间进行切换
    - 语法:`$(selector).slideToggle(speed,callback);`
- 动画
> jQuery animate() 方法用于创建自定义动画

  - `$(selector).animate({params},speed,callback);`
  - 必需的 params 参数定义形成动画的 CSS 属性，注意 CSS 样式的格式。
  - 注意：默认地，所有 HTML 元素都有一个静态位置，且无法移动。如需对位置进行操作，要记得首先把元素的 CSS position 属性设置为 relative、fixed 或 absolute 。
- 停止动画
> jQuery stop() 方法用于停止动画或效果，在它们完成之前。

  - `$(selector).stop(stopAll,goToEnd);`
  - 可选的 stopAll 参数规定是否应该清除动画队列。默认是 false，即仅停止活动的动画，允许任何排入队列的动画向后执行。
  - 可选的 goToEnd 参数规定是否立即完成当前动画。默认是 false。
- Chaining
> Chaining 允许我们在一条语句中允许多个 jQuery 方法（在相同的元素上）。

  下面的例子把 css(), slideUp(), and slideDown() 链接在一起。"p1" 元素首先会变为红色，然后向上滑动，然后向下滑动
  ```
  $("#p1").css("color","red").slideUp(2000).slideDown(2000);
  ```
  提示：当进行链接时，代码行会变得很差。不过，jQuery 在语法上不是很严格；您可以按照希望的格式来写，包含折行和缩进。
  ```
  $("#p1").css("color","red")
  .slideUp(2000)
  .slideDown(2000);
  ```
