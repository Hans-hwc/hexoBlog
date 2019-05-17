---
title: SpringBoot+Jpa多数据源配置
categories: 
- SpringBoot
tags:
- springboot
---
#### 关于
有时候，随着业务的发展，项目关联的数据来源会变得越来越复杂，使用的数据库会比较分散，这个时候就会采用多数据源的方式来获取数据。另外，多数据源也有其他好处，例如分布式数据库的读写分离，集成多种数据库等等。下面分享我在实际项目中配置多数据源的案例。

#### 步骤
1.application.yml文件中，配置数据库源。这里primary是主库，secondary是从库。
```
server:
  port: 8089

# 多数据源配置
#primary
spring:
  primary:
    datasource:
      url: jdbc:mysql://127.0.0.1:3306/database1?autoReconnect=true&useUnicode=true&characterEncoding=UTF-8&useSSL=false&useLegacyDatetimeCode=false&serverTimezone=Asia/Shanghai
      username: root
      password: ******
      driver-class-name: com.mysql.jdbc.Driver

  #secondary
  secondary:
    datasource:
      url: jdbc:mysql://127.0.0.1:3306/database1?autoReconnect=true&useUnicode=true&characterEncoding=UTF-8&useSSL=false&useLegacyDatetimeCode=false&serverTimezone=Asia/Shanghai
      username: root
      password: ******
      driver-class-name: com.mysql.jdbc.Driver

  jpa:
    hibernate:
      primary-dialect: org.hibernate.dialect.MySQL5Dialect
      secondary-dialect: org.hibernate.dialect.MySQL5Dialect
    open-in-view: true
    show-sql: true
```

2.创建一个Spring配置类，其中spring.primary.datasource的路径参考yml文件的配置。
```
@Configuration
public class DataSourceConfig {

    @Bean(name = "primaryDataSource")
    @Qualifier("primaryDataSource")
    @ConfigurationProperties(prefix="spring.primary.datasource")
    public DataSource primaryDataSource() {
        return DataSourceBuilder.create().build();
    }

    @Bean(name = "secondaryDataSource")
    @Qualifier("secondaryDataSource")
    @Primary
    @ConfigurationProperties(prefix="spring.secondary.datasource")
    public DataSource secondaryDataSource() {
        return DataSourceBuilder.create().build();
    }

}
```

3.分别创建主库、从库的配置类。
注意：entity包和dao包的配置，以及@Primary注解指定主库。

主库配置类：
```
@Configuration
@EnableTransactionManagement
@EnableJpaRepositories(
        entityManagerFactoryRef = "entityManagerFactoryPrimary",
        transactionManagerRef = "transactionManagerPrimary",
        basePackages = {"com.xxx.xxx.dao.primary"}) //设置Repository所在位置
public class PrimaryConfig {
    @Autowired
    private JpaProperties jpaProperties;

    @Autowired
    @Qualifier("primaryDataSource")
    private DataSource primaryDataSource;

    @Primary
    @Bean(name = "entityManagerPrimary")
    public EntityManager entityManager(EntityManagerFactoryBuilder builder) {
        return entityManagerFactoryPrimary(builder).getObject().createEntityManager();
    }

    @Primary
    @Bean(name = "entityManagerFactoryPrimary")
    public LocalContainerEntityManagerFactoryBean entityManagerFactoryPrimary(EntityManagerFactoryBuilder builder) {
        return builder
                .dataSource(primaryDataSource)
                .properties(getVendorProperties(primaryDataSource))
                .packages("com.infinitus.yunxiao_data.entity.primary") //设置实体类所在位置
                .persistenceUnit("primaryPersistenceUnit")
                .build();
    }


    private Map getVendorProperties(DataSource dataSource) {
        return jpaProperties.getHibernateProperties(dataSource);
    }

    @Primary
    @Bean(name = "transactionManagerPrimary")
    public PlatformTransactionManager transactionManagerPrimary(EntityManagerFactoryBuilder builder) {
        return new JpaTransactionManager(entityManagerFactoryPrimary(builder).getObject());
    }
}
```

