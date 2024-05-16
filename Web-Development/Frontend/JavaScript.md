# 快速入门
## 2.1、引入JavaScript
### 1.内部引入
```html
<script>
  alert('hello,world');
</script>
```
### 2.外部引入
**abs.js**
```javascript
alert('hello,world');
```
**abs.html**
```html
<script src="js/hello%20world!.js"></script>
```
## 2.3、数据类型
**>>字符串**
我们使用单引号，或者双引号包裹('abc' "abc")
**>>数组**
Java的数值必须是相同类型的对象~，JS中不需要这样!
```javascript
//保证代码的可读性，尽量使用[]
var arr = [1,2,3,4,5, 'he11o' ,null,true];
new Array(1,12,3,4,4,5 , 'he11o');
```
取数组下标：如果越界了，就会undefined
***Array可以包含任意的数据类型***
```javascript
var arr = [1,2,3,4,5,6];	//通过下标取值和赋值
arr[0]
arr[0] = 1
```
**>>对象**
对象是大括号，数组是中括号~~

> 每个属性之间使用逗号隔开，最后一个不需要添加

```javascript
//Person person = new Person(1,2,3,4,5);
var person = {
    name : "hairui" ,
    age: 3,
    tags: ['js ', 'java' , 'web ' ,'...']
}
/*
let person = {
  name:"Anduin",
  age: 15,
  petPhrase: 'Wow……',
  nickname:'MuGou'
}*/
```
取对象的值
**>>变量字符串**

1. 正常字符串我们使用单引号，或者双引号包裹('abc'	"abc")
1. 注意转义字符
```javascript
\
\n
lt
\u4e2d		\u#### unicode字符
\x41						 Asc11字符
```
3、多行字符串编写
```javascript
var made = 
          `hello 
           world
           fuck
           you`
```

4. 模板字符串
```javascript
let damn = "sb";
let cjb = "witcher3";
let gentle = `你好呀，${damn}`
```

5. 字符串长度
```javascript
console. log(str.length)
```

6. 字符串的可变性，不可变

