# Maven

## 一、下载

### 1. 官网

https://maven.apache.org/download.cgi

```ps
注意：针对一些老项目 还是尽量采用 3.6.3版本，针对idea各个版本的兼容性就很兼容
0.IDEA 2022 兼容maven 3.8.1及之前的所用版本
1.IDEA 2021 兼容maven 3.8.1及之前的所用版本
2.IDEA 2020 兼容Maven 3.6.3及之前所有版本
3.IDEA 2018 兼容Maven3.6.1及之前所有版本
```

![image-20230202151823741-16753223085961](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/image-20230202151823741-16753223085961.png)

### 2. 配置环境

[![p9xkzmF.png](https://s1.ax1x.com/2023/05/31/p9xkzmF.png)](https://imgse.com/i/p9xkzmF)

在path中添加`%MAVEN_HOME%\bin`

### 3. 检查安装

- cmd 运行 `mvn - v`![image-20230202152251476-16753225725983](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/image-20230202152251476-16753225725983.png)


## 二、手打project

### 1. 项目工程结构

![image-20230202152515853-16753227177254](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/image-20230202152515853-16753227177254.png)

```java
package com.hunter;

public class Demo{
	public String say(String name){
		System.out.println("Hello" + name);
		return "Hello" + " " + name;
	}
}
```

```java
package com.hunter;

import org.junit.Test;
import org.junit.Assert;

public class DemoTest{
    @Test
	public void testSay(){
		Demo d = new Demo();
		String ret = d.say("maven");
		Assert.assertEquals("Hello maven",ret);
	}
}
```

### 2. 新建pom.xml

#### 1. 模板

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion><!-- 固定 -->

    <!-- 父项目（如果使用maven创建父子模块，会自动生成 -->
    <parent>
	    <groupId>在maven中对应的包名</groupId>
	    <artifactId>项目名</artifactId>
	    <version>版本</version>
    </parent>
    <!-- 子项目：本项目 -->
    <groupId>在maven中对应的包名</groupId>
    <artifactId>项目名</artifactId>
    <version>版本</version>
    <packaging>打包方式</packaging>
    <description>项目描述</description>

    <!-- spring-boot-starter-parent：有多个作用，后面会解释 -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.4.RELEASE</version>
        <relativePath/>
    </parent>

    <properties>
        <!-- java.version和maven.compiler.target之间的区别 -->
        <java.version>1.8</java.version>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <maven.compiler.target>1.8</maven.compiler.target>
        <maven.compiler.source>1.8</maven.compiler.source>
        <junit.version>4.10</junit.version>
        <spring.boot.version>2.0.4.RELEASE</spring.boot.version>
        <spring.cloud.version>Finchley.RELEASE</spring.cloud.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>${spring-cloud.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>

        <!-- https://mvnrepository.com/artifact/cn.hutool/hutool-all -->
		<dependency>
		    <groupId>cn.hutool</groupId>
		    <artifactId>hutool-all</artifactId>
		    <version>5.5.8</version>
		</dependency>
    </dependencies>

    <dependencyManagement>
        <dependencies>
            <!--<dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring.cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <dependency>
                <groupId>com.alibaba.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>${alibaba.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency> -->
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring.cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>${spring.boot.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>${nacos.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <dependency>
                <groupId>com.alibaba.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>2.1.0.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <!-- 可忽略，没有没有此配置项，会生成一个默认的格式的名字 -->
        <finalName>这里写打包之后的war包的名字</finalName>

        <!-- 插件 -->
        <plugins>

            <!-- 1.maven-compiler-plugin 插件 ：指定编译版本-->
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>${maven.compiler.plugin.version}</version>
    <configuration>
        <source>${java.version}</source>
        <target>${java.version}</target>
        <encoding>${java.encoding}</encoding>
    </configuration>
</plugin>

            <!-- 2.spring-boot-maven-plugin 插件 -->
            <plugin>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
            <!-- 2.详细说明： 排除SpringBoot jar包中的其他依赖包 -->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
	                <layout>ZIP</layout>
	                <!-- 打包时只包含指定的依赖包 -->
	                <includes>
	                    <!-- jar中不包含其他依赖包 -->
	                    <include>
	                        <groupId>nothing</groupId>
	                        <artifactId>nothing</artifactId>
	                    </include>
	                    <!-- <include>
	                        <groupId>cn.hutool</groupId>
	                        <artifactId>hutool-all</artifactId>
	                    </include> -->
	                </includes>
	                <!-- 打包时去除指定的依赖包 -->
	                <!-- <excludes>
	                    <exclude>
	                        <groupId>cn.hutool</groupId>
	                        <artifactId>hutool-all</artifactId>
	                    </exclude>
	                </excludes> -->
                </configuration>
                <!-- 默认goal，可忽略（打jar包时，不可忽略，加了才能导入第三方依赖包）。在mvn package之后，再次打包可执行的jar/war，同时保留mvn package生成的jar/war为.origin -->
                <executions>
	                <execution>
	                    <goals>
	                        <goal>repackage</goal>
	                    </goals>
	                </execution>
                </executions>
            </plugin>

            <!-- 3.maven-dependency-plugin 插件：拷贝其他依赖到指定目录 -->
            <!-- 在项目发布部署到服务器后，个人认为只需要在第一次运行的时候加上此插件，在去掉之后，将新加的依赖的jar包手动复制到此目录下即可 -->
            <plugin>
	            <groupId>org.apache.maven.plugins</groupId>
	            <artifactId>maven-dependency-plugin</artifactId>
	            <executions>
	                <execution>
	                    <id>copy-dependency</id>
	                    <phase>package</phase>
	                    <goals>
	                        <goal>copy-dependencies</goal>
	                    </goals>
	                    <configuration>
	                       <!--输出目录-->
	                       <outputDirectory>${project.build.directory}/lib</outputDirectory>
	                       <excludeTransitive>false</excludeTransitive>
	                       <stripVersion>false</stripVersion>
	                       <!-- <includeScope>runtime</includeScope> 不知道作用，先放着-->
	                    </configuration>
	                </execution>
	            </executions>
            </plugin>

			<!-- 4.maven-resources-plugin 插件：拷贝资源文件 到指定的resource目录-->
			<!-- 此插件适用于资源文件找不到的情况的可以使用，一般可不使用 -->
			<plugin>
			    <artifactId>maven-resources-plugin</artifactId>
			    <executions>
			        <execution>
			            <id>copy-dependencies</id>
			            <phase>package</phase>
			            <goals>
			                <goal>copy-resources</goal>
			            </goals>
			            <configuration>
			                <!-- 资源文件输出目录 -->
			               <outputDirectory>${project.build.directory}/resources</outputDirectory>
			                <resources>
			                    <resource>
			                        <directory>src/main/resources</directory>
			                        <filtering>true</filtering>
			                        <!--包含的文件-->
			                        <includes>
			                            <include>*/**</include>
			                        </includes>
			                    </resource>
			                </resources>
			            </configuration>
			        </execution>
			    </executions>
			</plugin>

			<!-- 5.maven-jar-plugin 插件：指定配置文件-->
			<plugin>
			    <groupId>org.apache.maven.plugins</groupId>
			    <artifactId>maven-jar-plugin</artifactId>
			    <configuration>
			        <archive>
			            <!-- 生成的jar中，不要包含pom.xml和pom.properties这两个文件 -->
			            <addMavenDescriptor>false</addMavenDescriptor>
			            <manifest>
			                <!-- 是否要把第三方jar加入到类构建路径 -->
			                <addClasspath>true</addClasspath>
			                <!-- 外部依赖jar包的最终位置 -->
			                <classpathPrefix>lib/</classpathPrefix>
			                <!-- 配置项目启动类 -->
			                <mainClass>com.ModeloneApplication</mainClass>
			            </manifest>
			            <!-- 指定配置文件的新目录，如果没有使用maven-resources-plugin插件，该配置项可忽略 -->
			            <manifestEntries>
			                <Class-Path>resources/</Class-Path>
			            </manifestEntries>
			        </archive>
			        <excludes>
			            <!--以target/classes为根目录-->
			            <!--资源文件排除-->
			            <exclude>/*.*</exclude>
			            <!--html页面排除-->
			            <exclude>/templates/</exclude>
			            <!--静态文件排除-->
			            <exclude>/static/</exclude>
			        </excludes>
                    <!-- 比方说。我仅仅想打包com.lala.api*以下的类打包。则配置例如以下-->
                    <includes>
					    <include>**/api/*</include>
				    </includes>
			    </configuration>
			</plugin>
            <!-- 6.maven-war-plugin：打war包-->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>2.6</version>
                <configuration>
                    <failOnMissingWebXml>false</failOnMissingWebXml>
                </configuration>
            </plugin>

        </plugins>

        <!-- 如果没报错，可忽略此配置 -->
        <resources>
            <!--注册webapp目录为资源目录-->
            <resource>
                <directory>src/main/webapp</directory>
                <targetPath>META-INF/resources</targetPath>
                <includes>
                    <include>**/*.*</include>
                </includes>
            </resource>
            <!-- SpringBoot项目整合Mybatis时Mapper.xml文件的存放位置：https://blog.csdn.net/yiguang_820/article/details/117961666 -->
            <resource>
                <directory>src/main/resources</directory>
            </resource>
        </resources>
    </build>
</project>
```

#### 2. 新建

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project
    xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <groupId>com.hunter</groupId>
    <artifactId>project-java</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```

#### 3. 项目构建命令

- Maven构建命令使用mvn开头，后面添加功能参数，可以一次执行多个命令，使用空格分隔


```txt
mvn compile		#编译
mvn clean		#清理
mvn test		#测试
mvn package		#打包
mvn install		#安装到本地仓库
```

## 三、Idea新建项目

### 依赖管理

#### 依赖传递冲突问题

```txt
路径优先:当依赖中出现相同的资源时，层级越深，优先级越低，层级越浅，优先级越高
声明优先:当资源在相同层级被依赖时，配置顺序靠前的覆盖配置顺序靠后的
特殊优先:当同级配置了相同资源的不同版本，后配置的覆盖先配置的
```

#### 可选依赖、排除依赖

- 可选依赖指**对外隐藏**当前所依赖的资源——不透明

```xml
<dependeney>
    <groupId>junit</groupid>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <optional>true</optional>
</dependency>
```

- 排除依赖指**主动断开**依赖的资源，被排除的资源无需指定版本——不需要

```xml
<dependency>
      <groupId>org.example</groupId>
      <artifactId>pro3</artifactId>
      <version>1.0-SNAPSHOT</version>
      <exclusions>
        <exclusion>
          <groupId>log4j</groupId>
          <artifactId>log4j</artifactId>
        </exclusion>
      </exclusions>
</dependency>
```

#### 依赖范围scope

- 各属性作用
  - compile ：作用于编译环境、测试环境、运行环境。
  - test ： 作用于测试环境。典型的就是Junit坐标，以后使用Junit时，都会将scope指定为该值
  - provided ：作用于编译环境、测试环境。我们后面会学习 servlet-api ，在使用它时，必须将 scope 设置为该值，不
    然运行时就会报错
  - runtime ： 作用于测试环境、运行环境。jdbc驱动一般将 scope 设置为该值，当然不设置也没有任何问题
- 依赖的jar默认情况可以在任何地方使用，可以通过scope标签设定其作用范围
- 作用范围
  - 主程序范围有效(main文件夹范围内)
  - 测试程序范围有效(test文件夹范围内)
  - 是否参与打包(package指令范围内)

![image-20230202204249071](https://raw.githubusercontent.com/Hunter9812/Jordan/main/img/image-20230202204249071.png)

- 依赖范围的传递性

  间接依赖打不打包是范围传递的前提条件，间接资源的范围就是直接范围和间接范围的交集
