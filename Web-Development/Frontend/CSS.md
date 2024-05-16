# CSS快速入门

## 1.规范
**规范**，`<style>`可以编写`css`的代码 · 每一个声明最好使用分号结尾
**语法**：
            选择器
            {
                声明1；
                声明2；
                声明3；
            }

```html
<style>
h1
{
    color: green;	<!--color：定义颜色-->
}
</style>
```

## 2.链接`css`文件
与上面一样，但加了一个`<link>`标签间接`css`文件，可以省去了`<style>`标签，链接代码如下：
```html
<link rel="stylesheet" href="css/style.css">
```

# css三种导入方式
## 1.行内样式(用的少)
```html
<h1 style="color: chocolate">幸福往往是摸的透彻，而敬业的心却时常隐藏</h1>
```
## 2.内部样式(修改细节）
```html
<style>
h1{
    color: green;
}
</style>
```
## 3.外部样式
### 链接式
```html
<link rel="stylesheet" href="css/style.css">
```
### 导入式(不常用，推荐使用链接式)
```html
<style>
	@import "css/style.css";
</style>
```
**Ps：**

1. 多种样式采取覆盖原则，电脑运行由上至下，前面的被后面的覆盖了。
   `css`样式使用的优先级：行内样式 > 内嵌样式 > 外部样式  (注意外部样式的link位置)
2. 首页link和import语法结构不同，前者`<link>`是html标签，只能放入html源代码中使用，后者可看作为`css`样式，作用是引入`css`样式功能。import在html使用时候需要`<style type="text/css">`标签，同时可以直接`""@import url(CSS文件路径地址);""`放如`css`文件或`css`代码里引入其它`css`文件。
   本质上两者使用选择区别不大，但为了软件中编辑布局网页html代码，一般使用link较多，也推荐使用link。

# 选择器
## 基本选择器
### 1.标签选择器
```html
<style>
  h1 {
    color: #a70505;
    background: #44a15d;
    border-radius: 24px;
  }
</style>
```
### 2.类选择器
`类选择器的格式.cLass的名称好处，可以多个标签归类，是同一个class，可以复用`
```html
<style>
    .hairu {
        color: #39ffb5;
    }
    .ruxian {
        color: #33616f;
    }
    .gangfeng {
        color: #743b79;
    }

</style>
```
### 3.Id选择器（id必须保证全局唯一）
优先级: id > class >标签
```html
#wu{
	color: #3d421f;
}
```
## 层次选择器
### 1.后代选择器
```
body p{
	background: #1e85ff;
}
```
### 2.子选择器
```
body>p{
	background: #11ee88;
}
```
### 3.相邻兄弟选择器
```html
/*二弟选择器:只有一个，相邻（向下)*/
.active+p{
	background: #ee2bd0;
}
```
### 4.通用选择器
```
/*通用兄弟选则器:当前选中元素的向下的所有兄弟元素*/
.active~p{
	background: #2000ee;
}
```
## 结构伪类选择器

### 1.E:nth-child(n) 和E:nth-last-child(n)

#### E:nth-child(n)

**E:nth-child(n)** 选择器用来定位某个父元素的一个或多个特定的子元素。其中“n”是其参数，而且可以是整数值(2,4,6)，也可以是表达式(n+1、-n+5)和关键词(odd、even)，但参数n的起始值始终是1，而不是0。也就是说，参数n的值为0时，选择器将选择不到任何匹配的元素。比如：



```css
      p:nth-child(n){border:1px solid #ccc}  表示E父元素中的第n个字节点
      p:nth-child(odd){border:1px solid #ccc}/*匹配奇数行*/
      p:nth-child(even){border:1px solid #ccc}/*匹配偶数行*/
      p:nth-child(2n){border:1px solid #ccc}/*其中n是从0开始计算*/
```

​      当“E:nth-child(n)”选择器中的n为一个表达式时，其中n是从0开始计算，当表达式的值为0或小于0的时候，不选择任何匹配的元素。

代码展示：

```text
HTNL：
<div class="dome">
   <div>div 1</div>
   <div>div 2</div>
   <div>div 3</div>
   <div>div 4</div>
   <div>div 5</div>
   <div>div 6</div>
   <div>div 7</div>
   <div>div 8</div>
</div>

CSS：

.dome div{
  border:1px solid orange;
  font-weight: bold;
}

.dome div:nth-child(2n){
  background: grey;
}
```


E:nth-child(n) 这个选择器只在父元素里面只用一种子元素好用，如果出现两种子元素，就不好用了

代码展示：

