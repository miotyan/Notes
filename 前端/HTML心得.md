- 即使 `<br>` 在所有浏览器中都是有效的，但使用 `<br />` 其实是更长远的保障
- 使用小写标签
- 属性值应该始终被包括在引号内。双引号是最常用的，不过使用单引号也没有问题。
在某些个别的情况下，比如属性值本身就含有双引号，那么您必须使用单引号，例如：
`name='Bill "HelloWorld" Gates'`
- 所有连续的空格或空行都会被算作一个空格
- 废弃标签和属性

```
标签：center|font|basefont|s|strike|u
属性：align|bgcolor|color
```
- 以上废弃属性和标签所形成的样式用`style`属性代替，它能定义css样式
- pre 标签内的空格和换行不被压缩，所以可以用来显示代码

#### 如何使用样式
- 外部样式表

```
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```
- 内部样式表

```
<head>

<style type="text/css">
body {background-color: red}
p {margin-left: 20px}
</style>
</head>
```
- 内联样式

```
<p style="color: red; margin-left: 20px">
This is a paragraph
</p>
```

### 杂技
- <base> 标签为页面上的所有链接规定默认地址或默认目标（target）
```
<head>
<base href="http://www.w3school.com.cn/images/" />
<base target="_blank" />
</head>
```

- 用 fieldset 组合表单数据
```
<form action="action_page.php">
<fieldset>
<legend>Personal information:</legend>
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit"></fieldset>
</form>
```

- datalist 元素
> 用户会在他们输入数据时看到预定义选项的下拉列表。

- H5 被删除元素
``` <acronym>
<applet>
<basefont>
<big>
<center>
<dir>
<font>
<frame>
<frameset>
<noframes>
<strike>
<tt>```

- 图片超链接
```
<a href="">
<img src="" />
</a>
```
[这是一个栗子](http://www.w3school.com.cn/tiy/t.asp?f=html_imglink)
