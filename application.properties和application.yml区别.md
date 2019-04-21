---
title: application.properties和application.yml文件的区别
categories: 
- SpringBoot
tags:
- springboot
---
#### 关于
一般上来说，当我们创建一个SpringBoot项目时，IDE会默认帮我们创建一个application.properties配置文件。有些朋友习惯把.properties文件改成.yml文件。那么这两种文件类型有什么区别呢？

#### 区别
1.内容格式比较：
.properties文件，通过.来连接，通过=来赋值，结构上，没有分层的感觉，但比较直接。
.yml文件，通过：来分层，结构上，有比较明显的层次感，最后key赋值的：后需要留一个空格

2.执行顺序
如果工程中同时存在application.properties文件和 application.yml文件，yml文件会先加载，而后加载的properties文件会覆盖yml文件。所以建议工程中，只使用其中一种类型的文件即可。

#### 案例
application.properties：
```
server.port=8081
 
spring.datasource.type=org.apache.tomcat.jdbc.pool.DataSource
spring.datasource.url=jdbc:mysql://aliyuncs.com:3306/database?useUnicode=true&zeroDateTimeBehavior=convertToNull&autoReconnect=true
spring.datasource.username=root
spring.datasource.password=******
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```

application.yml：
```
server:
  port: 8082
  
spring:
    datasource:
        name: test
        url: jdbc:mysql://127.0.0.1:3306/database
        username: root
        password: ******
        type: com.alibaba.druid.pool.DruidDataSource
        driver-class-name: com.mysql.jdbc.Driver
```
