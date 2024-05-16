# SpringBoot快速上手

使用IDEA的Spring Initializr创建项目

- 选 2.7.x的版本

## 开发环境热部署

devtools依赖

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
```

application.yaml中配置devtools

```yaml
spring:
  devtools:
    restart:
      enabled: true # 热部署生效
      additional-paths: src/main/java # 设置重启目录
      exclude: static/** # 设置classpath目录下的WEB-INF文件夹内容修改不重启
```

- 如果使用了Eclipse，那么在修改完代码并保存之后，项目将自动编译并触发重启，而如果使用了IntelliJ IDEA，还需要配置项目自动编译。
- 打开Settings页面，在左边的菜单栏依次找到
  Build,Execution,Deployment→Compile，勾选Build project automatically
- 按Ctrl+Shift+Alt+/快捷键调出Maintenance页面，单击Registry，勾选compiler.automake.allow.when.app.running复选框。
  2021以后的版本在settings -> advanced settings -> compiler 勾选第一个就可以完成第二步
- 做完这两步配置之后，若开发者再次在IntelliJ IDEA中修改代码，则项目会自动重启。

## Web入门

- Spring Boot将传统Web开发的mvc、json、tomcat等框架整合，提供了spring-boot-starter-web组件，简化了Web应用配置。
- 创建SpringBoot项目勾选Spring Web选项后，会自动将spring-boot-starter-web组件加入到项目中。
- spring-boot-starter-web启动器主要包括web、webmvc、json、tomcat等基础依赖组件，作用是提供Web开发场景所需的所有底层依赖。
- webmvc为Web开发的基础框架，json为JSON数据解析组件,tomcat为自带的容器依赖。

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

# SpringBoot Controller

## 控制器

- Spring Boot提供了@Controller和@RestController两种注解来标识此类负责接收和处理HTTP请求。
- 如果请求的是页面和数据，使用@Controller注解即可;如果只是请求数据，则可以使用@RestController注解。

### @Controller的用法

- 示例中返回了hello页面和name的数据，在前端页面中可以通过${name}参数获取后台返回的数据并显示。

- @Controller通常与Thymeleaf模板引擎结合使用。

  ```java
  @Controller
  public class HelloController {
      @RequestMapping("/hello")
      public String index(ModelMap map){
          map.addAttribute("name","zhangsan");
          return "hello";
      }
  }
  ```

### @RestController的用法

默认情况下，RestController注解会将返回的对象数据转换为JSON格式。

```java
@RestController
public class HelloController {
    @RequestMapping ("/user")
    public User getUser(){
        User user = new User();
        user.setUsername("zhangsan").user.setPassword("123");
        return user;
    }
}

```

## 路由映射

- @RequestMapping注解主要负责URL的路由映射。它可以添加在Controller类或者具体的方法上。
- 如果添加在Controller类上，则这个Controller中的所有路由映射都将会加上此映射规则，如果添加在方法上，则只对当前方法生效。
- @RequestMapping注解包含很多属性参数来定义HTTP的请求映射规则。常用的属性参数如下:
  - value:请求URL的路径，支持URL模板、正则表达式
  - method: HTTP请求方法
  - consumes:请求的媒体类型(Content-Type)，如application/json
  - produces:响应的媒体类型
  - params，headers:请求的参数及请求头的值
- RequestMapping的value属性用于匹配URL映射，value支持简单表达式`RequestMapping("/user")`
- @RequestMapping支持使用通配符匹配URL，用于统一映射某些URL规则类似的请求:`@RequestMapping("/getJson/*.json")`，当在浏览器中请求/getJson/a.json或者/getJson/b.json时都会匹配到后台的Json方法
- @RequestMapping的通配符匹配非常简单实用，支持`“*" “?” “**”`等通
  配符
- 符号`“*”`匹配任意字符，符号`“**”`匹配任意路径，符号`“?”`匹配单个字符。
- 有通配符的优先级低于没有通配符的，比如`/user/add.json`比`/user/*.json`优先匹配。
  有`“**”`通配符的优先级低于有`“*”`通配符的。

# SpringBoot文件上传+拦截器

## 静态资源访问

- 使用IDEA创建Spring Boot项目，会默认创建出classpath:/static/目录，静态资源一般放在这个目录下即可。

- 如果默认的静态资源过滤策略不能满足开发需求，也可以自定义静态资源过滤策略。

- 在application.properties中直接定义过滤规则和静态资源位置:

  spring.mvc.static-path-pattern=/static/**
  spring.web.resources.static-locations=classpath:/static/

- 过滤规则为/static/**，静态资源位置为classpath:/static/

## 文件上传原理

- 表单的enctype属性规定在发送到服务器之前应该如何对表单数据进行编码。
- 当表单的enctype="application/x-www-form-urlencoded”(默认）时，form表单中的数据格式为: key=value&key=value
- 当表单的enctype="multipart/form-data"时，其传输数据形式如下

### SpirngBoot实现文件上传功能

- Spring Boot工程嵌入的tomcat限制了请求的文件大小,
  每个文件的配置最大为1Mb，单次请求的文件的总数不能大于10Mb。

- 要更改这个默认值需要在配置文件（如application.properties）中加入两个配置

  `spring.servlet.multipart.max-file-size=10MB`

  `spring.servlet.multipart.max-request-size=10MB`

- 当表单的enctype="multipart/form-data"时,可以使用MultipartFile获取上传的文件数据，再通过transferTo方法将其写入到磁盘中

## 拦截器

- 拦截器在Web系统中非常常见，对于某些全局统一的操作，我们可以把它提取到拦截器中实现。总结起来，拦截器大致有以下几种使用场景:
- 权限检查:如登录检测，进入处理程序检测是否登录，如果没有，则直接返回登录页面。
- 性能监控:有时系统在某段时间莫名其妙很慢，可以通过拦截器在进入处理程序之前记录开始时间，在处理完后记录结束时间，从而得到该请求的处理时间
- 通用行为:读取cookie得到用户信息并将用户对象放入请求,从而方便后续流程使用，还有提取Locale、Theme信息等，只要是多个处理程序都需要的，即可使用拦截器实现。

### 拦截器定义

```java
public class LoginIntercetor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("LoginInterceptor");
        return true;
    }

}
```

- Spring Boot定义了HandlerInterceptor接口来实现自定义拦截器的功能
- Handlerlnterceptor接口定义了preHandle、postHandle、afterCompletion三种方法，通过重写这三种方法实现请求前、请求后等操作

### 拦截器注册

- addPathPatterns方法定义拦截的地址
- excludePathPatterns定义排除某些地址不被拦截
- 添加的一个拦截器没有addPathPattern任何一个url则默认拦截所有请求
- 如果没有excludePathPatterns任何一个请求，则默认不放过任何一个请求

```java
@Configuration
public class Webconfigurer implements WebMvcconfigurer {
    @override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LoginInterceptor()).addPathPatterns(" /user/**");
    }
}

```

# RESTful服务和Swagger



## RESTful介绍

- RESTful是目前流行的互联网软件服务架构设计风格。
- REST (Representational State Transfer，表述性状态转移)一词是由RoyThomas Fielding在2000年的博士论文中提出的，它定义了互联网软件服务的架构原则，如果一个架构符合REST原则，则称之为RESTful架构。
- REST并不是一个标准，它更像一组客户端和服务端交互时的架构理念和设计原则，基于这种架构理念和设计原则的Web API更加简洁，更有层次。

### RESTful的特点

- 每一个URI代表一种资源
- 客户端使用GET、POST、PUT、DELETE四种表示操作方式的动词对服务端资源进行操作:GET用于获取资源，POST用于新建资源（也可以用于更新资源),PUT用于更新资源，DELETE用于删除资源。
- 通过操作资源的表现形式来实现服务端请求操作。
- 资源的表现形式是JSON或者HTML。
- 客户端与服务端之间的交互在请求之间是无状态的，从客户端到服务端的每个请求都包含必需的信息。

### RESTful API

- 符合RESTful规范的Web API需要具备如下两个关键特性:
  - 安全性:安全的方法被期望不会产生任何副作用，当我们使用GET操作获取资源时，不会引起资源本身的改变，也不会引起服务器状态的改变。
  - 幂等性:幂等的方法保证了重复进行一个请求和一次请求的效果相同(并不是指响应总是相同的，而是指服务器上资源的状态从第一次请求后就不再改变了)，在数学上幂等性是指N次变换和一次变换相同。

## HTTP Method

- HTTP提供了POST、GET、PUT、DELETE等操作类型对某个Web资源进行Create、Read、Update和Delete操作。

- 一个HTTP请求除了利用URI标志目标资源之外，还需要通过HTTP Method指定针对该资源的操作类型，一些常见的HTTP方法及其在RESTful风格下的使用:

  ![image-20231024172806501](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/202310241728598.png)

### HTTP状态码

- HTTP状态码就是服务向用户返回的状态码和提示信息，客户端的每一次请求，服务都必须给出回应，回应包括HTTP状态码和数据两部分。
- HTTP定义了40个标准状态码，可用于传达客户端请求的结果。状态码分为以下5个类别:
- 1xx:信息，通信传输协议级信息
- 2xx:成功，表示客户端的请求已成功接受
- 3xx:重定向，表示客户端必须执行一些其他操作才能完成其请求4xx:客户端错误，此类错误状态码指向客户端
- 5xx:服务器错误，服务器负责这写错误状态码

### Spring Boot实现RESTful API

- Spring Boot提供的spring-boot-starter-web组件完全支持开发RESTful API,提供了与REST操作方式(GET、POST、PUT、DELETE)对应的注解。
- @GetMapping:处理GET请求，获取资源。
- @PostMapping:处理POST请求，新增资源。
- @PutMapping:处理PUT请求，更新资源。
- @DeleteMapping:处理DELETE请求，删除资源。
- @PatchMapping:处理PATCH请求，用于部分更新资源。

- 在RESTful架构中，每个网址代表一种资源，所以URI中建议不要包含动词，只包含名词即可，而且所用的名词往往与数据库的表格名对应。

- 用户管理模块API示例:

  ![image-20231024173101598](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/202310241731644.png)

## 什么是Swagger

- Swagger是一个规范和完整的框架，用于生成、描述、调用和可视化RESTful风格的Web服务，是非常流行的API表达工具。
- Swagger能够自动生成完善的RESTful API文档,，同时并根据后台代码的修改同步更新，同时提供完整的测试页面来调试API。

- 使用Swagger生成Web API文档

  在Spring Boot项目中集成Swagger同样非常简单，只需在项目中引入springfox-swagger2和springfox-swagger-ui依赖即可。

### 配置Swagger

- 注意事项
  Spring Boot 2.6.X后与Swagger有版本冲突问题，需要在
  application.properties中加入以下配置:
  spring.mvc.pathmatch.matching-strategy=ant_path_matcher

### 使用Swagger2进行接口测试

启动项目访问http://127.0.0.1:8080/swagger-ui.html，即可打开自动生成的可视化测试页面

### Swagger常用注解

Swagger提供了一系列注解来描述接口信息，包括接口说明、请求方法、请求参数、返回信息等

![image-20231024195659739](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/202310241956826.png)

# MyBatis快速上手

数据库工具可以选择DBeaver或者Navicat

## ORM介绍

- ORM (Object Relational Mapping，对象关系映射)是为了解决面向对象与关系数据库存在的互不匹配现象的一种技术。
- ORM通过使用描述对象和数据库之间映射的元数据将程序中的对象自动持久化到关系数据库中。
- ORM框架的本质是简化编程中操作数据库的编码。

## 添加依赖

- mybatis-plus-boot-starter
- mysql-connector-java
- druid-spring-boot-starter

## 全局配置

- 配置数据库相关信息

  ```properties
  spring.datasource.type=com.a1ibaba.druid.poo1.DruidDatasource
  spring.datasource.driver-class-name=com.mysq1.jdbc.Driver
  spring.datasource.ur1=jdbc:mysql://localhost:3306/mydb?usessL=false
  spring.datasource.username=root
  spring.datasource.password=root
  mybatis-p1us.configuration.1og-impl=org.apache.ibatis.logging.stdout.stdoutImpl
  ```

  ```yml
  spring:
    datasource:
      type: com.alibaba.druid.pool.DruidDataSource
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://local:3306/mydb?useSSL=false
      username: root
      password: 123456
  mybatis-plus:
    configuration:
      log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
  ```

- 添加@MapperScan注解

  ```java
  @SpringBootApplication
  @MapperScan("com.example.helloworld.mapper")
  public class HelloworldApplication {
      public static void main(String[] args) {
          SpringApplication.run(HelloworldApplication.class, args);
      }

  }
  ```

## MyBatis的注解开发

### 常见注解

| 注解     | 功能                                  |
| -------- | ------------------------------------- |
| @Insert  | 实现插入                              |
| @Update  | 实现更新                              |
| @Delete  | 实现删除                              |
| @Select  | 实现查询                              |
| @Result  | 实现结果集封装                        |
| @Results | 可以和@Result一起使用，封装多个结果集 |
| @One     | 实现一对一结果集封装                  |
| @Many    | 实现一对多结果集封装                  |

### Mapper实现

```java
@Mapper
public interface UserMapper {
    @Insert("insert into user values(#{id}, #{username}, #{password}, #{birthday})")
    int insert(User user);

    @Delete("delete from user where id=#{id}")
    int delete(int id);

    @Update("update user")
    int update(User user);

    @Select("select * from user")
    User UserById(int id);

    @Select("select * from user")
    List<User> getAll();
}

```

# 多表查询及分页查询

实现复杂关系映射，可以使用@Results注解，@Result注解，@One注解，@Many注解组合完成复杂关系的配置。

## 分页查询

编写配置文件

```java
@
```



