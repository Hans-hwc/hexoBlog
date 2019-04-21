---
title: hexo主题的个性化设置及评论系统的集成
categories: 
- Hexo
tags:
- hexo
---
### 前言
这篇文章是续<玩Hexo博客，从搭建到百度、谷歌收录全流程>的补充篇，该篇文章主要描述的是Hexo在实际的配置过程中，需要设置的点。以本博客为案例，一步步配置自己喜欢的Hexo显示。

### 正文
#### 修改或新增菜单
打开themes/next/_config.yml 文件，搜索menu关键字，修改对应图标名称或者新增对应menu的图标。
```
menu:
  #首页 default
  home: / || home
  #归档 default
  archives: /archives/ || archive
  #分类
  categories: /categories/ || th
  #标签
  tags: /tags/ || tags
  #相册
  photo_album: /photo_album/ || image
  #友链
  friendly_link: /friendly_link/ || link
  #关于
  about: /about/ || user
```
注意：
1.除了home，archives , /后面都需要手动创建这个页面。
2.图片对应的名称，例如link图标，可以在[hexo个性化icon网站](https://fontawesome.com) 找到。


#### 添加头像
打开 themes/next/_config.yml文件，搜索Sidebar Avatar关键字，去掉avatar 前面的#，并补充自己的头像路径。注意：头像存放路径\themes\next\source\uploads，uploads文件夹如果没有则新建，然后存放头像图片即可读取。
```
# Sidebar Avatar
# in theme directory(source/images): /images/avatar.gif
# in site  directory(source/uploads): /uploads/avatar.gif
avatar: /uploads/hans_icon.jpg
```

#### 上下浏览当前页面时显示当前浏览进度
打开 themes/next/_config.yml ,搜索关键字 scrollpercent ,把 false 改为 true。
```
# Scroll percent label in b2t button
  scrollpercent: true
```
如果想把 top按钮放在侧边栏,打开 themes/next/_config.yml ,搜索关键字 b2t ,把 false 改为 true。
```
# Back to top in sidebar
  b2t: true

  # Scroll percent label in b2t button
  scrollpercent: true
```

#### 设置侧边栏社交链接
打开 themes/next/_config.yml 文件,搜索关键字 social ,然后添加社交站点名称与地址即可。其中，图标可以根据上面菜单图标的方式替换。
```
#社交连接
social:
  GitHub: https://huangweicai.github.io/ || github
  简书: https://www.jianshu.com/u/28a4d1accff3 || book
  Coding: http://lantianwork.coding.me/ || codiepie
  知乎: https://www.zhihu.com/people/wei-c-77-91/activities || certificate
```

#### 开启版权声明
主题配置文件下,搜索关键字 post_copyright , enable 改为 true：
```
# Declare license on posts
post_copyright:
  enable: true
  license: CC BY-NC-SA 4.0
  license_url: https://creativecommons.org/licenses/by-nc-sa/4.0/
```

#### 添加顶部加载条
打开 themes/next/_config.yml ，搜索关键字 pace ,设置为 true ,可以更换加载样式：
```
# Progress bar in the top during page loading.
pace: true
# Themes list:
#pace-theme-big-counter
#pace-theme-bounce
#pace-theme-barber-shop
#pace-theme-center-atom
#pace-theme-center-circle
#pace-theme-center-radar
#pace-theme-center-simple
#pace-theme-corner-indicator
#pace-theme-fill-left
#pace-theme-flash
#pace-theme-loading-bar
#pace-theme-mac-osx
#pace-theme-minimal
# For example
# pace_theme: pace-theme-center-simple
pace_theme: pace-theme-flash #替换更换样式
```

其他的可以参考该文章:
[Hexo+Next个人博客主题优化](https://www.jianshu.com/p/efbeddc5eb19)