从库的配置类：
```
@Configuration
@EnableTransactionManagement
@EnableJpaRepositories(
        entityManagerFactoryRef = "entityManagerFactorySecondary",
        transactionManagerRef = "transactionManagerSecondary",
        basePackages = {"com.infinitus.yunxiao_data.dao.secondary"}) //设置Repository所在位置
public class SecondaryConfig {
    @Autowired
    private JpaProperties jpaProperties;

    @Autowired
    @Qualifier("secondaryDataSource")
    private DataSource secondaryDataSource;

    @Bean(name = "entityManagerSecondary")
    public EntityManager entityManager(EntityManagerFactoryBuilder builder) {
        return entityManagerFactorySecondary(builder).getObject().createEntityManager();
    }

    @Bean(name = "entityManagerFactorySecondary")
    public LocalContainerEntityManagerFactoryBean entityManagerFactorySecondary(EntityManagerFactoryBuilder builder) {
        return builder
                .dataSource(secondaryDataSource)
                .properties(getVendorProperties(secondaryDataSource))
                .packages("com.xxx.xxx.entity.secondary") //设置实体类所在位置
                .persistenceUnit("primaryPersistenceUnit")
                .build();
    }


    private Map getVendorProperties(DataSource dataSource) {
        return jpaProperties.getHibernateProperties(dataSource);
    }

    @Bean(name = "transactionManagerSecondary")
    PlatformTransactionManager transactionManagerSecondary(EntityManagerFactoryBuilder builder) {
        return new JpaTransactionManager(entityManagerFactorySecondary(builder).getObject());
    }

}
```

4.分别创建主、从库dao类。
主dao：
```
@Repository
public interface PrimaryRepository extends JpaRepository<PrimaryEntity, Long> {

    @Query(value = "SELECT p FROM PrimaryEntity p")
    List<PrimaryEntity> queryList();

}
```

从dao：
```
@Repository
public interface SecondaryRepository extends JpaRepository<SecondaryEntity, Long> {

    @Query(value = "SELECT p FROM SecondaryEntity p")
    List<SecondaryEntity> queryList();

}
```

5.分别创建主、从库entity类。
主entity：
```
@Entity
@Table(name = "holiday_scheme")
@EntityListeners(AuditingEntityListener.class)
public class PrimaryEntity extends AbstractPersistable<Long> {
    @Column(name = "date")
    public String date;
    @Column(name = "hour")
    public String hour;
    @Column(name = "holiday")
    public String holiday;
    @Column(name = "holiday_explain")
    public String holiday_explain;

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

    @Override
    public String toString() {
        return "PrimaryEntity{" +
                "date='" + date + '\'' +
                ", hour='" + hour + '\'' +
                ", holiday='" + holiday + '\'' +
                ", holiday_explain='" + holiday_explain + '\'' +
                '}';
    }
}
```

从entity：
```
@Entity
@Table(name = "active_dashboards")
@EntityListeners(AuditingEntityListener.class)
public class SecondaryEntity extends AbstractPersistable<Long> {

    @Column(name = "dashboard_id")
    public String dashboard_id;
    @Column(name = "user_id")
    public String user_id;
    @Column(name = "order_index")
    public String order_index;

    public String getDashboard_id() {
        return dashboard_id;
    }

    public void setDashboard_id(String dashboard_id) {
        this.dashboard_id = dashboard_id;
    }

    public String getUser_id() {
        return user_id;
    }

    public void setUser_id(String user_id) {
        this.user_id = user_id;
    }

    public String getOrder_index() {
        return order_index;
    }

    public void setOrder_index(String order_index) {
        this.order_index = order_index;
    }

    @Override
    public String toString() {
        return "SecondaryEntity{" +
                "dashboard_id='" + dashboard_id + '\'' +
                ", user_id='" + user_id + '\'' +
                ", order_index='" + order_index + '\'' +
                '}';
    }
}
```

6.controller请求获取不同数据库的数据。
```
@RestController
@RequestMapping("/database")
public class MailController {
    private final Logger logger = LoggerFactory.getLogger(this.getClass());

    @Autowired
    PrimaryRepository primaryRepository;
    @Autowired
    SecondaryRepository secondaryRepository;

    @RequestMapping("/primary")
    @ResponseBody
    public String primary() {
        return primaryRepository.queryList().toString();
    }

    @RequestMapping("/secondary")
    @ResponseBody
    public String secondary() {
        return secondaryRepository.queryList().toString();
    }

}
```

#### 注意
下面提两个在配置多数据源时遇到的坑点，一不注意就掉坑了。
1.Application类不需要配置@EnableJpaRepositories注解，会报如下错误。
```
A component required a bean named 'entityManagerFactory' that could not be f
```
2.注意检查dao类，获取数据的方法上格式是否正确，有没有某个字段是表中不存在的，避免启动异常。如下，SecondaryEntity表中是不存在job_name字段的，所以注释掉才能启动成功等。
```
//@Query(value = "SELECT p FROM SecondaryEntity p where p.job_name = ?1")
//List<SecondaryEntity> queryOdcRecord(String job_name);
```

