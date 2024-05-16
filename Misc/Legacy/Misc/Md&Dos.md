# Markdown

## Markdown插入图片

**Markdown插入图片的语法：**

```md
![Alternative text](link "optional title")
```

**注释：**

>  Alternative text：替代文本，即当图片不能正常显示的时候显示的文本。这个字段中不能有空格，如果一定要填空格可以使用`%20`代替，我一般是使用下划线代替空格~
>
>  Link：图片的本地地址，或者网络地址，这个地址最好选择相对地址，不能使用绝对地址，如果非要引用不同文件夹的文件，那么解决办法在下面~
>
>  Optional Title：鼠标悬停的时候显示的标题和文字，可以不写

**举例**

```md
![电脑桌面背景图](备选图片1.png "经典草原桌面")
```

**解释：**

```text
选择的文件名叫做“备选图片1.png”，鼠标悬停上去显示的是“经典草原桌面”

如果图片不能正常显示，就显示代替文字“电脑桌面背景图”
```

**不能使用绝对路径**

因此建议将图片文件和 **.md** 文件保存在同一个文件夹中，通过相对路径进行调用~

如果非要调用其他文件夹的图片，那就记住一个原则，就是Markdown进行文件搜寻的方式是，从 **.md** 所在的文件夹出发，然后开始路径搜寻~什么意思呢，就是一定是相对路径，绝路路径行不通~

搜寻的方式向上用 `../../`，向下用`filename/filename/`

**举例**

```text
.md 文件的路径为：/user/markdown/demo.md

图片文件 的路径为：/user/pic/test.png

调用图片的写法：![test](../../pic/test/png)
```



常见的块级元素有哪些？
​div、h1-h6、form、p、li、ol、li、dl、dt、dd、address、caption、table、tbody、td、tfoot、th、thead、tr​

以下口诀方便记忆：三大列表和表格、六大标题和表单、段落地址要分块。

<a href="javascript:;" onclick="js_method()"></a>

边缘计算、Hadoop


# Dos命令

## 相对路径和绝对路径

"." --  表示当前目录，相对路径。

".." --  代表上一层目录，相对路径。

"../../" -- 上一层目录的上一层目录，相对路径。

"/" --  根目录，绝对路径。

"D:/New folder/" --  物理路径，绝对路径。

## 路径中"`/`" "`\`" "`\\`"的区别

Unix使用斜杆/ 作为路径分隔符，而web应用最先使用在Unix系统上面，所以目前所有的网络地址都采用 斜杆/ 作为分隔符。

Windows由于使用 斜杆/ 作为DOS命令提示符的参数标志了，为了不混淆，所以采用 反斜杠\  作为路径分隔符。所以目前windows系统上的文件浏览器都是用 反斜杠\  作为路径分隔符。随着发展，DOS系统已经被淘汰了，命令提示符也用的很少，斜杆和反斜杠在大多数情况下可以互换，没有影响。

知道这个背景后，可以总结一下结论：

（1）浏览器地址栏网址使用 斜杆/ ;

（2）windows文件浏览器上使用 反斜杠\ ;

（3）出现在html url() 属性中的路径，指定的路径是网络路径，所以必须用 斜杆/ ;

```html
<div style="background-image:url(/Image/Control/title.jpg); background-repeat:repeat-x; padding:10px 10px 10px 10px"></div>
// 如果url后面用反斜杠，就不会显示任何背景
```

（4）出现在普通字符串中的路径，如果代表的是windows文件路径，则使用 斜杆/ 和 反斜杠\ 是一样的；如果代表的是网络文件路径，则必须使用 斜杆/ ;

```html
<img src=".\Image/Control/ding.jpg" /> // 本地文件路径，/ 和 \ 是等效的
<img src="./Image\Control\cai.jpg" />
<img src="http://hiphotos.baidu.com/yuhua522/pic/item/01a949c67e1023549c163df2.jpg" /> // 网络文件路径，一定要使用 斜杆/
```

（5） windows系统的地址栏能够识别单反斜杠"`\`"，而不能识别双反斜杠"`\\`"，这是系统文件系统自身的约定，路径层次使用“\”区分而不是使用“\\”来区分：
所以F:\Office\Trunk\__Out\Pro Debug\Bin\\OfficeInfo.dll这样是不正确的。
而在程序中，字符串中的“`\\`”主要是为了转义，“`\\`”转义后被理解为“`\`”,“`\`”才能够被操作系统文件系统所理解，比如用字符串表示上述路径：“`F:\\Office\\Trunk\\__Out\\Pro Debug\\Bin\\OfficeIn`可以fo.dll”，同理，如果想要表示“`\\`”，可以写作“`\\\\`”。

## 常用的dos命令

1. 查看当前目录是有什么
   `dir`	`dir d: abc2\ test2002`.

2. 切换到其他盘下:	盘符号 cd
   案例演示:	切换到c盘	`cd /D c:`

3. 切换到当前盘的其他目录下(使用相对路径和绝对路径演示)
   案例演示: `cd d:\abc2\test200 cd ..\.. \abc2\ test2004.`

4. 切换到上一级:
   案例演示:	`cd ..`

5. 切换到根目录:	`cd \`
   案例演示:	`cd \`

6. 查看指定的目录下所有的子级目录	tree

   案例演示:	`tree d:`

7. 清屏	`cls`（苍老师）

8. 退出Dos	exit

9. md、rd、copy、del、echo、type、move

```txt
命令 全称 作用
dir directory 显示文件和子目录
cd change directory 改变当前的路径
md make directory 新建一个子目录（文件夹）
rd remove directory 删除一个子目录（文件夹）
copy copy 复制文件
del delete 删除文件
ren rename 重命名
type type 显示内容
format format 格式化
diskcopy diskcopy 复制磁盘
deltree delete tree 删除整个目录（包括子目录）
mem memory 查看内存大小
chkdsk check disk 检查磁盘使用情况
sys system 制作启动盘
path path 添加程序执行路径
cls clean screen 清屏


# md = make directory(目录)
md d:\\createfile
# rd = remove directory
rd d:\\removefile
```

切换盘符
直接输入盘符+回车即可
例如：d: 回车    e: 回车   f：回车...

## win10通过端口查找对应进程

```pwsh
# netstat -ano，列出所有端口的情况
# |findstr "1900" 从找到的信息中匹配"1900"的字符串
netstat -aon | findstr "5037"
# 然后中止任务
taskkill -f -pid 14448
```


