# 知识

## 1、基本语法

### 1.1、 操作库

```sql
-- 1、创建数据库
create database [if not exists] westos;

-- 2、删除数据库
drop database [if exists] westos;

-- 3、使用数据库
SELECT * FROM admin
选中结果不存在时
/*
> 1146 - Table 'school.admin' doesn't exist
*/
-- tab键的上面,如果你的表名或者字段名是一个特殊字符，就需要带``
use `school`

-- 4、查看数据库
show databases -- 查看所有的数据库
```

### 1.2、 操作表

```sql
-- 显示数据库中的所有表
show tables;

-- 创建数据表
CREATE TABLE pet (
    name VARCHAR(20),
    owner VARCHAR(20),
    species VARCHAR(20),
    sex CHAR(1),
    birth DATE,
    death DATE
);

-- 查看数据表结构
-- describe pet;
desc pet;

-- 查询表
SELECT * from pet;

-- 插入数据
INSERT INTO pet VALUES ('puffball', 'Diane', 'hamster', 'f', '1990-03-30', NULL);

-- 修改数据
UPDATE pet SET name = 'squirrel' where owner = 'Diane';

-- 删除数据
delete from pet where name = 'Fluffy';
```

增删改查（CRUD）

**--增加INSERT**

```sql
1,insert into 表名(字段名) values (值)
	insert into user(name,age) values('张三',20),('李四',18)
2,insert into 表名 set column1=values1，column2=values2
	insert into user set name='张三',age=17
3,insert into 表名 select 语句（两个表结构相同）
	insert into user select '张三，17' union all '李四 ，18'
4,insert into 表名 (字段名）select 语句（两个表结构不同）
	insert into user (name) select user1.age=user2.age
```

**--删除DELETE**

**--修改UPDATE**

**--查询SELECT**

##  2、建表约束

###  2.1、主键约束

它能够唯一确定一张表中的一条记录，也就是我们通过给某个字段添加约束，就可以使得改字段不重复且不为空。

```sql
create table user(
  id int primary key,
  name varchar(20)
);

insert into user values( 1,'张三');
#> 1062 - Duplicate entry '1' for key 'user.PRIMARY'
insert into user values( null,'张三');
#> 1048 - Column 'id' cannot be null
```

如果说我们创建表的时候，忘记创建主键约束了?改怎么办?

```sql
#创建表
create table user4(
    id int,
    name varchar(20)
);
#修改表结构，添加主键
alter table user4 add primary key(id);
#如何删除？
alter table user4 drop primary key;
#使用modify 修改字段，添加约束
alter table user4 modify id int primary key;
```

###  2.2、自增约束

```sql
create table user3(
	id int primary key auto_increment,
	name varchar(20)
);
insert into user3 (name) values ('zhangsan');
```

###  2.3、唯一约束

````sql
-- 创建唯一约束
create table user6(
	id int,
	name varchar(20),
	unique(name)
);

create table user7(
	id int,
	name varchar(20) unique
);

-- 如何删除唯一约束
alter table user7 drop index name;

-- 总结:
-- 1、建表的时候就添加约束
-- 2、可以使由alter …… add ……
-- 3、alter …… modif ……
-- 4、删除alter …… drop ……
````

###  2.4、非空约束

```sql
-- 非空约束 not null
-- 修饰的字段不能为空NULL
create table user9(
	id int,
	name varchar(20) not null
);
```

###  2.5、默认约束

```sql
-- 默认约束
-- 就是当我们插入字段值的时候，如果没有传值，就会使用默认值

create table user10(
	id int,
	name varchar(20),
	age int default 10
);

-- 如果传了值就不会使用默认值
```

### 2.6、外键约束

```sql
-- 外键约束
-- 涉及到两个表:父表,子表
-- 主表,副表。

# 父表中被参考列必须要唯一约束或主键约束
-- 班级
create table classes(
	id int primary key,
	name varchar(20)
);

-- 学生表
create table students(
	id int primary key,
	name varchar(20),
	class_id int,
	foreign key(class_id) references classes(id)
);

-- 1 主表(父表)classes中没有的数据值，在副表(子表)中，是不可以使用的。
-- 2 主表中的记录被副表引用,是不可以被删除的。
```

# __________________________________________________________________________________

# 入门

## 1、初始`MySql`

### `MySql`的安装

1. 在`R:\Work\mysql-5.7.29`(自己决定)下新建my.ini 文件（8.0版本不需要配置ini文件）

2. 编辑my.ini文件,注意替换路径位置

   ```
   [mysqld]
   basedir=R:\Work\mysql-5.7.29\
   datadir=R:\Work\mysql-5.7.29\data\
   port=3306
   skip-grant-tables
   ```

3. 启动管理员模式下的CMD，并将路径切换至`mysql` 下的bin目录，然后输入`mysqld -install`(安装`mysql`)

4. 再输入`mysqld --initialize-insecure --user=mysql`
   初始化数据文件

