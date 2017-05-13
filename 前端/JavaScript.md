# JavaScript 笔记
### 基础
- HTML 插入 js 代码
```
<script>js code</script>
```
- HTML 中导入外部 js 文件
```
<script src="script_name.js"></script>
```
js 文件中的内容不需要`<script></script>`
- JS 在页面中的位置
  - 放在`<head>`部分
  > 浏览器解析head部分就会执行这个代码，然后才解析页面的其余部分。
  - 放在`<body>`部分
  > JavaScript代码在网页读取到该语句的时候就会执行。
- 注释
> 分为单行注释和多行注释，和 Java 一样
- 变量
 ```
var 变量名;//定义变量
//*变量名称规则和 Java 基本相同
//*区分大小写
```
- 函数
```
function 函数名(){
    code;
}
```
- 输出
```
document.write(字符串或变量); //使用方法基本等于 Java 的 print()
```
- 警告
```
alert(); //与 document.write() 相似
```
- 确认
> 在浏览器页面弹出一个确认窗口，让用户选择是与否
```
confirm(); //与 document.write() 相似
//返回值: Boolean值
//当用户点击"确定"按钮时，返回true
//当用户点击"取消"按钮时，返回false
```
- 提问
```
prompt(str1, str2);
//str1: 要显示在消息对话框中的文本，不可修改
//str2：文本框中的内容，可以修改
//返回值：
//点击确定按钮，文本框中的内容将作为函数返回值
//点击取消按钮，将返回null
```
- 打开新窗口
```
window.open([URL], [窗口名称], [参数字符串])
```
  - URL:地址<br />
  - 窗口名称：可选参数，被打开窗口的名称。
   - 该名称由字母、数字和下划线字符组成。
   - "_top"、"_blank"、"_self"具有特殊意义的名称。
       - _blank：在新窗口显示目标网页
       - _self：在当前窗口显示目标网页
       - _top：框架网页中在上部窗口中显示目标网页
  - 参数字符串：可选参数，设置窗口参数，各参数用逗号隔开。![参数表](http://img.mukewang.com/52e3677900013d6a05020261.jpg)
- 关闭窗口
```
window.close(); //关闭本窗口
窗口对象.close();   //关闭指定的窗口
```
- 通过ID获取元素
```
document.getElementById(“id”);
//返回:null或[object HTMLParagraphElement]
```
- innerHTML 属性
> 用于获取或替换 HTML 元素的内容

  ```
  Object.innerHTML  //Object是元素对象
  ```
- 改变 HTML 样式
```
Object.style.property="new style";
//Object:获取的元素对象
//property:CSS 属性
//*注意*：JS中调用样式时，使用连字符的属性名称需要改为驼峰式的名称才能正常使用，如mychar.style.backgroundColor，css中的background-color要更改为backgroundColor，去连字符，第二个单词首字母大写。
```
- 显示和隐藏
```
Object.style.display = "value";
//value=none   隐藏
//value=block  显示为块级元素
```
- 控制类名
> className 属性设置或返回元素的class 属性
```
object.className = "classname";
作用:
1.获取元素的class 属性
2.为网页内的某个元素指定一个css样式来更改该元素的外观
```
- 数组
  - 创建数组 `var myarr=new Array();`
  - 初始化数值： `var myarray = new Array(66,80,90,77,59);` 或 `var myarray = [66,80,90,77,59];`
  - 数组长度 `myarr.length` 。 注意 js 数组随内容的个数可变。
  - 二维数组的两种创建方式
  ```
  1.
  var myarr=new Array();  //先声明一维
  for(var i=0;i<2;i++){   //一维长度为2
    myarr[i]=new Array();  //再声明二维
    for(var j=0;j<3;j++){   //二维长度为3
    myarr[i][j]=i+j;   // 赋值，每个数组元素的值为i+j}}
  2.
  var Myarr = [[0 , 1 , 2 ],[1 , 2 , 3]]
  //赋值和 Java 一样
  ```

### 事件响应
> 事件是可以被 JavaScript 侦测到的行为

- 鼠标单击事件( onclick ）
- 鼠标经过事件（onmouseover）
- 鼠标移开事件（onmouseout）
- 光标聚焦事件（onfocus）
- 失焦事件（onblur）
- 内容选中事件（onselect）:当文本框或者文本域中的文字被选中时，触发onselect事件。
- 文本框内容改变事件（onchange）:通过改变文本框的内容来触发onchange事件,注意要文本框失焦后事件才会触发。
- 加载事件（onload）：事件会在页面加载完成后，立即发生。
  - 注意：
  - 1.加载页面时，触发onload事件，事件写在 `<body>` 标签内。
  - 2.加载页面，可理解为打开一个新页面时。
- 卸载事件（onunload）:当用户退出页面时（页面关闭、页面刷新等），触发onUnload事件。

### JavaScript 内置对象
- Date 日期对象
```
var date_name=new Date(); //初始值为当前电脑系统时间
也可以自定初始值：
var date_name = new Date(2017,5,8); //2017年5月8日
var date_name = new Date('May 8,2017'); //2017年5月8日
```
    使用方法设置时间：<br />
    - 设置/返回年份：`set/getFullYear()`
    - 返回星期：`getDay()` 返回0-6的数字，0代表星期日。
    - 返回/设置时间方法 ：`get/setTime()` 注意单位是毫秒数，计算从 1970 年 1 月 1 日零时到日期对象所指的日期的毫秒数。
- String 字符串对象
  - length 属性：`stringObject.length;` 返回该字符串的长度。
  - `charAt()方法` 可返回指定位置的字符
  - `indexOf()方法` 返回指定的字符串值在字符串中首次出现的位置。<br />`stringObject.indexOf(substring, startpos); //startpos指定开始查找的位置，可选项。 `
- Array 数组对象
  - 数组定义
  ```
  1. 定义了一个空数组:
  var  数组名= new Array();
  2. 定义时指定有n个空元素的数组：
  var 数组名 =new Array(n);
  3.定义数组的时候，直接初始化数据：
  var  数组名 = [<元素1>, <元素2>, <元素3>...];
  ```
### 浏览器对象
- window 对象
  - 计时器
    - 间隔性触发计时器：每隔一定的时间间隔就触发一次。
    - 一次性计时器：仅在指定的延迟时间之后触发一次。
      ```
      1.
      setInterval(代码,交互时间);
      //在执行时,从载入页面后每隔指定的时间（单位毫秒）执行代码。
      //返回值：一个可以传递给 clearInterval() 从而取消对"代码"的周期性执行的值。
      clearInterval(id_of_setInterval);
      //停止计时器
      //id_of_setInterval：由 setInterval() 返回的 ID 值。
      2.
      setTimeout(代码,延迟时间);
      //在载入后延迟指定时间后,去执行一次表达式,仅执行一次。
      clearTimeout(id_of_setTimeout);
      //停止计时器
      ```
- History 对象
> history对象记录了用户曾经浏览过的页面(URL)，并可以实现浏览器前进与后退相似导航的功能。从窗口被打开的那一刻开始记录，每个浏览器窗口、每个标签页乃至每个框架，都有自己的history对象与特定的window对象关联。

  - 语法：`window.history.[属性|方法]`
  - 属性 `length`：返回浏览器历史列表 URL 的数目。
  - 方法
    - `back()` 加载 history 列表的前一个 URL，back()相当于go(-1)。
    - `forward()` 加载 history 列表的下一个 URL，forward()相当于go(1)。
    - `go()` 加载 history 列表的某个具体的页面
- Location 对象
> location用于获取或设置窗体的URL，并且可以用于解析URL。

  - 语法：`location.[属性|方法]`
  - 属性结构<br />![属性结构](http://img.mukewang.com/53605c5a0001b26909900216.jpg)
  - 属性<br />![属性](http://img.mukewang.com/5354b1d00001c4ec06220271.jpg)
  - 方法<br />![方法](http://img.mukewang.com/5354b1eb00016a2405170126.jpg)
- Navigator 对象
> Navigator 对象包含有关浏览器的信息，通常用于检测浏览器与操作系统的版本。

  - 对象属性<br />![属性](http://img.mukewang.com/5354cff70001428b06880190.jpg)
  - 语法：`navigator.[属性]`
- screen 对象
>  用于获取用户的屏幕信息。

  - 语法：`window.screen.属性`
  - 属性<br />![属性](http://img.mukewang.com/5354d2810001a47706210213.jpg)

### DOM 对象
