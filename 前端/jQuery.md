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
### jQuery HTML
- 获得内容和属性
  - text() 设置或返回所选元素的文本内容
  - html() 设置或返回所选元素的内容（包括 HTML 标记）
  - val()  设置或返回表单字段的值
  - attr() 获取或设置属性值
  ```
  $("#btn1").click(function(){
    alert("Text: " + $("#test").text());
    alert("HTML: " + $("#test").html());
    alert("Value: " + $("#test").val());
    alert($("#w3s").attr("href"));
  });
  ```
- 设置内容和属性
  - 四个方法同上
  - 栗子：

  ```
  $("#btn1").click(function(){
  $("#test1").text("Hello world!");
  $("#test2").html("<b>Hello world!</b>");
  $("#test3").val("Dolly Duck");
  $("#w3s").attr("href","http://www.w3school.com.cn/jquery");
  });

  //attr() 方法也允许同时设置多个属性
  $("button").click(function(){
  $("#w3s").attr({
    "href" : "http://www.w3school.com.cn/jquery",
    "title" : "W3School jQuery Tutorial"
    });
  });
  ```
- 添加元素
  - append() ： 在被选元素的结尾插入内容
  - prepend() ： 在被选元素的开头插入内容
  - after() ： 在被选元素之后插入内容
  - before() ： 在被选元素之前插入内容
  - 高级用法--用以添加 HTML 标签
  ```
  function appendText()
  {
  var txt1="<p>Text.</p>";              // 以 HTML 创建新元素
  var txt2=$("<p></p>").text("Text.");  // 以 jQuery 创建新元素
  var txt3=document.createElement("p"); // 以 DOM 创建新元素
  txt3.innerHTML="Text.";
  $("p").append(txt1,txt2,txt3);        // 追加新元素
  }
  ```
- 删除元素
  - remove()：删除被选元素（及其子元素）
    - remove() 方法也可接受一个参数，允许您对被删元素进行过滤。
    - `$("p").remove(".italic"); //删除 class="italic" 的所有 <p> 元素`
  - empty()： 从被选元素中删除子元素
- 获取并设置 CSS 类
  - addClass()  向被选元素添加一个或多个类
    - 可以在 addClass() 方法中规定多个类：`$("#div1").addClass("important blue");`
  - removeClass()  从被选元素删除一个或多个类
  - toggleClass()  对被选元素进行添加/删除类的切换操作
  - css()  设置或返回样式属性:具体下面介绍
- jQuery-css() 方法
> css() 方法设置或返回被选元素的一个或多个样式属性

  - 返回指定的 CSS 属性的值: `css("propertyname");`
  - 设置指定的 CSS 属性: `css("propertyname","value");`
  - 设置多个 CSS 属性: `css({"propertyname":"value","propertyname":"value",...});`
- 尺寸
> 没有参数时，返回元素的宽度/高度；有参数时，设置元素的宽度/高度。

  - width() 方法设置或返回元素的宽度（不包括内边距、边框或外边距）。
  - height() 方法设置或返回元素的高度（不包括内边距、边框或外边距）。
  - innerWidth() 方法返回元素的宽度（包括内边距）。
  - innerHeight() 方法返回元素的高度（包括内边距）。
  - outerWidth() 方法返回元素的宽度（包括内边距和边框）。
  - outerHeight() 方法返回元素的高度（包括内边距和边框）。
  - outerWidth(true) 方法返回元素的宽度（包括内边距、边框和外边距）。
  - outerHeight(true) 方法返回元素的高度（包括内边距、边框和外边距）。

### jQuery 遍历
- 祖先
  - parent() 方法返回被选元素的直接父元素。
  - parents() 方法返回被选元素的所有祖先元素，它一路向上直到文档的根元素 (`<html>`)。
    - 可以使用可选参数来过滤对祖先元素的搜索 `$("span").parents("ul");`
  - parentsUntil() 方法返回介于两个给定元素之间的所有祖先元素。 `$("span").parentsUntil("div");`
- 后代
  - children() 方法返回被选元素的所有直接子元素。
    - 可以使用可选参数来过滤对子元素的搜索  `$("div").children("p.1"); //返回类名为 "1" 的所有 <p> 元素，并且它们是 <div> 的直接子元素`
  - find() 方法返回被选元素的后代元素，一路向下直到最后一个后代。
    - 下面的例子返回属于 `<div>` 后代的所有 `<span>` 元素
      ```
      $(document).ready(function(){
        $("div").find("span");
      });
      ```
    - 下面的例子返回 `<div>` 的所有后代
      ```
      $(document).ready(function(){
        $("div").find("*");
      });
      ```
- 同胞
  - siblings() 方法返回被选元素的所有同胞元素。
    ```
    $(document).ready(function(){
      $("h2").siblings();  //返回 <h2> 的所有同胞元素
       $("h2").siblings("p"); //返回属于 <h2> 的同胞元素的所有 <p> 元素
    });
    ```
  - next() 方法返回被选元素的下一个同胞元素。
    ```
    $(document).ready(function(){
      $("h2").next();
    });
    ```
  - nextAll() 方法返回被选元素的所有跟随的同胞元素。
    ```
    $(document).ready(function(){
      $("h2").nextAll();
    });
    ```
  - nextUntil() 方法返回介于两个给定参数之间的所有跟随的同胞元素。
    ```
    $(document).ready(function(){
      $("h2").nextUntil("h6");  //返回介于 <h2> 与 <h6> 元素之间的所有同胞元素，不包括 <h6>
    });
    ```
  - prev(), prevAll() 以及 prevUntil() 方法的工作方式与上面的方法类似，只不过方向相反而已：它们返回的是前面的同胞元素（在 DOM 树中沿着同胞元素向后遍历，而不是向前）。
- 过滤
- first() 方法返回被选元素的首个元素
  ```
  $(document).ready(function(){
    $("div p").first();  //选取首个 <div> 元素内部的第一个 <p> 元素
  });
  ```
- last() 方法返回被选元素的最后一个元素
- eq() 方法返回被选元素中带有指定索引号的元素,索引号从 0 开始，因此首个元素的索引号是 0 而不是 1。
  ```
  $(document).ready(function(){
    $("p").eq(1); //选取第二个 <p> 元素
  });
  ```
- filter() 方法允许您规定一个标准。不匹配这个标准的元素会被从集合中删除，匹配的元素会被返回
  ```
  $(document).ready(function(){
    $("p").filter(".intro"); //返回带有类名 "intro" 的所有 <p> 元素
  });
  ```
- not() 方法返回不匹配标准的所有元素，与 filter() 相反
