---
title: Hexo增加搜索功能
categories: 
- Hexo
tags:
- hexo
---
#### 关于
随着时间的推移，个人站点的博客文章会越来越多，那怎么样才能快速找到你印象中的文章呢？增加一个站点内的搜索功能是非常有必要和方便的。

#### 具体操作
1.安装搜索：在Hexo的根目录下，打开命令可执行窗口，执行如下命令：
```
npm install hexo-generator-searchdb --save
```

2.全局配置文件_config.yml，新增如下内容：
```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

3.hexo主题配置文件（\themes\next\_config.yml），修改local_search的enable为true：
```
# Local search
# Dependencies: https://github.com/flashlab/hexo-generator-search
local_search:
  enable: true
  # if auto, trigger search by changing input
  # if manual, trigger search by pressing enter key or search button
  trigger: auto
  # show top n results per article, show all results by setting to -1
  top_n_per_article: 1
```