```text
HTNL：
<div class="dome">
   <div>div 1</div>
   <h2>我是h2</h2>
   <h2>我是h2</h2>
   <div>div 2</div>
   <div>div 3</div>
   <div>div 4</div>
   <div>div 5</div>
   <div>div 6</div>
   <div>div 7</div>
   <div>div 8</div>
</div>

CSS：

.dome div{
  border:1px solid orange;
  font-weight: bold;
}

.dome div:nth-last-child(2n){
  background: grey;
}
```


因为它既然满足元素为div，又要满足2n，才会显示grey背景。

这个问题 就需要用E:nth-of-type(n) 来解决。

#### E:nth-last-child(n)

**E:nth-last-child(n)** 选择器和前面的**E:nth-child(n)**选择器非常的相似，只是这里多了一个“last”，所起的作用和“E:nth-child(n)”选择器有所区别，从某父元素的最后一个子元素开始计算，来选择特定的元素。就不举例说明了。

### 2.E:nth-of-type(n)和E:nth-last-of-type(n)

#### E:nth-of-type(n)

**E:nth-of-type(n)**选择器和“E:nth-child(n)”选择器非常类似，不同的是它只计算父元素中指定的某种类型的子元素。当某个元素中的子元素不单单是同一种类型的子元素时，使用**E:nth-of-type(n)**选择器来定位于父元素中某种类型的子元素是非常方便。在**E:nth-of-type(n)**选择器中的“n”和**E:nth-child(n)**选择器中的“n”参数也一样，可以是具体的整数，也可以是表达式，还可以是关键词。

 刚才的那个例子就可以直接利用这个选择器实现，它可以只选中div元素

代码展示：

```text
.dome div:nth-of-type(2n){
  background: grey;
}
```

效果：这样就可以选出双数的div


#### E:nth-last-of-type(n)

**E:nth-last-of-type(n)**选择器和前面的**E:nth-of-type(n)**选择器非常的相似，只是这里多了一个“last”，所起的作用和“E:nth-of-type(n)”选择器有所区别，从某父元素的最后一个子元素开始计算，来选择特定的元素。就不举例说明了。

### 3.E:first-child和E:last-child

#### E:first-child

E:first-child选择器表示的是选择父元素的第一个子元素的元素E。简单点理解就是选择元素中的第一个子元素，记住是子元素，而不是后代元素。

```text
.dome div:first-child{
  background: grey;
}
```

#### E:last-child

**E:last-child**选择器与**E:first-child**选择器作用类似，不同的是**E:last-child**选择器选择的是元素的最后一个子元素。

### 4.总结

​      1.通用子元素过滤器：E:nth-child(n)（顺序过滤）和E:nth-last-child(n)(逆序过滤)

​      2.通用子类型元素过滤器：E:nth-of-type（顺序过滤）和E:nth-last-of-type(n)(逆序过滤)

​      3.特定位置的子元素：E:first-child,E:last-child,E:first-of-type,E:last-of-type

​      4.特定状态的元素：E:root（根节点）、E:only-child（独子元素）、E:only-of-type（独子类型元素）和E:empty（孤节点）

```html
ul li:first-child{
	background: #ee22ad;
}

ul li:last-child{
	background: #2f5897;
}

p:nth-child(3){
	background: #9adb30;
}

p:nth-of-type(2){
	background: #ee3400;
}

a:hover{
	background: #c51dee;
}
```
## 属性选择器
属性名，属性名=属性值（正则）
=	绝对等于
*=	包含这个元素
^=	以这个开头
$=	以这个结尾
# 美化页面元素
## 1.字体样式
```html
body {
font-family: "Agency FB", 楷体;
color: #4691ff;
}

h1 {
font-size: 50px;
}

p1 {
font-weight: bold;
}
```
## 2.文本样式

1. 颜色
1. 文本对齐的方式
1. 首行缩进
1. 行高
1. 装饰
## 3.超链接伪类
正常只用a，a：active
```html
<style>
/*默认的颜色*/a{
text-decoration: none;color: #000;
}
*鼠标悬浮的状态（只需要记住:hover)*/
a: hover{
  color: orange;font-size: 50px;
}
/*鼠标按住未释放的状态*/
a:active{
color:green;
}
a:visited{
color:#ff008a;
}
/*text-shadow:阴影颜色，水平偏移，垂直偏移，阴影半径*/
#price{
text-shadow : #3cc7f5 10px 0px 2px;
}
</style>
```
## 4.列表
**list-style:**
_none_去掉原点
_circle_空心圆
_decimal_数字
_square_正方形

```html
#nav{
    width: 300px;
    background: #a0a0a0;
}
.title {
    font-size: 18px;
    font-weight: bold;
    text-indent: 1em;
    line-height: 35px;
    background: red;
}

/*ul li*/
ul{
    background: #a0a0a0;
}

ul li{
    height: 30px;
    list-style: none;
    text-indent: 1em;
}

a{
    text-decoration: none;
    font-size: 14px;
    color: #008;
}

a:hover{
    color: orange;
    text-decoration: underline;
}

```
## 5.背景

