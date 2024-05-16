# MyBatis核心配置文件详解

MyBatis核心配置文件的顶层结构如下:

- configuration(配置)
  - properties(属性)
  - settings(设置)
  - typeAliases(类型别名)
  - typeHandlers(类型处理器)
  - objectFactory (对象工厂)
  - plugins(插件)
  - environments(环境配置)
    - environment(环境变量)
      - transactionManager (事务管理器)
      - dataSource(数据源)
  - o databaseldProvider (数据库厂商标识)
  - mappers(映射器)

- 类型别名(typeAliases)

  ```xml
  <typeAliases >
  	<package name="com.itheima.pojo"/>
  </typeAliases>
  ```

  细节:配置各个标签时，**需要遵守前后顺序**

# 配置文件Curd

配置文件完成增删改查

## 1. 查

```xml
<!--1.基础方法 -->
<select id="selectAll" resultType="com.hunter.pojo.Brand">
    select *
    from tb_brand;
</select>

<!--2.起别名-->
<!--
	sql片段
-->
<sql id="brand_column">
    id,brand_name as brandName, company_name as companyName, ordered, description, status
</sql>

<select id="selectAll" resultType="com.hunter.pojo.Brand">
    select
    <include refid="brand_column" />
    from tb_brand;
</select>

<!--3.resultMap-->

<!--
        数据库表的字段名称 和 实体类的属性名称 不一样，则不能自动封装数据
        * 起别名: 对不一样的列名起别名，让别名和实体类的属性名一样
            * 缺点: 每次查询都要定义一次别名
                * sql片段
                    * 缺点: 不灵活
        * resultMap:
            1.定义<resultMap>标签
            2.在<select>标签中，使用resultMap属性替换 resultType属性
-->

<!--
    id:唯一标识
    type:映射的类型,支持别名
-->

<resultMap id="brandResultMap" type="com.hunter.pojo.Brand">

    <!--
    	id:完成主键字段的映射
    		column:表的列名
    		property:实体类的属性名
    	result:完成一般字段的映射
	-->
	<result column="brand_name" property="brandName"/>
	<result column="company_name" property="companyName"/>
</resultMap>
<select id="selectAll" resultMap="brandResultMap">
	select *
	from tb_brand;
</select>

<!--4.参数占位符-->
<!--
    * 参数占位符：
        1. #{}:会将其替换为 ？，防止SQL注入问题
        2. ${}:拼接sql，会出现SQL注入问题
        3. 使用时机
            * 参数传递的时候：#{}
            * 表名或列名不固定的情况下：${}
    * 参数类型:parameterType:可以省略不写
    * 特殊字符处理:
        1. 转义字符
        	< : &lt;
        2. CDATA区
        	<![CDATA[

        	]]>
-->
<select id="selectById" resultMap="brandResultMap">
    select *
    from tb_brand
    where id
    <![CDATA[
            <
        ]]>
    #{id};
</select>

<!--5.条件查询-->
<!--
    条件查询
-->
<select id="selectByCondition" resultMap="brandResultMap">
    select *
    from tb_brand
    where status = #{status}
      and company_name like #{companyName}
      and brand_name like #{brandName}
</select>

<!--
    动态条件查询
        * if:条件判断
            * test:逻辑表达式
        * 问题: 第一个条件不需要逻辑运算符
            * 恒等式 where 1 = 1 and …… and ……
            * <where> 替换 where 关键字
-->

<select id="selectByCondition" parameterType="int" resultMap="brandResultMap">
    select *
    from tb_brand
    /*where 1 = 1*/
    <where>
        <if test="status != null">
            and status = #{status}
        </if>
        <if test="companyName != null and companyName != '' ">
            and company_name like #{companyName}
        </if>
        <if test="brandName != null and brandName != '' ">
            and brand_name like #{brandName}
        </if>
    </where>
</select>

```

## 2. 增

```xml
<!--添加主键返回-->
<!--
	useGeneratedKeys：
		其设置为 true 时，表示如果插入的表id以自增列为主键，则允许 JDBC 支持自动生成主键，并可将自动生成的主键id返回;
		其参数只针对 insert 语句生效，默认为 false；
	keyProperty：
		其中对应的值是实体类的属性，而不是数据库的字段。
-->
<insert useGeneratedKeys="true" keyProperty="id">
```

