---
title: Hexo使用不蒜子统计功能失效问题解决
categories: 
- Hexo
tags:
- hexo
---
#### 关于
比较早的时候使用next主题，想要开启站点统计功能（访客、总访问量），只需要找到_config.yml配置文件，把busuanzi_count的enable设置为true即可。但是近期，大概是2018年10月份左右，这个不蒜子的统计功能就失效了。查阅了[不蒜子官方](http://busuanzi.ibruce.info/)的说法，
> “因七牛强制过期『dn-lbstatics.qbox.me』域名，与客服沟通无果，只能更换域名到『busuanzi.ibruce.info』！”

#### 具体操作
1.找到原来不蒜子的域名文件，并替换掉旧的域名。
文件路径：\themes\next\layout\_third-party\analytics\busuanzi-counter.swig，只需要替换src对应的域名即可，如下是替换后的域名。
```
<script async src="https://busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```

2.注意：_config.yml配置文件busuanzi_count是需要打开的。我这里是已经开启过了，只是域名失效了而已。如果默认没有打开，可以参考如下配置。
配置文件路径：\themes\next\_config.yml
```
# Show PV/UV of the website/page with busuanzi.
# Get more information on http://ibruce.info/2015/04/04/busuanzi/
busuanzi_count:
  # count values only if the other configs are false
  enable: true
  # custom uv span for the whole site
  site_uv: true
  site_uv_header: 访客数
  site_uv_footer: 人
  # custom pv span for the whole site
  site_pv: true
  site_pv_header: 总访问量
  site_pv_footer: 次
  # custom pv span for one page only
  page_pv: true
  page_pv_header: <i class="fa fa-file-o"></i>  阅读数
  page_pv_footer:
```