```html
<style>
  div {
    width: 1000px;
    height: 700px;
    border: 1px solid red;
    background-image: url("images/1.jpg")
      /*默认是全部平铺的repeat*/
  }

  .div1 {
    background-repeat: repeat-x;
  }

  .div2 {
    background-repeat: repeat-y;
  }

  .div3 {
    background-repeat: no-repeat;
  }
</style>
```
## 6.渐变
```css
background-color:#21D4FD;
background-image: linear-gradient(19deg, #21D4FD 0%, #B721FF 100%);
```
# 盒子模型
## 边框（border）
```css
<style>
/*body.总有一个默认的外边距margin: 0.常见操作*/
  h1, ul, li, a, body {
    margin: 0;
    padding: 0;
    text-decoration: none;
    }
/*border:粗细，样式，颜色*/
    #box{
        width:300px;
        border:1px solid red;
    }
    form{
        background: #3cbda6;
    }
    h2{
      font-size: 16px;
      background-color: #3cbda6;
      line-height: 30px;
    }
    form{
      background: #3cbda6;
    }
    div:nth-of-type(1) input {
      border: 3px solid black;
    }
    div:nth-of-type(2) input {
      border: 3px dashed #4d0b8c;
    }
    div:nth-of-type(2) input {
      border: 2px dashed #008c27;
    }

</style>
```
## 内外边距（padding，margin）
margin四个参数的时候是上右下左(顺时针)

## 圆角边框
```css
<style>
div{
  width: 100px;
  height: 100px;
  border: 10px solid red;
  border-radius: 100px;
}
</style>
```
## 阴影
margin：0 auto；	居中
要求：块元素，块元素有固定的宽度
```css
<style>
div {
  width: 100px;
  height: 100px;
  border: 10px solid red;
  border-radius: 50px;
  box-shadow: 10px 10px 100px yellow;
}
</style>
```
# 浮动
## 1.开头
块级元素:独占一行
`h1~h6  p  div 列表...`
行内元素:不独占一行
`span  a  img  strong...`
行内元素可以被包含在块级元素中，反之，则不可以
## 2.display
```css
<style>
div{
  width: 100px;
  height: 100px;
  border: 1px solid red;
  display: none;
}

span{
  width: 100px;
  height: 100px;
  border: 1px solid red;
  display: inline-block;
}
</style>
```

- 这个也是一种实现行内元素排列的方式，但是我们很多情况都是用float
## 3.float
```css
div {
    margin: 10px;padding : 5px;
}
#father {
    border : 1px #000 solid;
}
.layer01 {
    border: 1px #F00 dashed;
    display: inline-block;
    float: right;
}
.layer02 {
    border: 1px #00F dashed;
    display: inline-block;
    float: right;
}
.layer03 {
    border: 1px #060 dashed;
    display: inline-block;
    float: right;
}
.layer04 {
    border : 1px #666 dashed;
    font-size: 12px;
    line-height: 23px;
    display:inline-block;
    float: right;
}
```
## 4.父级边框塌陷问题
**clear**
```css
clear: right;	右侧不允许有浮动元素
clear: left;	左侧不允许有浮动元素
clear: both;	两侧不允许有浮动元素
clear: none;
```
解决方案

1. 增加父级元素的高度
```css
#father{
border : 1px #000 solid;
height: 800px;
}
```

2. 增加一个空的div标签，清除浮动
```css
<div class="clear"></div>

.clear{
		clear:both;
		margin : 0;
		padding: 0;
}
```

3. overflow
```css
在父级元素中增加一个	overf1ow: hidden;
```

4. 父类添加一个伪类: after
```css
#father:after{
		content: '';
	  display: b1ock;
  	clear: both;
}
```
**小结:**

1. 浮动元素后面增加空div简单，代码中尽量避免空div
1. 设置父元素的高度

简单，元素假设有了固定的高度，就会被限制

3.  overflow

简单，下拉的一些场景避免使用

4. 父类添加一个伪类: after(推荐)

写法稍微复杂一点，但是没有副作用，推荐使用
## 对比

- display

方向不可以控制

-  float

浮动起来的话会脱离标准文档流，所以要解决父级边框塌陷的问题

# 定位
## 1.相对定位
相对定位:position: relative;
相对于原来的位置，进行指定的偏移，相对定位的话，它任然在标准文档流中!
```css
top: -20px;
left: 20px;
bottom: -10px;
right: 20px;
```
## 2.绝对定位

## 3.z-index

