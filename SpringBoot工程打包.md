---
title: SpringBoot工程打包
categories: 
- SpringBoot
tags:
- springboot
---
#### 关于
在SpringBoot的应用里，最方便的莫过于可以直接把工程打成一个jar/war包，由于内嵌了tomcat，所以可以直接在服务器上启动。而SpringBoot适合前后端分离，所以建议打jar包，在服务器上，通过java -jar xx.jar即可启动。

#### 打包流程
1.在pom文件中添加打包插件
```
<!-- 打包spring boot应用 -->
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <!--配置入口-->
                <mainClass>com.aaa.bbb.Application</mainClass>
            </configuration>
        </plugin>

        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>8</source>
                <target>8</target>
            </configuration>
        </plugin>
    </plugins>
</build>
```

2.Application入口类继承SpringBootServletInitializer抽象类，并实现configure方法。
```
public class Application extends SpringBootServletInitializer {
    
//springboot打包需要
@Override
protected SpringApplicationBuilder configure(
        SpringApplicationBuilder builder) {
    return builder.sources(this.getClass());
}  
```

3.执行打包操作
在Intellij的最右边点击Maven Project，依次操作，先clean，再install。
![](https://note.youdao.com/yws/public/resource/deb65d9809f64da2cf633488c0b702bd/xmlnote/9E3857C801964118BBBF329D26499802/8343)

4.操作完毕后，下面就是SpringBoot打出来的jar包了，快放到服务器上试试吧。
![](https://note.youdao.com/yws/public/resource/deb65d9809f64da2cf633488c0b702bd/xmlnote/FBA518621143446C88C240A3128926F5/8348)

