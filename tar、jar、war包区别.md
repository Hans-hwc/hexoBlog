---
title: tar、jar、war包区别
categories: 
- Java
tags:
- tar
- jar
- war
---
#### 前言:
在部署包的时候，经常会看到很多类型的包，其中常见的有tar包、jar包、war包等，那么这三种类型的包有什么区别？

#### 区别：
tar包：
linux打包工具生成的包通常用tar作为后缀，tar包不一定有压缩，其实可以压缩，也可以不压缩，例如xxx.tar.gz，就表示这个tar包是压缩的，并且使用的压缩算法是GNU ZIP，而xxx.tar.bz2就表示这个包使用了bzip2算法进行压缩，当然这样的命名只是一种惯例，并非强制。简单地说，linux下的tar命令就仅是打包。

jar包：
Java Archive，Java编译好之后生成的class文件的包，由于直接发布这些class文件不是很方便，所以就会把许多的class文件打包成一个jar，jar中除了class文件还可以包括一些资源和配置文件，通常一个jar包就是一个java程序或者一个java库。

war包：
Web application  Archive，与jar基本相同，但它通常表示这是一个Java的Web应用程序的包，tomcat这种Servlet容器会认出war包并自动部署。