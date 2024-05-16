# SpringBoot2基础入门

## 02、入门

### 1、翻看[Spring](https://spring.io)官网

- https://spring.io/projects/spring-boot#learn

- https://docs.spring.io/spring-boot/docs/2.7.10-SNAPSHOT/reference/html/getting-started.html#getting-started

### 2、导入依赖

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.7.9</version>
</parent>

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

### 3、Hello world

在src>main>java下创建文件com.example.boot.MainApplication.java并在boot下创建文件controller.HelloController.java

```java
// MainApplication.java
/**
 * 主程序类
 * @SpringBootApplication：这是一个Springboot应用
 */
@SpringBootApplication
public class MainApplication {
    public static void main(String[] args) {
        SpringApplication.run(MainApplication.class,args);
    }
}

//HelloController.java

//@ResponseBody
//返回字符字符串
//@Controller

@RestController
//@RestController 是 @Controller 和 @ResponseBody 的结合
public class HelloController {
    @RequestMapping("/fuck")
    public String hand01(){
        //return "Hello, Spring Boot 2!";
        return "Fuck you, 冯运佳!";
    }
}

```

### 4、创建一个可执行Jar包

(Creating an Executable Jar)

- 添加插件

    ```xml
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
    ```

- 创建jar包

    运行Maven里面的Lifecycle的clean和package

## 03、自动配置原理

### 1、SpringBoot特点

#### 1.1、依赖管理

+ 父项目做依赖管理

    ```xml
    <!-- 依赖管理 -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.7.9</version>
    </parent>

    <!-- 它的父项目 -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-dependencies</artifactId>
        <version>2.7.9</version>
    </parent>

    <!-- 几乎声明了所有开发中常用的依赖的版本号，自动版本仲裁机制 -->
    ```

+ 开发导入starter场景启动器

    ```xml
    1、见到很多 spring-boot-starter-* : *代表某种场景
    2、只要引入starter，这个场景的所有常规需要的依赖我们都自动引入
    3、Springboot所有支持的场景
    https://docs.spring.io/spring-boot/docs/2.7.10-SNAPSHOT/reference/html/using.html#using.build-systems.starters
    4、见到的 *-spring-boot-starter：第三方为我们提供的简化开发的场景启动器。
    5、所有场景启动器最底层的依赖
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
        <version>2.7.9</version>
        <scope>compile</scope>
    </dependency>
    ```

+ 无需关注版本号，自动版本仲裁

+ 自定义版本号

    ```xml
    1、查看spring-boot-dependencies里面规定当前依赖的版本用的key。
    2、在当前项目里重写配置
    <properties>
        <mysql.version>8.0.32</mysql.version>
    </properties>
    从spring-boot-dependencies里可以找到依赖的版本以及坐标
    ```

#### 1.2、自动配置

+ 自动配好Tomcat

    + 引入Tomcat的依赖
    + 配置Tomcat

+ 自动配好SpringMVC

    + 引入SpringMVC全套组件
    + 自动配好SpringMVC常用组件（功能）

+ 自动配好Web常见的功能，如字符编码问题

    + SpringBoot帮我们配置好了所有web开发的常见场景

+ 默认的包结构

    + 主程序所在的包及其下面的所有子包里面的组件都会被默认扫描进来

    + 无需以前的包扫描配置

    + 想要改变扫描路径，`@SpringBootApplication(scanBasePackages = "com.hunter")`

        + 或者`@ComponentScan("com.hunter")`指定扫描路径

        ```xml
        @SpringBootApplication
        等同于
        @SpringBootConfiguration
        @EnableAutoConfiguration
        @ComponentScan
        ```



+ 各种配置拥有默认值

    + 默认配置最终都是映射到MultipartProperties
    + 配置文件的值最终会绑定每个类上，这个类会在容器中创建对象

+ 按需加载所有自动配置项

    + 非常多的starter
    + 引入了哪些场景这个场景的自动配置才会开启
    + SpringBoot所有自动配置功能都在spring-boot-autoconfigure包里面

