---
title: sql多表关联查询
categories: 
- 数据库
tags:
- sql
- 关联查询
---
#### 关于
有时候，我们查询数据时，会采用多数据库关联查询的方式。数据库通过连接两张表或多张表查询时，会生成一张临时的中间表，然后返回给用户的就是这张临时表的数据。那么具体怎么操作呢？我们可以采用left join，搭配on、where来实现。

#### 具体
备注：
1.on条件是在生成临时表时使用的条件，它不管on中的条件是否为真，都会返回左边表中的记录。
2.where条件是在临时表生成好后，再对临时表进行过滤的条件。这时已经没有left join的含义（必须返回左边表的记录）了，条件不为真的就全部过滤掉。
```
SELECT * FROM table1 a LEFT JOIN table2 b ON a.Sid = b.Sid WHERE a.Sname="小明"
Select * from aaa a left join bbb b on a.id = b.id and b.name = '111111111';
```

个人案例：选用两表中部分字段
```
SELECT a.project_id AS 项目id,
       b.before_time AS 统计的结束时间,
       b.valid_row_count AS 行数,
       b.add_row_count AS 增加行数,
       b.delete_row_count AS 删除行数
 FROM 
 gitlog_project_app a
 LEFT JOIN
 gitlog_detail b
 ON a.id = b.project_app_id
 order by project_id desc
```