5. 启动mysql `net start mysql`
   然后用命令`mysql -u root -p`
   进入`mysql`管理界面(密码可为空)

6. 进入界面后更改root密码

   `update mysql.user set authentication_string=password('123456') where user='root' and Host= 'localhost';`

   mysql8 用：

   `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';`
   (最后输入flush privileges;刷新权限)

7. 修改my.ini文件删除最后一句skip-grant-tables

8. 重启`mysql`即可正常使用

   ```
   net stop mysql
   net start mysql
   ```

9. 上测试出现以下结果就安装好了

   ![IMG_20220925_1851_8](https://cdn.jsdelivr.net/gh/Hunter9812/Jordan/img/IMG_20220925_1851_8.png)



###  安装Navicat和使用

**从网上搜的[Navicat Premium 15安装与激活（内含注册机）](https://www.jianshu.com/p/4113cd5ef139)**

排序规则:

![IMG_20220925_1851_7](https://cdn.jsdelivr.net/gh/Hunter9812/Jordan/img/IMG_20220925_1851_7.png)

﻿

新建表后默认这样设置就可以了

### 连接数据库

```sql
mysql -uroot -p123456		-- 连接数据库
update mysql.user set authentication_string=password('123456') where user='root' and Host ='localhost'; 					-- 修改用户密码
flush privileges;				-- 刷新权限
---------------------------------------hr
--------------------------------------------------
-- 所有的语句都是用;结尾
show databases;					-- 查看所有的数据库

mysql> use school 			-- 切换数据库	use 数据库名
Database changed

show tables; 						-- 查看数据库中所有的表
describe student; 			-- 显示数据库中所有的表的信息

create database westos; -- 创建一个数据库
exit; 									--退出连接

-- 单行注释(SQL的本来的注释)
/*	(sql的多行注释）
he11oi
asdasd
asdas
*/
```

**数据库xxx语言**

**DDL**		定义

**DML**	操作

**DQL**		查询

**DCL**	控制

## 2、操作数据库

操作数据库>操作数据库中的表>操作数据库中表的数据

**mysql关键字不分区大小写**

###  2.1、操作数据库

```
-- 1、创建数据库
create database [if not exists] westos;
-- 2、删除数据库
drop database [if exists] westos;
-- 3、使用数据库
SELECT * FROM admin
选中结果不存在时
/*
> 1146 - Table 'school.admin' doesn't exist
*/

-- tab键的上面,如果你的表名或者字段名是一个特殊字符，就需要带``
use `school`
-- 4、查看数据库
show databases -- 查看所有的数据库
```

对比: Navicat的可视化操作

###  2.2、数据库的列类型

> 数值

●tinyint		十分小的数据		1个字节

●smallint		较小的数据		2个字节

●mediumint	中等大小的数据 	3个字节

●int 			标准的数据		4个字节	常用

●bigint		较大的数据		8个字节

●float			浮点数			4个字节

●double		浮点数			8个字节	（精度问题）

●decimal		字符串形式的浮点数	一般用于金融计算

> 字符串

●char			字符串固定大小的	0~255

●varchar		可变字符串	0~65535		常用

●tinytext 		微型文本		2^8 - 1

●text			文本串		2^16 - 1		保存大文本

> 时间日期

**java.util.Date**

●date 		YYYY-MM-DD，日期格式

●time 		HH: mm: ss ，时间格式

●datetime 	YYYY-MM-DD  HH: mm: ss	最常用的时间格式

●timestamp	时间戳，	1970.1.1到现在的毫秒数!	也较为常用!

●year			年份表示

> null

●没有值，未知

●**注意，不要使用NULL进行运算，结果为NULL**

```sql
//数据类型
bigint
binary
bit
blob
char
date
datetime
decimal
double
enum
float
geometry
geometrycollection
int
integer
json
linestring
longblob
longtext
mediumblob
mediumint
mediumtext
multilinestring
multipoint
multipolygon
numeric
point
polygon
real
set
smallint
text
time
timestamp
tinyblob
tinyint
year
```

###  2.2、数据库的字段属性（imp）

**无符号：**

●无符号的整数（Unsigned）

●声明了该列不能声明为负数

**填充零：**

●0的填充（zerofill）

●不足的位数使用0来填充，	int(3) ，5 -- 005

**自动递增：**

●通常理解为自增，自动在上一条记录的基础上+1(默认)

●通常用来设计唯一的主键~ index。必须是整数类型

●可以自定义设计主键白增的起始值和步长

**不是null：**（not null）

●假设设置为not null ，如果不给它赋值，就会报错!

●Null，如果不填写值，默认就是null!

**默认:**

●设置默认的值!

●sex，默认值为男，如果不指定该列的值，则会有默认的值!

拓展：[阿里mysql规范](https://www.cnblogs.com/lizhonghua34/p/7685848.html)

```
/*每一个表，都必须存在以下五个字段!未来做项目用的，表示一个记录存在意义!

id					主键
`version`		乐观锁
is_delete		伪删除
gmt_create	创建时间
gmt_update	修改时间

*/
```