+ ……

### 2、容器功能

#### 2.1、组件添加

##### 1、@Configuration

+ 基本使用
+ Full模式与Lite模式
    + 示例
    + 最佳实战
        + 配置类组件之间无依赖关系用Lite模式加速容器启动过程，减少判断
        + 配置类组件之间有依赖关系，方法会被调用得到之前单实例组件，用Full模式

##### 2、@Bean、@Component、@Controller、@Service、@Repository

+ @Bean：表示一个方法实例化、配置或者初始化一个Spring IoC容器管理的新对象。
+ @Component: 自动被component扫描。 表示被注解的类会自动被component扫描
+ @Repository: 用于持久层，主要是数据库存储库。
+ @Service: 表示被注解的类是位于业务层的业务component。
+ @Controller:表明被注解的类是控制component，主要用于展现层 。

+ @Bean与@Component区别
     @Component是 spring 2.5引入的，为了摆脱通过classpath扫描根据xml方式定义的bean的方式.

    @Bean是spring 3.0 引入的，和 @[Configuration](https://so.csdn.net/so/search?q=Configuration&spm=1001.2101.3001.7020)一起工作，为了摆脱原先的xml和java config方式。

    Spring管理Bean方式有两种，一种是注册Bean，一种装配Bean。
     可以通过三种方式实现bean管理，一使用自动配置的方式、二使用JavaConfig的方式、三使用XML配置的方式。

+ @Component与@Service区别
     目前基本没有区别。@Service是一种具体的@Component

+ @Autowired
     自动装配

+ @Component 作用就相当于 XML配置

> 备注:
>  @Resource的作用相当于@Autowired，只不过@Autowired按byType自动注入，而@Resource默认按 byName自动注入罢了。@Resource有两个属性是比较重要的，分是name和type。
>
> Spring将@Resource注解的name属性解析为bean的名字，而type属性则解析为bean的类型。所以如果使用name属性，则使用byName的自动注入策略，而使用type属性时则使用byType自动注入策略。
>
> 如果既不指定name也不指定type属性，这时将通过反射机制使用byName自动注入策略。

##### 3、@ComponentScan.@lmport

```java
 * 4、@Import({User.class, ByteArrayUtil.class})
 *      给容器中自动创建出这两个类型的组件、默认组件的名字就是全类名
 */
@Import({User.class, ByteArrayUtil.class})
@Configuration(proxyBeanMethods = false) //告诉Springboot这是个配置类 == 配置文件
public class MyConfig {
}
```



##### 4、@Conditional

条件装配：满足Conditional指定的条件，则进行组件注入

![image-20230319171104349](../img/image-20230319171104349.png)

```java
@Configuration(proxyBeanMethods = false) //告诉Springboot这是个配置类 == 配置文件
//@ConditionalOnBean(name = "cat")
@ConditionalOnMissingBean(name = "cat")
public class MyConfig {
    /**
     * 外部无论对配置类中这个组件注册方法调用多少次获取的都是之前注册容器中的单实例对象
     * @return
     */

    @Bean //给容器中添加组件。以方法名作为组件的id，返回类型就是组件类型。返回的值，就是组件在容器中的实例。
    public User user01(){
        User zhangsan = new User("zhangsan", 18);
        //User组件依赖了Pet组件
        zhangsan.setPet(tomcatPet());
        return zhangsan;
    }
    @Bean("cat22") //自定义组件名称
    public Pet tomcatPet(){
        return new Pet("tomcat");
    }
}

public class MainApplication {
    public static void main(String[] args) {
        //1、返回ICO容器
        ConfigurableApplicationContext run = SpringApplication.run(MainApplication.class, args);

        //2、查看容器里的组件
        String[] names = run.getBeanDefinitionNames();
        for (String s : names) {
            System.out.println(s);
        }
        boolean cat = run.containsBean("cat");
        System.out.println("容器中Cat组件: " + cat);

        boolean user01 = run.containsBean("user01");
        System.out.println("容器中的user01组件: " + user01);

        boolean cat22 = run.containsBean("cat22");
        System.out.println("容器中的Cat组件: " + cat22);
    }
}

```



#### 2.2、原生配置文件引入

##### 1、@ImportResource

```xml
================MyConfig.java====================
@ImportResource("classpath:beans.xml")
==================bean.xml=======================
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="haha" class="com.hunter.boot.bean.User">
        <property name="name" value="zhangsan"></property>
        <property name="age" value="18"></property>
    </bean>

    <bean id="hehe" class="com.hunter.boot.bean.Pet">
        <property name="name" value="tomcat"></property>
    </bean>

</beans>
```

#### 2.3、属性值绑定

如何使用Java读取到properties文件的内容，并且把它封装到JavaBean中，以供随时使用；

```java
public class getProperties {
    public static void main(String[ ] args) throws FileNotFoundException，IOException {
        Properties pps = new Properties();
        pps.load(new FileInputstream("a.properties"));
        Enumeration enum1 = pps.propertyNames(); //得到配置文件的名字
        while(enum1.hasMoreElements()) {
            String strKey = (String)enum1.nextElement();
            string strValue = pps.getProperty(strKey);
            System.out.println(strKey + "="+ strValue);
            //封装到JavaBean。
        }
    }
}
```

##### 1、@ConfigurationProperties

##### 2、@EnableConfigurationProperties + @ConfigurationProperties

```java
@EnableConfigurationProperties(Car.class)
//1、开启Car属性配置功能
//2、把这个Car这个组件自动注册到容器中
//人家类没标Component
public class MyConfig {
}
```

##### 3、@Component + @ConfigurationProperties

```java
@Component
@ConfigurationProperties(prefix = "mycar")
```

### 3、自动配置原理入门

#### 3.1、引导加载自动配置类

```java
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(
    excludeFilters = {@Filter(
    type = FilterType.CUSTOM,
    classes = {TypeExcludeFilter.class}
), @Filter(
    type = FilterType.CUSTOM,
    classes = {AutoConfigurationExcludeFilter.class}
)}
)
public @interface SpringBootApplication{}

===================================

```

##### 1、@SpringBootConfiguration

```java
@Configuration。代表当前是一个配置类
@Indexed
```

##### 2、@ComponentScan

指定扫描哪些，Spring注解；

##### 3、@EnableAutoConfiguration

```java
@AutoConfigurationPackage
@Import({AutoConfigurationImportSelector.class})
public @interface EnableAutoConfiguration {}
```

###### 1、@AutoConfigurationPackage

自动配置包？

```java
@Import({Registrar.class})
public @interface AutoConfigurationPackage {}

//利用Registrar给容器中导入一系列组件
//将指定的一个包下的所有组件导入进来？MainApplication所在包下。
```

#### 3.2、按需开启自动配置项

#### 3.3、定制化修改自动配置

#### 3.4、最佳实践

+ 引入场景依赖
    + https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.build-systems.starters
+ 查看自动配置了哪些（选做）
    + 自己分析，引入场景对应的自动配置一般都生效了
    + 在配置文件中写入`debug=true`，开启自动配置报告。Negative（不生效） \ Positive（生效）
+ 是否需要定制化
    + 参照文档修改配置项
        + https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#appendix.application-properties
        + 自己分析。xxxProperties绑定了配置文件的哪些
    + 自定义加入或者替换组件
        + @Bean、@Component……
    + 自定义器 xxxCustomizer（ServletWebServerFactoryCustomizer）

### 4、开发小技巧

#### 4.1、Lombok

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
</dependency>
并搜索安装lombok插件
```

- `@Getter` / `@Setter`
  在类或字段上添加该注解，即可自动生成getters和setters方法。
- `@ToString`
  在类上添加该注解后，会自动生成toString方法，可以打印出对象的属性值。
- `@EqualsAndHashCode`
  在类上添加该注解后，会自动生成equals和hashCode方法。
- `@NoArgsConstructor` 和 `@AllArgsConstructor`
  当类中无参构造方法和全参构造方法都存在时，添加该注解可以自动生成无参构造方法或全参构造方法。
- `@RequiredArgsConstructor`
  在final类型的成员变量上添加该注解，可以自动生成构造方法，并将这些final成员变量作为参数传入构造方法。
- `@Data`
  在类上添加该注解，等价于同时添加`@Getter、@Setter、@ToString、@EqualsAndHashCode`注解。
- `@Builder`
  在类上添加该注解，在建造者模式中使用，可以使用链式调用来构建对象。

```java
===============简化日志开发========================
@Slf4j
@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String handle01(@RequestParam("name") String name){
        log.info("请求进来了……");
        return "Hello, Spring Boot 2!"+"你好"+name;
    }
}
```

#### 4.2、Spring Initailizr（项目初始化向导）

idea创建项目或模板的时候有Spring Initailizr

<!--4.3、dev-tools-->

# SpringBoot2核心功能

## 04、配置文件

### 1、文件类型

#### 1.1、properties

同以前的properties用法

#### 1.2、yaml

##### 1.2.1、简介

YAML是“YAML Ain't Markup Language” (YAML 不是一种标记语言）的递归缩写。在开发的这种语言时，YAML的意思其实是:"Yet Another Markup Language"(仍是一种标记语言）。

非常适合用来做以数据为中心的配置文件

##### 1.2.2、基本语法

+ key: value; kv之间有空格。
+ 大小写敏感
+ 使用缩进表示层级关系
+ 缩进不允许使用tab，只允许空格
+ 缩进的空格数不重要，只要相同层级的元素左对齐即可。"#'表示注释
+ "与""表示字符串内容会被转义/不转义

##### 1.2.3、数据类型

+ 字面量：单个的、不可再分的值。date、boolean、string.number、null

    ```yaml
     k: v
    ```

+ 对象：键值对的集合。map、 hash、set、object

    ```yaml
    行内写法：	k: {k1:v1,k2:v2,k3:v3}
    #或
    k:
    	k1: v1
    	k2: v2
    	k3: v3
    ```

+ 数组：一组按次序排列的值。array、list、queue

    ```yaml
    行内写法：	k: [v1,v2,v3]
    #或者
    k:
    	- v1
    	- v2
    	- v3
    ```

## 05、Web开发

### 1、Spring MVC 自动配置概览

Spring MVC Auto-configuration
Spring MVC 自动配置

Spring Boot provides auto-configuration for Spring MVC that **works well with most applications.（大多场景我们都无需自定义配置）**
Spring Boot为SpringMVC提供了自动配置功能，可以与大多数应用程序配合使用。

The auto-configuration adds the following features on top of Spring’s defaults:
自动配置在Spring的默认值之上添加了以下特性：

+ Inclusion of `ContentNegotiatingViewResolver` and `BeanNameViewResolver` beans.
    包含 `内容协商视图解析器`和`BeanName视图解析器`。
+ Support for serving static resources, including support for WebJars (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#web.servlet.spring-mvc.static-content)).
    支持提供**静态资源**，包括支持WebJars（[本文档稍后将介绍](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#web.servlet.spring-mvc.static-content)）.
+ Automatic registration of `Converter`, `GenericConverter`, and `Formatter` beans.
    自动注册 `Converter` 、 `GenericConverter` 、`Formatter`。
+ Support for `HttpMessageConverters` (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#web.servlet.spring-mvc.message-converters)).
    支持 `HttpMessageConverters` （[本文档稍后将介绍](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#web.servlet.spring-mvc.message-converters)）。
+ Automatic registration of `MessageCodesResolver` (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#web.servlet.spring-mvc.message-codes)).
    自动注册 `MessageCodesResolver` （[本文档稍后将介绍](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#web.servlet.spring-mvc.message-codes)）。(国际化用)
+ Static `index.html` support.
    支持静态 `index.html`。
+ Automatic use of a `ConfigurableWebBindingInitializer` bean (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#web.servlet.spring-mvc.binding-initializer)).
    自动使用 `ConfigurableWebBindingInitializer`（[本文档稍后将介绍](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#web.servlet.spring-mvc.binding-initializer)）。(DataBinder负责将请求数据绑定到JavaBean上)

> If you want to keep those Spring Boot MVC customizations and make more [MVC customizations](https://docs.spring.io/spring-framework/docs/6.0.6/reference/html/web.html#mvc) (interceptors, formatters, view controllers, and other features), you can add your own `@Configuration` class of type `WebMvcConfigurer` but **without** `@EnableWebMvc`.
>
> 不用@EnableWebMvc注解。使用@Configuration + WebMvcConfigurer 自定义规则

> If you want to provide custom instances of `RequestMappingHandlerMapping`, `RequestMappingHandlerAdapter`, or `ExceptionHandlerExceptionResolver`, and still keep the Spring Boot MVC customizations, you can declare a bean of type `WebMvcRegistrations` and use it to provide custom instances of those components.
>
> 声明 WebMvcRegisytration 改变默认底层组件

> If you want to take complete control of Spring MVC, you can add your own `@Configuration` annotated with `@EnableWebMvc`, or alternatively add your own `@Configuration`-annotated `DelegatingWebMvcConfiguration` as described in the Javadoc of `@EnableWebMvc`.
>
> 使用 @EnableWebMvc+@Configuration+DelegatingWebMvcConfiguration 全面接管SpringMVC

| Spring MVC uses a different `ConversionService` to the one used to convert values from your `application.properties` or `application.yaml` file. It means that `Period`, `Duration` and `DataSize` converters are not available and that `@DurationUnit` and `@DataSizeUnit` annotations will be ignored.  If you want to customize the `ConversionService` used by Spring MVC, you can provide a `WebMvcConfigurer` bean with an `addFormatters` method. From this method you can register any converter that you like, or you can delegate to the static methods available on `ApplicationConversionService`. |
| ------------------------------------------------------------ |

### 2、简单功能分析

#### 2.1、静态资源访问

##### 1、静态资源目录

类路径下 called `/static` (or `/public` or `/resources` or `/META-INF/resources`
访问：当前项目根目录/ + 静态资源名

原理：静态映射/**
请求进来，先去找Controller看能不能处理。不能处理的所有请求又都交给静态资源处理器。静态也找不到返回404。

改变默认的静态资源路径

```yaml
spring:
  web:
    resources:
      static-locations: classpath:/haha/
