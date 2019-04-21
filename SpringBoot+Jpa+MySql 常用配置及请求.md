---
title: SpringBoot+Jpa+MySql 常用配置及请求
categories: 
- SpringBoot
tags:
- springboot
---
#### 关于
这篇文章，介绍SpringBoot常用的配置和请求处理。大致分成三个部分介绍：常用的请求方式、Jpa配置、MySql配置。

#### 常用的请求方式
如下是常用的几种请求方式：
get请求：一般用于查询数据，获取一些非重要性的信息。
post请求：一般用于插入数据。
put请求：一般用于数据更新。
delete请求：一般用于数据删除。

那么，在SpringBoot中，怎么对这些请求方式进行处理。（这里以最常用的get、post请求为例，其他的类似）

**get请求：**
```
//get请求，获取url路径上的参数 @PathVariable
//注：localhost：8080/test/11/hans
@RequestMapping(value = "/test/{id}/{name}", method = RequestMethod.GET)
public String sayHello(@PathVariable("id") Integer id, @PathVariable("name") String name) {
    return "id:" + id + " name:" + name;
}

//get请求，获取url请求参数的值 @RequestParam
//localhost:8080/test?id=99
@RequestMapping(value = "/test", method = RequestMethod.GET)
public String sayHello(@RequestParam Integer id) {
    return "id:" + id;
}

//get请求，获取url请求参数的值，增加参数映射，默认值 @RequestParam
//required=false 表示url中可以无id参数，此时就使用默认参数
@RequestMapping(value = "/test2", method = RequestMethod.GET)
public String sayHello2(@RequestParam(value = "id", required = false, defaultValue = "1") Integer id) {
    return "id:" + id;
}
```

**post请求：**
```
//post请求
//表单参数
@RequestMapping(value= "/getMessage", method = RequestMethod.POST)
public String getMessage(int code, String message)  {
    return "success";
}

//post请求
//json raw参数
@PostMapping(value= "/getMessageBody")
public String getMessagePost(@RequestBody HolidayEntity bean)  {
    return "success";
}

//匹配参数
//password如果匹配对，@RequestParam不写都ok
public void login(@RequestParam("account") String name, @RequestParam String password) {
    System.out.println(name + ":" + password);
}

//@RequestHeader注解用来将请求头的内容绑定到方法参数上。
@PostMapping(value = "login")
public void login2(@RequestHeader("access_token") String accessToken,@RequestParam String name) {
    System.out.println("accessToken:" + accessToken);
}
```

**补充：**
```
组合注解(RequestMapping的变形)
@GetMapping = @RequestMapping(method = RequestMethod.GET)
@PostMapping = @RequestMapping(method = RequestMethod.POST)
@PutMapping = @RequestMapping(method = RequestMethod.PUT)
@DeleteMapping = @RequestMapping(method = RequestMethod.DELETE)
```


#### Jpa配置
1.pom文件加入Jpa配置
```
<!--jpa-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

2.Application入口类增加@EnableJpaRepositories注解
```
@EnableJpaRepositories
public class Application extends SpringBootServletInitializer {
```

3.dao接口
```
@Repository
public interface HolidayRepository extends JpaRepository<HolidayEntity, Long> {

    @Query(value = "SELECT p FROM HolidayEntity p")
    List<HolidayEntity> queryHoliday();

}
```

4.entity类
```
@Entity
@Table(name = "holiday_scheme")
@EntityListeners(AuditingEntityListener.class)
public class HolidayEntity extends AbstractPersistable<Long> {
    @Column(name = "date")
    public String date;
    @Column(name = "hour")
    public String hour;
    @Column(name = "holiday")
    public String holiday;
    @Column(name = "holiday_explain")
    public String holiday_explain;
    @Column(name = "type")
    public String type;//SUB假期，ADD调休

    public String getDate() {
        return date;
    }

    public void setDate(String date) {
        this.date = date;
    }

    public String getHour() {
        return hour;
    }

    public void setHour(String hour) {
        this.hour = hour;
    }

    public String getHoliday() {
        return holiday;
    }

    public void setHoliday(String holiday) {
        this.holiday = holiday;
    }

    public String getHoliday_explain() {
        return holiday_explain;
    }

    public void setHoliday_explain(String holiday_explain) {
        this.holiday_explain = holiday_explain;
    }

    public String getType() {
        return type;
    }

    public void setType(String type) {
        this.type = type;
    }

    @Override
    public String toString() {
        return "HolidayEntity{" +
                "date='" + date + '\'' +
                ", hour='" + hour + '\'' +
                ", holiday='" + holiday + '\'' +
                ", holiday_explain='" + holiday_explain + '\'' +
                ", type='" + type + '\'' +
                '}';
    }
}
```

5.执行，获取数据
```
@Autowired
private HolidayRepository holidayRepository;

@RequestMapping("/test")
@ResponseBody
public List<HolidayEntity> test() {
    return holidayRepository.findAll();
}
```


#### MySql配置
1.pom文件加入MySql配置
```
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.46</version>
</dependency>
```

2.application.properties文件配置MySql相关
```
# tomcat配置
server.port=8090

# 数据库配置
#Mysql属性配置文件,Spring-boot系统配置
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.datasource.url=jdbc:mysql://*.*.*.*:3306/db?autoReconnect=true&amp;useUnicode=true&amp;characterEncoding=UTF-8&amp;useSSL=false&amp;useLegacyDatetimeCode=false&amp;serverTimezone=Asia/Shanghai
spring.datasource.username=***
spring.datasource.password=***

#配置自动建表：updata:没有表新建，有表更新操作,控制台显示建表语句
#spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5InnoDBDialect
#如下的配置会导致报错 Unable to build Hibernate SessionFactory
#spring.jpa.properties.hibernate.hbm2ddl.auto=validate
```

[目录导航](https://www.jianshu.com/p/d44c9e717eb3)
[源码](https://github.com/huangweicai/SpringBootAll)