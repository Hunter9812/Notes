
# 一、Java入门

## 1、打印Hello World

- 安装
  - windows: [Java I tell you-爪哇我话你知](https://www.injdk.cn/)
  - linux: [sdkman](https://sdkman.io/)、archlinux自带一个java版本管理工具：archlinux-java

- 下载jdk8，配置环境文件

**配置环境变量**<br/>
编辑器：[notepad++](https://github.com/notepad-plus-plus/notepad-plus-plus/)、editplus；Sublime；IDEA；eclipse；

- 下载个Notepad++
- 编写代码
```java
public class Hello{
	public static void main(String[] args){
		System.out.print("Hello,World!");
	}
}
```

- 编译	javac java文件，生成一个class文件
- 运行	class文件，java class文件
- 显示	Hello，World!


## 2、**新建**IDEA**工程模板**

1. 选择Empty Project

![图片.png](https://cdn.nlark.com/yuque/0/2022/png/22775287/1646962902893-79071ff9-505f-4b4a-b55f-7e42cf5b90fc.png#clientId=ua945ac15-f34d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=430&id=mSs4U&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=781&originWidth=1004&originalType=binary&ratio=1&rotation=0&showTitle=false&size=59374&status=done&style=none&taskId=u8b18f22d-61e2-4af5-8856-d5ac4d358e9&title=&width=552.4000244140625)

2. 点击Project Structure

![图片.png](https://cdn.nlark.com/yuque/0/2022/png/22775287/1647223842137-311bbf81-db6c-4e7b-b77a-1a77a716afbb.png#clientId=uc5da5bb7-716e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=478&id=ubb15097b&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=598&originWidth=460&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36217&status=done&style=none&taskId=uc9c73df8-7541-4db7-87d6-921cc490fe0&title=&width=368)

3. 配置好SDK和Language level

![图片.png](https://cdn.nlark.com/yuque/0/2022/png/22775287/1646962791369-307cbef8-aeab-42dc-b329-7e388f539597.png#clientId=ua945ac15-f34d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=278&id=ESdN9&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=409&originWidth=1069&originalType=binary&ratio=1&rotation=0&showTitle=false&size=42217&status=done&style=none&taskId=u5d7e2032-c56b-4394-95b9-0b1b7930814&title=&width=727.4000244140625)

<a name="OOLix"></a>

## ps：

### 1、中文问题

若在代码中添加中文，则需将编码格式改为GBK，否则javac进行编译会报错<br />![图片.png](https://cdn.nlark.com/yuque/0/2022/png/22775287/1657442190154-c7b091e0-28a5-48bb-a99e-21d21724dcfa.png#clientId=u2b862ccc-e97d-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=114&id=u4af444f5&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=147&originWidth=610&originalType=binary&ratio=1&rotation=0&showTitle=false&size=16736&status=done&style=none&taskId=u4d9abd21-b12d-4f21-b2dc-4e708d1b36b&title=&width=473)

> 1.Java保存的文件名必须与类名一致；<br />2.如果文件中只有一个类，文件名必须与类名一致；<br />3.一个Java文件中只能有一个public类；<br />4.如果文件中不止一个类，文件名必须与public类名一致；<br />5.如果文件中不止一个类，而且没有public类，文件名可与任一类名一致。

> 什么是运行
> 1.有了可执行的java程序(Hello.class字节码文件)
> 2.通过运行工具java.exe对字节码文件进行执行,本质就是.class装载到jvm 机执行。

<a name="IiSaG"></a>

### 2、代码相关说明

> **1.Java源文件以.java为扩展名。源文件的基本组成部分是类(class)，如本类中的Hello**
> **类。**
> **2.Java应用程序的执行入口是main()方法。它有固定的书写格式:**
> **public static void main(String[] args) {...}**
> **3.Java语言严格区分大小写。**
> **4.Java方法由一条条语句构成，每个语句以“;”结束。**
> **5.大括号都是成对出现的，缺一不可。[习惯，先写再写代码]**
> **6.一个源文件中最多只能有一个public类。其它类的个数不限。[演示]**
> **7.如果源文件包含一个public类，则文件名必须按该类名命名!**
> **8.一个源文件中最多只能有一个public类。其它类的个数不限，也可以将main方法写在非**
> **public类中，然后指定运行非public类，这样入口方法就是非public的main方法**

# 二、基础语法

## 1、基本语法

1. 大小写敏感：Java 是大小写敏感的，这就意味着标识符 Hello 与 hello 是不同的。
   类名：对于所有的类来说，类名的首字母应该大写。如果类名由若干单词组成，那么每个单词的首字母应该大写，例如 MyFirstJavaClass 。
2. 方法名：所有的方法名都应该以小写字母开头。如果方法名含有若干单词，则后面的每个单词首字母大写。
3. 源文件名：源文件名必须和类名相同。当保存文件的时候，你应该使用类名作为文件名保存（切记 Java 是大小写敏感的），文件名的后缀为 .java。（如果文件名和类名不相同则会导致编译错误）。
4. 主方法入口：所有的 Java 程序由 public static void main(String[] args) 方法开始执行。

## 2、注释

```java
//单行注释
//输出一个Hello,World!

//多行注释
/*
它将输出 Hello World
这是一个多行注释的示例
*/

//文本注释	/**	*/
/**
  * @description HelloWorld
  * @Author Hunter
  */
```

## 3、标识符、关键字、修饰符

**标识符需注意：**(规则)

- ​		所有的标识符都应该以字母（A-Z 或者 a-z）,美元符（$）、或者下划线（_）开始
- ​		首字符之后可以是字母（A-Z 或者 a-z）,美元符（$）、下划线（_）或数字的任何字符组合
- ​		关键字不能用作标识符
- ​		标识符是大小写敏感的
- ​		合法标识符举例：age、$salary、_value、__1_value
- ​		非法标识符举例：123abc、-salary

**关键字需注意：**

下面列出了 Java 关键字。这些保留字不能用于常量、变量、和任何标识符的名称。

```java
private protected public default abstract class extends final implements interface native new static strictfp synchronized transient volatile break case continue default do else for if instanceof return switch while assert catch finally throw throws try import package boolean byte char double float int long short super this void goto const
```

**修饰符**

​	像其他语言一样，Java可以使用修饰符来修饰类中方法和属性。主要有两类修饰符：

- 访问控制修饰符 : default, public , protected, private
- 非访问控制修饰符 : final, abstract, static, synchronized

**标识符命名规范**

1. 包名:多单词组成时所有字母都小写: aaa.bbb.ccc//比如com.hsp.crm
2. 类名、接口名:多单词组成时，所有单词的首字母大写:XxxYyyZzz
   比如:TankShotGame
3. 变量名、方法名:多单词组成时，第一个单词首字母小写,第二个单词开始每个
   单词首字母大写:xxxYyyZzz [小驼峰]
   比如: tankShotGame
4. 常量名:所有字母都大写。多单词时每个单词用下划线连接: XXX_YYY_ZZZ
   比如:定义一个所得税率 TAX_RATE
5. 后面我们学习到类，包,接口，等时，我们的命名规范要这样遵守,更加详细的看文档.

## 4、数据类型

1. java数据类型分为两大类基本数据类型，引用类型
2. 基本数据类型有8中 数值型 [ 整数型 (byte , short , int , long ),  浮点型 (float ,double)] 字符型 char , 布尔型 boolean
3. 引用类型 [类,接口，数组]

一般地整型变量默认为 int 类型；浮点数的默认类型为 double 类型；
所以声明long类型常量须加 ‘L’ 或 ‘l’；float型后面加上“F”或‘f’；

### 1.类型默认值

下表列出了 Java 各个类型的默认值：

| **基本数据类型**       | 所占字节(byte)      | **默认值** |
| ---------------------- | ------------------- | ---------- |
| byte                   | 1（1 byte = 8 bit） | 0          |
| short                  | 2                   | 0          |
| int                    | 4                   | 0          |
| long                   | 8                   | 0L         |
| float                  | 4                   | 0.0f       |
| double                 | 8                   | 0.0d       |
| char                   | 2                   | 'u0000'    |
| String (or any object) |                     | null       |
| boolean                | 1                   | false      |

### 2.基本数据类型

#### 1）整数型

**Detail:**

1. **Java各整数类型有固定的范围和字段长度，不受具体OS[操作系统]的影响，以**
**保证java程序的可移植性。**
2. Java的整型常量（具体值）默认为int型，声明long型常量须后加火或‘L’
2. java程序中变量常声明为int型，除非不足以表示大数，才使用long
4. bit:计算机中的最小存储单位。byte:计算机中基本存储单元,1byte = 8 bit,
[二进制再详细说,简单举例一个 byte 3和short 3 ]

#### 2）浮点型

1. 关于浮点数在机器中存放形式的简单说明,浮点数=符号位+指数位+尾数位
2. 尾数部分可能丢失，造成精度损失(小数都是近似值)。

**Detail:**

1. 与整数类型类似，Java浮点类型也有固定的范围和字段长度，不受具体OS的
   影响。[float 4个字节double是8个字节]
2. Java的浮点型常量(具体值)默认为double型，声明float型常量，须后加‘f"或‘F'
3. 浮点型常量有两种表示形式
   十进制数形式 : 如 : 5.12  512.0f  .512 (必须有小数点)
   科学计数法形式 : 如 : 5.12e2 [ ]  5.12E-2 [ ]
4. 通常情况下，应该使用double型,因为它比float型更精准。[ 举例说明 ]
   double num9 = 2.1234567851;
   float num10 = 2.1234567851F;
5. 浮点数使用陷阱 : 2.7和8.1/3 比较
   得到一个重要的使用点:当我们对运算结果是小数的进行相等判断时，要小心
   应该是以两个数的差值的绝对值，在某个精度范围类判断

#### 3）字符型

**Detail:**

1. 字符常量是用单引号('')括起来的单个符。使用双引号会变成字符串，即会报错。
   例如:char c1 = 'a'; char c2 = '中'; char c3 = '9';
2. Java中还允许使用转义字符‘\′来将其后的字符转变为特殊字符型常量。
   例如:char c3 = '\n'；//  '\n' 表示换行符
3. 在java中,char的本质是一个整数，在输出时，是unicode码对应的字符。
   http://tool.chinaz.com/Tools/Unicode.aspx
4. 可以直接给char赋一个整数,然后输出时，会按照对应的unicode字符输出[97]
5. char类型是可以进行运算的,相当于一个整数，因为它都对应有Unicode码.

**字符编码表**

1. ASCII (ASCII编码表一个字节表示，一个128个字符)
2. Unicode (Unicode编码表固定大小的编码使用两个字节来表示字符，字母和汉字统一都是占用两个字节，这样浪费空间)
3. utf-8(编码表，大小可变的编码字母使用1个字节，汉字使用3个字节)gbk(可以表示汉字，而且范围广，字母使用1个字节，汉字2个字节)
4. gb2312(可以表示汉字，gb2312<gbk)
5. big5码(繁体中文,台湾，香港)

#### 4）布尔值

**使用细节说明**
不可以0或非0的整数替代false和true，这点和C语言不同

### 3.数据类型转换

#### 1）自动类型转换

**AutoConvert**

```
低  ------------------------------------>  高

byte,short,char—> int —> long—> float —> double
```

数据类型转换必须满足如下规则：

\1. 不能对boolean类型进行类型转换。

\2. 不能把对象类型转换成不相关类的对象。

\3. 在把容量大的类型转换为容量小的类型时必须使用强制类型转换。

\4. 转换过程中可能导致溢出或损失精度，例如：

```
int i =128;
byte b = (byte)i;//b=-128
```

因为 byte 类型是 8 位，最大值为127，所以当 int 强制转换为 byte 类型时，值 128 时候就会导致溢出。

\5. 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入，例如：

```
(int)23.7 == 23;
(int)-45.89f == -45
```

**Detail:**

1. 有多种类型的数据混合运算时，

   系统首先自动将所有数据转换成容量最大的那种数据类型,然后再进行计算。

2. 当我们把精度(容量)大的数据类型赋值给精度(容量)小的数据类型时，就会报错，反之就会进行自动类型转换。

3. (byte, short)和char之间不会相互自动转换。

4. byte,short, char他们三者可以计算,在计算时首先转换为int类型。

5. boolean不参与转换。

6. 自动提升原则:表达式结果的类型自动提升为操作数中最大的类型。

#### 2）强制类型转换

1. 当进行数据的大小从大——>小，就需要使用到强制转换

2. 强转符号只针对于最近的操作数有效，往往会使用小括号提升优先级

   ```java
   //int x =(int)10*3.5+6*1.5;
   int y =(int)(10*3.5+6*1.5);System.out.println(y);
   ```

3. char类型可以保存int的常量值，但并不能保存int的变量值,需要强转

   ```java
   char c1 = 100;
   int m = 100;
   char c2 = m;//错误
   char c3 = (char)m;
   System.out.println(c2);
   ```

4. byte和short类型在进行运算时，当做int类型处理。

#### 3）基本数据类型和String类型的转换

**基本类型转String类型**
语法:	将基本类型的值+" "即可

```java
//数值转字符串
Integer a = 15;
//1.使用字符串拼接
String s1 = a+"";
//2.主动调用重写的toString方法
String s2 = a.toString();
//3.被动转换, 使用String.valueOf(), 将传进去的参数变成String
String s3 = String.valueOf(a);
```

**String类型转基本数据类型**
语法:	通过基本类型的包装类调用parseXX方法即可

```java
//字符串转数值
String s = "10.9";
//1.使用BigDecimal进行操作
BigDecimal bi = new BigDecimal(s);
//2.使用Integer的parseInt方法, 返回int对象
int i = Integer.ParseInt(s);
//3.使用包装类的静态方法valueOf, 将传入参数转为包装类对象
Integer i3 = Integer.valueOf(s)
```



**Detail:**

在将String类型转成基本数据类型时，要确保String类型能够转成有效的数据，比如我们可以把"123"，转成一个整数，但是不能把"hello"转成一个整数
如果格式不正确，就会抛出异常，程序就会终止，这个问题在异常处理章节中，会处理

## 5、运算符

运算符分为算术运算符、赋值运算符、关系运算符[比较运算符]、逻辑运算符、位运算符[需要二进制基础]、三元运算符。

### 1）运算符表

| 类别     | 操作符                                     | 关联性   |
| -------- | ------------------------------------------ | -------- |
| 后缀     | () [] . (点操作符)                         | 左到右   |
| 一元     | expr++  expr--                             | 从左到右 |
| 一元     | ++expr --expr + - ～ ！                    | 从右到左 |
| 乘性     | * /％                                      | 左到右   |
| 加性     | + -                                        | 左到右   |
| 移位     | >> >>>  <<                                 | 左到右   |
| 关系     | >  >=  <  <=                               | 左到右   |
| 相等     | == !=                                      | 左到右   |
| 按位与   | ＆                                         | 左到右   |
| 按位异或 | ^                                          | 左到右   |
| 按位或   | \|                                         | 左到右   |
| 逻辑与   | &&                                         | 左到右   |
| 逻辑或   | \| \|                                      | 左到右   |
| 条件     | ？：                                       | 从右到左 |
| 赋值     | = + = - = * = / =％= >> = << =＆= ^ = \| = | 从右到左 |
| 逗号     | ，                                         | 左到右   |

### 2）进制

对于整数，有四种表示方式:

1. 二进制：0,1，满2进1。以0b或0B开头。
2. 十进制：0-9，满10进1。
3. 八进制：0-7，满8进1。以数字0开头表示。
4. 十六进制：0-9及A(10)-F(15)，满16进1。以0x或0X开头表示。此处的A-F不区
   分大小写。

### 3）位运算符



### ps：

1. **程序中 + 号的用法**

   1. 当左右两边都是数值型时,则做加法运算
   2. 当左右两边有一方为字符串,则做拼接运算
   3. 运算顺序，是从左到右

2. 在%的本质    看一个公式  a % b = a - a / b * b

   ```java
   System.out.println(10 % 3);//1
   System.out.print1n(-10 % 3);//-1
   System.out.println(10 % -3); //1
   System.out.print1n(-10 % -3);//-1
   ```

## 6、控制结构

#### 1）顺序控制

#### 2）分支控制(if ,else, switch)

#### 3）循环控制(for, while , dowhile,**多重循环**)

1. **Java 增强 for 循环**

   Java5 引入了一种主要用于数组的增强型 for 循环。

   Java 增强 for 循环语法格式如下:

   ```java
   for(声明语句 : 表达式)
   {
       //代码句子
   }
   ```

   **声明语句：**声明新的局部变量，该变量的类型必须和数组元素的类型匹配。其作用域限定在循环语句块，其值与此时数组元素的值相等。**表达式：**表达式是要访问的数组名，或者是返回值为数组的方法。



   3.1 break
   3.2 continue
   3.3 return

## 7、数组

```java
//定义
int[] array = {1,2,4,7,3,5};
int[] array1 = new int[6];
int[] arr;
arr = new int[array.length]

//数值拷贝 ArrayCopy
int[] array1 = new int[array.length];//开辟新的数据空间，大小为array.length
for (int i = 0; i < array.length; i++) {
            array1[i] = array[i];//遍历复制
}

//数组扩容
```



### java和C语言数组的差异

1. **数组的声明**

Java：int[] data = new int[] {1, 2, 3}；

C：int data[] = {1, 2, 3}；且除声明以外，不允许使用花括号列表的形式赋值；

2. **数组长度的计算**

Java：data.length(行数），data[0].length(列数）；

C：sizeof(data) / sizeof(int)；

3. **数组的赋0初始化**

Java：默认声明时初始化0；或是Arrays.fill(data, 0)；

C：必须使用安全函数memset_s进行初始化，否则内存的数据随机；

4. **数组内容的操作**

Java：数组可以相互赋值 int[] data2 = data；//**数组在默认情况下是引用传递，赋的值是地址，赋值方式为引用赋值**

C：不允许把数组作为一个单元赋给另一个数组（数组名是常量，就是data[0]的地址）；

5. **数组的遍历**

一致，都是使用数组的index索引取值遍历；

# 三、提升

## 1、常用类



## 2、 集合类

### 1）泛型

**java 中泛型标记符：**

+ **E** - Element (在集合中使用，因为集合中存放的是元素)
+ **T** - Type（Java 类）
+ **K** - Key（键）
+ **V** - Value（值）
+ **N** - Number（数值类型）
+ **？** - 表示不确定的 java 类型

## 3、IO流





# 填充：

## 1、代码规范

[阿里巴巴编码规范（Java）](https://www.jianshu.com/p/1884cdc54409)<br />![图片.png](https://cdn.nlark.com/yuque/0/2022/png/22775287/1657446450102-ddfd88cf-888c-42b4-8375-eeee2f474864.png#clientId=u41e3419e-8509-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=463&id=u1226bc2c&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=892&originWidth=1229&originalType=binary&ratio=1&rotation=0&showTitle=false&size=125594&status=done&style=none&taskId=ue850d21f-5ecc-42f3-b5ca-6641acc3b87&title=&width=637.4000244140625)
<a name="uiOne"></a>

> 1. 类、方法的注释,要以javadoc的方式来写。
> 2. 非Java Doc的注释，往往是给代码的维护者看的，着重告述读者为什么这样写如何修改，注意什么问题等
> 3. 使用tab操作,实现缩进,默认整体向右边移动，时候用shift+tab整体向左移
> 4. 运算符和=两边习惯性各加一个空格。比如:2+4*5+ 345-89
> 5. 源文件使用utf-8编码
> 6. 行宽度不要超过80字符
> 7. 代码编写次行风格和行尾风格



## 2、DOS原理

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

```
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

## 3、生成JavaDoc文档

1. cmd

```
javadoc -encoding UTF-8 -charset UTF-8 Doc.java
```

2. idea生成

   1. 选择是整个项目还是模块还是单个文件

   2. 文档输出路径

   3. Locale 选择地区，这个决定了文档的语言，中文就是zh_CN

   4. 传入JavaDoc的参数，一般这样写

      ```
      -encoding UTF-8 -charset UTF-8 -windowtitle “文档HTML页面标签的标题” -link http://docs.Oracle.com/javase/7/docs/api
      ```

## 4、JDK、JRE和JVM三者之间关系

1. JDK=JRE＋开发工具集（例如Javac,java编译工具等)
2. JRE=JVM +Java SE标准类库(java核心类库)
3. 如果只想运行开发好的.class文件只需要JRE

> JDK（Java Development Kit）是针对Java开发员的产品，是整个Java的核心，包括了Java运行环境JRE、Java工具和Java基础类库。
> Java Runtime Environment（JRE）是运行JAVA程序所必须的环境的集合，包含JVM标准实现及Java核心类库。
> JVM是Java Virtual Machine（Java虚拟机）的缩写，是整个java实现跨平台的最核心的部分，能够运行以Java语言写作的软件程序。

[详细点击此处](https://blog.csdn.net/geyouchao/article/details/51669552)

## 5、System.out.printf

若使用System.out.printf，请注意

| 输出控制符    | 针对的数据类型      |
| ------------- | ------------------- |
| %d            | int long short byte |
| %x %#x %X %#X | int long            |
| %c            | char                |
| %f            | float double        |
| %s            | string              |

## 6、键盘输入

```java
Scanner myScanner = new Scanner(System.in);
System.out.println("请输入你的名字：");
String name = myScanner.next();
System.out.println(name);
```



## ∞、xjb搞

### 1、println和print区别

java里常用的控制台输出语句有System.out.println和System.out.print

#### 一:两者之间的区别如下：

1. 参数有区别：

   System.out.println() 可以不写参数

   System.out.print(参数) 参数不能为空.必须有

2. 效果有区别：

   println :会在输出完信息后进行换行,产生一个新行

   print: 不会产生新行

3. println更简洁, print更灵活

   print可以后面跟"\n"来达到和println一样的效果

   也可以跟"\t" 制表符, 等.

#### 二:通过阅读java源代码来理解

System.out.println(字符串参数); 源代码如下

```java
public void println(String x) {
    synchronized (this) {
        print(x);//先调用print(x)来打印信息
        newLine();//然后换行
    }
}
```

 System.out.print(字符串参数); 源代码 如下

```java
public void print(String s) {
    if (s == null) {
        s = "null";
    }
    write(s);
}
```
