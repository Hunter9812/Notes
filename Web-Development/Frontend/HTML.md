## 初识HTML

1. 全称HTML： Hyper Text Markup Language (超文本标记语言)

2. W3C（World Wide Web Consortiun<万维网联盟>）

    其标准:>结构化标准语言(HTML、XML)

   ​		 	\>表现标准语言(css)
   ​		 	\>行为标准(DOM、ECMAScript )

3基本结构

```html
<html>

<head>

<title>我的第一个网页</title>

<!--网页头部-->

</head>

<body>

<!--我的第一个网页/

主体部分-->

</body>

</html>
```

> <body>、</body>等成对的标签，分别叫﻿开放标签﻿和﻿闭合标签﻿单独呈现的标签(空元素),如<hr/>:意为用/来关闭空元素 。

## 标签



### 1、基本标签

####  1.标题标签



<h1>一级标签</h1> <h2>二级标签</h2> <h3>三级标签</h3> <h4>四级标签</h4> <h5>五级标签</h5> <h6>六级标签</h6>

#### 2.段落标签

<p> </p>

#### 3.换行标签

<br/>

#### 4.水平线标签

<hr/>

#### 5.字体样式标签

斜体：<em>斜体 </em>

粗体：<strong>粗体</strong>

#### 6.注释及特殊符号

注释： <!--标签学习-->

特殊符号:

空格：`&nbsp;`

大于号：`&gt;`

小于号：`&lt;`

版权符号：`&copy;`

###  2、图像标签

1. <img>

src ：图片地址(相对地址,绝对地址)；（必填）

../：表示上一级目录；

alt：未加载出图像时所显示的文本；（必填）

title：悬停文字；

width,height：设置图像尺寸；

###  3、超链接标签

#### 1. 链接

<a href="A">B</ a>

href :必填,表示要跳转到那个页面

A：所要填写的网址；B：代表网址的文字，也可插入图像；

target（其表示窗口在哪里打开）

_blank：在新标签中打开；

_self：在自己的网页中打开；

#### 2. 锚链接

<1>需要一个锚标记 ；

<2>跳转到标记；

使用name作为标记：<a name="top">顶部</a>

锚链接比普通的多一个#：<a href="#	">	</ a>

#### 3. 功能性链接邮件链接

mailto：<a href="mailto:xxxxxxxxqq.com">文本< / a>

QQ链接：QQ推广

####  4. 行内元素和块元素

**1)块元素**

◆无论内容多少，该元素独占一行

(p、h1-h6...)|

**2)行内元素**

◆内容撑开宽度﹐左右都是行内元素的可以在排在一行

( a . strong . em ... )

#### 5. 列表标签

**1)有序列表**：<ol></ol>；<li></li>；

```html
<ol start="100">
  <li>John</li>
  <li>Kelly</li>
  <li>Linda</li>
  <li>Frederic</li>
  <li>Sam</li>
</ol>
<!--
reversed	规定列表顺序为降序。(9,8,7...)
start			规定有序列表的起始值。
type			规定在列表中使用的标记类型。
1  A  a  I  i
-->
```

**2)无序列表**：<ul></ul>；<li></li>；

```html
<ul style="list-style-type: square">
    <li>服装鞋帽</li>
    <li>数码家电</li>
    <li>运动户外</li>
    <li>孕婴用品</li>
    <li>厨卫家居</li>
</ul>
<!--
none				不使用项目符号
disc				实心圆，默认值
circle			空心圆
square			实心方块
decimal			阿拉伯数字
lower-roman	小写罗马数字
upper-roman	大写罗马数字
lower-alpha	小写英文字母
upper-alpha	大写英文字母
-->
```

**3)自定义列表**：<dl></dl>；<dt></dt>；<dd></dd>；

dl :标签	dt :列表名称	dd :列表内容

#### 6. 表格标签

table：表格 ；caption：标题；tr：行；td：列；colspan：跨列；rowspan：跨行；

```html
<table border="1px">；

<td colspan="2"> </td>;

<td rowspan="2">1-2</td>；
```

## 媒体元素

音频和视频

src ：资源路径；

controls：控制条；（音频要加上进度条，否则一片白）

autoplay ：自动播放；

```html
<video src=""></video>
<audio src=""></audio>
```

##  页面结构分析

| 元素名      | 描述                                              |
| ----------- | ------------------------------------------------- |
| **header**  | 标题头部区域的内容(用于页面或页面中的一块区域)    |
| **footer**  | 标记脚部区域的内容（用于整个页面或页面的一块区域) |
| **section** | Web页面中的一块独立区域                           |
| **article** | 独立的文章内容                                    |
| **aside**   | 相关内容或应用（常用于侧边栏)                     |
| **nav**     | 导航类辅助内容                                    |

##  表单

```html
<!--表单form
action :表单提交的位置,可以是网站,也可以是一个请求处理地址
method : post , get提交方式
get方式提交:我们可以在url中看到我们提交的信息，不安全，高效
post :比较安全,传输大文件.
-->


<form action="1.我的第一个网页.html" method="post">

    <!---文本输入框: input type="text"
    value="洪荒之力"    默认初始值
    maxlength="8"     最长能写几个字符
    size="30"         文本框的长度
    -->
    <p>名字：<input type="text" name="username" value="洪荒之力" maxlength="8" size="30"></p>

    <!--密码框: input type="password"-->
    <p>密码：<input type="password" name="code"></p>

    <!--单选框标签
    input type="radio"
    "value": 单选框的值
    "name":表示组
    -->

    <p>性别:
        <input type="radio" value="boy" name="sex" checked/>男
        <input type="radio" value="girl" name="sex"/>女
    </p>

    <!--多选框
    -->
    <p>爱好:
        <input type="checkbox" value="sleep" name="hobby">睡觉
</form>
```

