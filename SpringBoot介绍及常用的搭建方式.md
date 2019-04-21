---
title: SpringBoot介绍及常用的搭建方式
categories: 
- SpringBoot
tags:
- springboot
---

#### SpringBoot简介
Spring Boot是Spring社区发布的一个开源项目，旨在帮助开发者快速并且更简单的构建项目。它使用习惯优于配置的理念让你的项目快速运行起来，使用Spring Boot很容易创建一个独立运行（运行jar，内置Servlet容器，Tomcat、jetty）、准生产级别的基于Spring框架的项目，使用SpringBoot你可以不用或者只需要很少的配置文件。

#### SpringBoot核心功能
- 独立运行的Spring项目：可以以jar包形式独立运行，通过java -jar xx.jar即可运行。
- 内嵌Servlet容器：可以选择内嵌Tomcat、Jetty等。
- 提供starter简化maven配置：一个maven项目，使用了spring-boot-starter-web时，会自动加载Spring Boot的依赖包。
- 自动配置Spring：Spring。 Boot会根据在类路径中的jar包、类，为jar包中的类自动配置Bean。
- 准生产的应用监控：提供基于http、ssh、telnet对运行时的项目进行监控。
- 无代码生成和xml配置：主要通过条件注解来实现。

#### SpringBoot项目搭建
这里使用maven进行项目搭建，有几种搭建方式
1、http://start.spring.io/，
填写相关的项目信息、jdk版本等，就会生成一个maven项目的压缩包，下载解压导入IDE就可以。

2、IDE下直接创建，推荐使用STS(Spring Tool Suite)、IntelliJ IDEA均支持直接搭建，STS是Spring基于eclipse进行二次开发的工具。

Spring Tool Suite　：新建Spring Initializr项目,填写项目信息和选择技术，将项目设置成maven项目。

IntelliJ IDEA：新建Spring Starter project,填写项目信息和选择技术完成maven工程创建。

3、Spring Boot CLI工具，使用命令创建。

4、手工构建maven项目
任意IDE新建空maven项目
修改pom.xml添加Spring Boot的父级依赖Spring-boot-starter-parent，添加之后这个项目就是一个Spring Boot项目了。

#### 项目搭建案例
**案例一：通过IDE直接生成SpringBoot项目**
1.Create New Project 新建项目
![image.png](https://upload-images.jianshu.io/upload_images/2405826-5cdf06c8351ffd8c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.选择新建Spring Initializr项目
![image.png](https://upload-images.jianshu.io/upload_images/2405826-3fdc4c75a1a7cfa6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.填入Group和Artifact
![image.png](https://upload-images.jianshu.io/upload_images/2405826-f07a8a15609a3b93.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.默认Core即可
![image.png](https://upload-images.jianshu.io/upload_images/2405826-83135191f7dd292f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.Finish，即创建完毕SpringBoot项目
![image.png](https://upload-images.jianshu.io/upload_images/2405826-1aa2817631f75bff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6.最终效果如下
![image.png](https://upload-images.jianshu.io/upload_images/2405826-6d5b5b3b7da6bdff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



**案例二：手工构建maven项目并通过修改pom.xml，增加SpringBoot配置，进而使得项目变成SpringBoot项目**

1.创建Maven项目
![image.png](https://upload-images.jianshu.io/upload_images/2405826-6e07003673fc508a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.填入Group和Artifact
![image.png](https://upload-images.jianshu.io/upload_images/2405826-f79631e79b843b39.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.Finish，创建完毕Maven项目
![image.png](https://upload-images.jianshu.io/upload_images/2405826-4b6d06be9b86b35f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.修改Maven项目pom.xml文件，添加SpringBoot配置
<project标签下，增加父级依赖Spring-boot-starter-parent
```
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.1.2.RELEASE</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>
```
补充：Spring-boot-starter-parent是一个特殊的starter，用来提供相关的maven默认依赖，使用之后，常用的包依赖可以省略version标签。

5.增加web支持
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>RELEASE</version>
    <scope>compile</scope>
</dependency>
```
6.增加编译插件
```
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

6.新建SpringbootApplication类，并加入@SpringBootApplication注解，代表开启Spring Boot自动配置
```
@RestController
@SpringBootApplication
public class SpringbootApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootApplication.class, args);
    }

    @RequestMapping("/")
    String index(){
        return "Hello My Spring Boot Demo";
    }
}
```

7.测试效果
启动项目，浏览器输入http://localhost:8080
![image.png](https://upload-images.jianshu.io/upload_images/2405826-568b9053127273d3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