## 3. 删

```xml
<!--
    mybatis会将数组参数，封装为一个Map集合。
        * 默认：array = 数组
        * 使用@Param注解改变map集合的默认key的名称
-->
<delete id="deleteByIds">
        delete from tb_brand where id
        in
    			<!--
					collection：可以用@Param注解，也可以直接写array
					item：遍历的每一个元素
					separator：分隔符
					open：开头添加片段
					close：末尾添加片段
				-->
                <foreach collection="ids" item="id" separator="," open="(" close=");">
                <!--<foreach collection="array" item="id" separator="," open="(" close=");">-->
                    #{id}
                </foreach>
</delete>
```

# 参数传递

```java
/**
    * Mybatis参数封装
    * - 单个参数:
    *   - POJO类型：直接使用，属性名和 参数占位符名称 一致
    *   - Map集合：直接使用，键名 和 参数占位符名称 一致
    *   - Collection:封装成Map集合，可以使用@Param注解，替换Map集合中默认的arg键名
    *      map.put("arg0",collection集合);
    *      map.put("collection",collection集合);
    *   - List:封装成Map集合，可以使用@Param注解，替换Map集合中默认的arg键名
    *      map.put("arg0",list集合);
    *      map.put("collection",list集合);
    *      map.put("list",list集合);
    *   - Array:封装成Map集合，可以使用@Param注解，替换Map集合中默认的arg键名
    *      map.put("arg0",数组);
    *      map.put("array",数组);
    *   - 其他类型:直接使用
    * - 多个参数:封装成Map集合，可以使用@Param注解，替换Map集合中默认的arg键名
    *      map.put("arg0",参数值1)
    *      map.put("param1",参数值1)
    *      map.put("param2",参数值2)
    *      map.put("arg1",参数值2)
*/
```

***MyBatis提供了ParamNameResolver类来进行参数封装***

**建议**:将来都使用@Param注解来修改Map集合中默认的键名，并使用修改后的名称来获取值，这样可读性更高!

# 注解Curd

查询:@Select

添加:@Insert

修改:@Update

删除:@Delete

> 提示
>
> 注解完成简单功能
> 配置文件完成复杂功能

# Misc

## @Param注解

### 1、概述

​	首先明确这个注解是为SQL语句中参数赋值而服务的。
​
​	@Param的作用就是给参数命名，比如在mapper里面某方法A（int id），当添加注解后A（@Param("userId") int id），也就是说外部想要取出传入的id值，只需要取它的参数名userId就可以了。将参数值传如SQL语句中，通过#{userId}进行取值给SQL的参数赋值。

### 2、实例：
​	实例一：@Param注解基本类型的参数

​	mapper中的方法：

```java
public User selectUser(@Param("userName") String name,@Param("password") String pwd);
```

​	映射到xml中的`<select>`标签
```xml
<select id="selectUser" resultMap="User">
	select * from user  where user_name = #{userName} and user_password=#{password}
</select>
```
​	其中where user_name = #{userName} and user_password = #{password}中的userName和password都是从注解@Param（）里面取出来的，取出来的值就是方法中形式参数 String name 和 String pwd的值。

​	实例二：@Param注解JavaBean对象

​	SQL语句通过@Param注解中的别名把对象中的属性取出来然后复制

​	mapper中的方法：
```java
public List<User> getAllUser(@Param("user") User u);
```

​	映射到xml中的<select>标签
```xml
    <select id="getAllUser" parameterType="com.vo.User" resultMap="userMapper">
            select
            from user t where 1=1
                 and   t.user_name = #{user.userName}
                  and   t.user_age = #{user.userAge}
        </select>
```
### 3、注意点

​	当使用了@Param注解来声明参数的时候，SQL语句取值使用#{}，${}取值都可以。

​	当不使用@Param注解声明参数的时候，必须使用的是#{}来取参数。使用${}方式取值会报错。

​	不使用@Param注解时，参数只能有一个，并且是Javabean。在SQL语句里可以引用JavaBean的属性，而且只能引用JavaBean的属性。

```java
@Select("SELECT * from Table where id = #{id}")
Enchashment selectUserById(User user);
```