```

##### 2、静态资源访问前缀

默认无前缀

建议在application中配置`spring.mvc.static-path-pattern=/resources/**`，给静态页面一个访问前缀

```yaml
spring:
  mvc:
    static-path-pattern: /res/**
```

当前目录 + static-path-pattern + 静态资源名 = 静态资源文件夹

##### 3、webjar

自动映射

https://www.webjars.org/

```xml
<dependency>
    <groupId>org.webjars.npm</groupId>
    <artifactId>jquery</artifactId>
    <version>3.6.4</version>
</dependency>
```

访问地址：http://localhost:8080/webjars/**jquery/3.6.4/dist/jquery.js** 后面的地址要按照依赖里面的包路径

#### 2.2、欢迎页支持

+ 静态资源路径下 index.html
    + 可以配置静态资源路径
    + 但是不可以配置静态资源的访问前缀。否则会导致 index.html不能被默认访问

```yaml
spring:
  mvc:
#    static-path-pattern: /res/** #会导致welcome page功能失效
  web:
    resources:
      static-locations: classpath:/haha/
      add-mappings: true
```

+ controller能处理/index （没成功，建议直接映射到"/"）

[【源码分析】SpringBoot 如何访问工程目录下的静态资源？](https://jishuin.proginn.com/p/763bfbd5db18)

#### 2.3、自定义 Favicon

favicon.ico 放在静态资源目录下即可

```yaml
spring:
  mvc:
    static-path-pattern: /res/** #此会导致 Favicon 功能失效
```

### 3、请求参数处理

1、普通参数与基本注解

+ 注解：

    @PathVariable、@RequestHeader、@ModelAttribute、@RequestParam、@MatrixVariable、@CookieValue、@RequestBody



    @PathVariable：路径变量

    @RequestHeader：获取请求头

    @ModelAttribute：

    @RequestParam：获取请求参数

    @MatrixVariable：矩阵变量

    @CookieValue：获取cookie值

    @RequestBody：获取请求体

+ Servlet API:

    WebRequest、ServletRequest、MultipartRequest、HttpSession、javax.servlet.http.PushBuilder、Principal、InputStream、Reader、HttpMethod、Locale、TimeZone、Zoneld

+ 复杂参数:

    Map、Errors/BindingResult、Model、RedirectAttributes、ServletResponse、SessionStatus、UriComponentsBuilder、ServletUriComponentsBuilder

+ 自定义对象参数:

    可以自动类型转换与格式化，可以级联封装。



+ SpringBoot启动默认加载 xxxAutoConfiguration 类 (自动配置类)
+ SpringMNE功能的自动配置类WebMvcAutoConfiguration，生效

```java
@AutoConfiguration(
    after = {DispatcherServletAutoConfiguration.class, TaskExecutionAutoConfiguration.class, ValidationAutoConfiguration.class}
)
@ConditionalOnWebApplication(
    type = Type.SERVLET
)
@ConditionalOnClass({Servlet.class, DispatcherServlet.class, WebMvcConfigurer.class})
@ConditionalOnMissingBean({WebMvcConfigurationSupport.class})
@AutoConfigureOrder(-2147483638)
public class WebMvcAutoConfiguration {}
```

+ 给容器中配了什么

```java
@Configuration(
        proxyBeanMethods = false
)
@Import({WebMvcAutoConfiguration.EnableWebMvcConfiguration.class})
@EnableConfigurationProperties({WebMvcProperties.class, WebProperties.class})
@Order(0)
```

+ 配置文件的相关属性和xxx进行了绑定。WebMvcProperties= =**spring.mvc**、WebProperties= =**spring.web**
    +



1、配置类只有一个有参构造器

```java
//有参构造器所有参数的值都会从容器中确定
// WebProperties webProperties：获取和spring.web绑定的所有的值的对象
// WebMvcProperties mvcProperties：获取和spring.mvc绑定的所有的值的对象
// ListableBeanFactory beanFactory Spring的beanFactory
// HttpMessageConverters 找到所有的HttpMessageConverters
public WebMvcAutoConfigurationAdapter(WebProperties webProperties, WebMvcProperties mvcProperties, ListableBeanFactory beanFactory, ObjectProvider<HttpMessageConverters> messageConvertersProvider, ObjectProvider<WebMvcAutoConfiguration.ResourceHandlerRegistrationCustomizer> resourceHandlerRegistrationCustomizerProvider, ObjectProvider<DispatcherServletPath> dispatcherServletPath, ObjectProvider<ServletRegistrationBean<?>> servletRegistrations) {
    this.resourceProperties = webProperties.getResources();
    this.mvcProperties = mvcProperties;
    this.beanFactory = beanFactory;
    this.messageConvertersProvider = messageConvertersProvider;
    this.resourceHandlerRegistrationCustomizer = (WebMvcAutoConfiguration.ResourceHandlerRegistrationCustomizer)resourceHandlerRegistrationCustomizerProvider.getIfAvailable();
    this.dispatcherServletPath = dispatcherServletPath;
    this.servletRegistrations = servletRegistrations;
    this.mvcProperties.checkConfiguration();
}
```





### 4、响应数据与内容协商

### 5、视图解析与模板引擎

### 6、拦截器

### 7、跨域