![image.png](https://cdn.nlark.com/yuque/0/2021/png/22775287/1635681597271-7c160c3f-313b-4f66-ae26-a492626529b3.png#clientId=ubb62ac7f-0538-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=179&id=t050q&margin=%5Bobject%20Object%5D&name=image.png&originHeight=358&originWidth=576&originalType=binary&ratio=1&rotation=0&showTitle=false&size=56197&status=done&style=none&taskId=u81a052eb-8829-4c19-ae10-8d9d06bf0ab&title=&width=288)

7. 大小写转换
```javascript
//注意，这里是方法，不是属性了
student.toUpperCase()
student.toLowerCase()
```

8. indexOf()函数
8. substring
```javascript
[)
student.substring(1)		//从第一个字符串截取到最后一个字符串
student.substring(1,3)	//[1,3)
```
> 首字符必须是字母、下划线（-）或美元符号（$）
> 数值不可以作为首字符。这样，JavaScript 就能轻松区分标识符和数值。

**_驼峰式大小写（Camel Case）：_**
例：FirstName, LastName, MasterCard, InterCity
**>>number**
javascript不区分小数和整数，Number
```javascript
123 // 整数123
123.1 // 浮点数
123.11.123e3 // 科学计数法
-99 // 负数
NaN // not a number
Infinity // 表示无限大
```
**>>布尔值**
在逻辑中，真值或逻辑值是指示一个陈述在什么程度上是真的。在计算机编程上多称作布尔值。
ture	false
**>>逻辑运算**
&&	||	！
**>>比较运算符**
```javascript
=		赋值
==	等于（类型不一样，值一样，也会判断为true）
===	绝对等于（类型一样，值一样，结果为true）
```

- NaN===NaN，这个与所有的数值都不相等，包括自己
- 只能通过isNaN(NaN)来判断这个数是否是NaN

_**浮点数问题：**_
```javascript
console.log((1/3) === (1-2/3))
console.log(Math.abs(1/3-(1-2/3))<0.0000001)
```
尽量避免使用浮点数进行运算，存在精度问题!
> **null**：空；
> **undefined**：未定义

## 2.4、严格检查模式
前提:IEDA需要设置支持ES6语法
**_'use strict'_**：严格检查模式．预防avaScript的随意性导致产生的一些问题，必须写在Javascript的第一行！
局部变量建议都使用let去定义

## >>常见函数
```
1.console.Log(score)
/*在浏览器的控制台打印变量!
system.out.println();*/

2.alert(message)
/*alert的用法是“alert(在对话框中显示的纯文本)”
和printf("")用法一样*/

3.alert和conlose.log的区别
console.log
在控制台输出
可以输出任意类型的数据
支持多个参数的写法
无阻塞作用
alert
在页面上弹出
只能输出String类型的数据
不支持多个参数的输出，只能输出第一个参数
有阻塞作用，点击确定按钮之后，代码才能执行下一步

4.
item	就是你数组中每个值(10,20,30)
index	就是数组索引(0,1,2）
array	就是你定义的arr

5.函数的定义
function name(参数 1, 参数 2, 参数 3) {
    要执行的代码
}
6.hasOwnProperty() 
用来判断某个对象是否含有指定的自身属性
```
### ps：

1. 注释//后加空格，否则会报错
1. Javascript严格区分大小写
1. 用indexOf()函数等查阅字符串中某个字符的位置时，从0开始计数
# 基本语法
## _1.定义变量_
变量类型	 变量名 = 变量值；
```javascript
var a = 1		//
let b = 1
const c = 1
```
## 2.条件控制
if，if else，else，switch，都适用（甚至可以不加分号结束）
## 3.数据类型
### 3.1、字符串

1. **正常字符串**我们使用单引号，或者双引号包裹('abc'	"abc")
1. **注意转义字符**
```javascript
\
\n
lt
\u4e2d		\u#### unicode字符
\x41						 Asc11字符
```
3、**多行字符串编写**
```javascript
var made = 
          `hello 
           world
           fuck
           you`
```

4. **模板字符串**
```javascript
let damn = "sb";
let cjb = "witcher3";
let gentle = `你好呀，${damn}`
```

5. **字符串长度**
```javascript
console. log(str.length)
```

6. **字符串的可变性，不可变**

![image.png](https://cdn.nlark.com/yuque/0/2021/png/22775287/1635681597271-7c160c3f-313b-4f66-ae26-a492626529b3.png#clientId=ubb62ac7f-0538-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=179&id=gRoS1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=358&originWidth=576&originalType=binary&ratio=1&rotation=0&showTitle=false&size=56197&status=done&style=none&taskId=u81a052eb-8829-4c19-ae10-8d9d06bf0ab&title=&width=288)

7. **大小写转换**
```javascript
//注意，这里是方法，不是属性了
student.toUpperCase()
student.toLowerCase()
```

8. **indexOf()函数**
8. **substring**
```javascript
[)
student.substring(1)		//从第一个字符串截取到最后一个字符串
student.substring(1,3)	//[1,3)
```
### 3.2、数组

1. 长度
```javascript
arr.length
```
注意:加入给arr.length赋值，数组大小就会发生变化~，如果赋值过小，元素就会丢失

2. indexOf，通过元素获得下标索引
```javascript
arr.indexof(2)
1
```
字符串的“1”和数字1是不同的

3. **slice ()**截取Array的一部分，返回一个新数组，类似于String中的substring
3. ***push(). pop()***		尾部
```javascript
arr.push():	压入到尾部
arr.pop():	弹出尾部的一个元素
```

5. ***unshift() , shift()*	**头部
```javascript
unshift:	压入到头部
shift:		弹出头部的一个元素
```

6. **排序sort()**
```javascript
arr.sort()
(6) ['A', 'B', 'C', 'D', 'E', 'F']
```

7. **元素反转 reverse()**
```javascript
arr.reverse()
(5) ['E', 'D', 'C', 'B', 'A']
```

8. ***concat ()*		**拼接数组
```javascript
arr.concat([1,2,3,3.1415926])
(9) ['E', 'D', 'C', 'B', 'A', 1, 2, 3, 3.1415926]
```
注意: concat ()并没有修改数组，只是会返回一个新的数组

9. **连接符 join**

打印拼接数组，使用特定的字符串连接
```javascript
(3) ['A', 'B', 'C']
arr.join('*')
'A*B*C'
```

10. **多维数组**
```javascript
arr=[[1,2],[3,4],['5','6']]
arr[2][1]
'6'
```
### 3.3、对象

1. **对象赋值**
```javascript
person.name = "hunter"
'hunter'
person.name
'hunter'
```

2. 使用一个不存在的对象属性，不会报错! undefined
```javascript
person.haha
undefined
```

3. 动态的删减属性，通过delete删除对象的属性
```javascript
delete person. name
true
person
```

4. 动态的添加，直接给新的属性添加值即可
```javascript
person.haha = "haha"
"haha"
person
```

5. 判断属性值是否在这个对象中!xxx in xxx!
```javascript
'age' in person
true
//继承
'tostring' in person
true
```

6. 判断一个属性是否是这个对象自身拥有的hasOwnProperty()
```javascript
person. hasownProperty('tostring')
false
person. hasownProperty('age')
true
```
### 3.4、流程控制
if判断
```javascript
let number = 18;
if(number<5){
  alert('child')
} else if(number>=5&&number<18){
	alert('teen')
} else{
	alert('adult')
}
```
while循环
```javascript
while(age<100){
age = age + 1;
console. 1og(age)
}
```
for循环
```javascript
for (let i = 0; ; i++) {
  if ( (i % 5 === 1) && (i % 6 === 5) && (i % 7 === 4) && (i % 11 === 10)){
    console.log(i);
    break;
  }
}
```
数组循环?
forEach循环
> 5.1引入

```javascript
let IQ = [10, 20, 30, 40, 50, 60, 70, 80, 250]
IQ.forEach(function (value){
  console.log(IQ)
}
)
```
for…in
```javascript
let age = [10, 20, 30, 40, 50, 60, 70, 80, 250]
for(var num in age){
  if(age.hasOwnProperty(num)){
    console.log("edgnb！")
    console.log(age[num])
  }
}
```
### 3.5、Map和Set
> ES6的新特性

**Map：**
```javascript
//Es6 Map
//学生的成绩，学生的名字
// var names = ["tom" , "jack " , "haha"];
// var scores = [100, 90,80];
var map = new Map([[ 'tom' ,100],[ 'jack' ,90], [ 'haha',80]]);
var name = map.get( 'tom'); //通过key获得value
map.set('admin',123456);
```
**Set：**无序不重复元素
```javascript
set.add(2);								//添加
set.delete(1);						//删除
console.log(set.has(3));	//是否包含某个元素
```
### 3.5、iterator
**遍历数组**
```javascript
//通过for of / for in下标
var arr = [3,4,5]
for (var x of arr){
		console.1og(x)
}
```
**遍历map**
```javascript
var map = new Map([["tom" ,100],["jack " ,90],["haha",80]]);
for (let x of map){
		console.log(x)
}
```
**遍历set**
```javascript
var set =new set([5,6,7]);
for (let x of set) {
		console.1og(x)
}
```
## 4.函数及面向对象
### 4.1、函数定义
绝对值函数
> 定义方式一

```javascript
function abs(x){
    if(x>=0){
    		return x;
    }else{
    		return -x;
		}
}
```
一旦执行到return代表函数结束，返回结果!
> 定义方式二

```javascript
var abs = function (x){
		if(x>=0){
				return x;
    }else{
				return -x;
		}
}
```
function(x) ....}这是一个匿名函数。但是可以把结果赋值给abs，通过abs 就可以调用函数!
> 调用函数

```javascript
abs(10)		//10
abs(-10)	//10
```
> arguments

```javascript
var abs = function(x){
    console.log( "x=>"+x);
    for (var i = o; i<arguments.length;i++){
    		console.log(arguments[i];
    }
    if(x>=0){
    		return x;
    }else{
    		return -×;
    }
}
```
问题: arguments包含所有的参数，我们有时候想使用多余的参数来进行附加操作。需要排除已有参数~
> rest

```javascript
function aaa(a,b, ...rest) {
		console.log("a=>"+a);
  	conso1e.log("b=>"+b);
  	conso1e.log(rest);
}
```
rest参数只能写在最后面，必须用...标识。
### 4.2、变量的作用域
在javascript中, var定义变量实际是有作用域的。
假设在函数体中声明，则在函数体外不可以使用~(非要想实现的话，后面可以研究一下`闭包`

```javascript
function qj() {
	var x = 1;
  	x = x+1;
}

= x+2; //Uncaught ReferenceError: x is not defined
```
如果两个函数使用了相同的变量名，只要在函数内部，就不冲突
```javascript
function qj() {
		var x = 1;
  	x = x+1;
}

function qj1() {
		var x = 'A';
  	x = x+1;
}
```
内部函数可以访问外部函数的成员，反之则不行
```javascript
function qj() {
		var x = 1;
//内部函数可以访问外部函数的成员，反之则不行
  	function qj2() {
				var y =x + 1;l/2
		}
		var z =y + 1;// Uncaught ReferenceError: y is not defined
}
```
> window

> 局部作用域 let

> 常量const

```javascript
const PI = '3.14'; //只读变量
console.log(PI);
PI = '123';
```
### 4.3、方法
```javascript
var bowen = {
		name : '博文'，
  	birth: 2000,
  	//方法
		age : function () {
				//今年 -出生的年
				var now = new Date(.getFullYear();
      	return now-this.birth;
		}
}
//属性
bowen.name
//方法，一定要带()
bowen.age()
```
> apply

```
4.3、闭包(难点)
4.4、箭头函数（新特性)
4.5、创建对象
4.6、class继承(新特性)
4.7、原型链继承(难)
```
## 5、常用对象
> 标准对象

```javascript
typeof 123
"number"
typeof '123'
"string"
typeof true
"boolean"
typeof NaN
"number"
typeof []
"object"
typeof {}
"object"
typeof Math.abs
"function"
typeof undefined
"undefined"
```
### 5.1、Date
```javascript
var now = new Date(); //sat Jan o4 
now.getFullYear(); //年
now.getMonth(); //月 0 ~ 11代表月
now.getDate(); //日
now.getDay(); //星期几
now.getHours();//时
now.getMinutes();//分
now.getSeconds();//秒
now.getTime(); //时间戳全世界统一
```
转换
```javascript
now.toLocaleString()//	注意，调用是一个方式，不是一个属性!
'2021/11/9 上午10:32:35'
```
### 5.2、JSON
在JavaScript一切皆为对象、任何js支持的类型都可以用JSON来表示格式：number，string……

- 对象都用{}
- 数组都用[]
- 所有的键值对 都是用 key:value

**JSON字符串 和 JS 对象的转化**
```javascript
let Character = {
  name: "Elizabeth",
  age: 19,
  gender: 'female',
  father: 'Booker'
}
//对象转换为json字符串
let jsonC = JSON.stringify(Character) //{"name":"Elizabeth","age":19,"gender":"female","father":"Booker"}
//json字符串转换为对象
let obj = JSON.parse(jsonC)           
//{name: 'Elizabeth', age: 19, gender: 'female', father: 'Booker'}
```
### 5.3、Ajax

- 原生的js写法	xhr 异步请求
- jQuey封装好的方法 $("#name").ajax("")
- axios请求
## 6、面向对象编程
### 6.1、原型对象
```javascript
let role = {
  name: "Elizabeth",
  age: 19,
  gender: 'female',
  father: 'Booker DeWitt',
  skill: function () {
    console.log(this.name + " can pick locks");
  }
}
let Booker = {
  name:"Booker"
}
Booker.__proto__ = role;
```
```javascript
function Student(name) {
  this.name = name;
}

//给Student新增一个方法
Student.prototype.hello = function () {
  alert('Hello')
```
### 6.2、class继承
```javascript
<script>
//定义一个学生的类
class Student {

  constructor(name) {
    this.name = name;
  }

  hello() {
    alert('hello');
  }


}

class pupil extends Student{
  constructor(name,grade) {
    super(name);
    this.grade = grade;
  }
  chaofeng(){
    alert('我是一名小学生')
  }
}

var xiaolan = new Student('xiaolan');
var xiaoming = new pupil('xiaoming',1);
var xiaohua = new Student('xiaohua');
</script>
```
> 原型链

![image.png](https://cdn.nlark.com/yuque/0/2021/png/22775287/1637480852071-27b19f2d-0de6-4cf6-a994-4f306c16e341.png#clientId=u3102fbf5-6428-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=277&id=u0b91dc5c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=554&originWidth=655&originalType=binary&ratio=1&rotation=0&showTitle=false&size=104799&status=done&style=none&taskId=u92acde69-e9c7-4350-8755-f6b440864cb&title=&width=327.5)
## 7、操作Dom对象（重点）
> window

window代表 浏览器窗口
```javascript
window.alert(1)
undefined
window.innerHeight
722
window.innerWidth
834
window.outerHeight
824
window.outerWidth
1536
```
> Navigator


> screen


> location


> Document

## 8、操作Dom对象（重点）
> 核心
> 获得dom节点
> 更新节点
> 更新节点
> 插入节点

## 9、操作表单（验证）
> 表单 form DOM树

- 文本框text
- 下拉框< select >
- 单选框radio
- 多选框checkbox
- 隐藏域hidden
- 密码框password
- ……

> 获得表单信息

> 提交表单

## 10、jQuery
jQuery API 3.5.1 速查表  --作者：Shifone
[https://jquery.cuishifeng.cn/](https://jquery.cuishifeng.cn/)
> 公式

$(selector).action()
> 选择器

标签、类、id选择器
> 事件
