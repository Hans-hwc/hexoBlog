---
title: Hexo+DaoVoice实现网页在线通讯功能
categories: 
- Hexo
tags:
- hexo
---
#### 关于
有天，你发了一篇很好的文章。你的读者看了，觉得写得很好，想要联系到你。评论留言？反馈太慢！找到你的关于简介，发邮件联系你？路径太长！现在DaoVoice就可以解决这个痛点，及时在线通讯，直接联系到作者。有问题或者咨询，可以第一时间得到反馈。并且DaoVoice现在打通了微信端，在网页上发送的消息，会直接推送到作者的微信上，另有小程序支持消息回复等，非常方便。


#### 具体操作
1.注册DaoVoice
首先在[DaoVoice](http://dashboard.daovoice.io/)官网上注册一个账号。
![](https://upload-images.jianshu.io/upload_images/2405826-d61b060e4b9e4b1e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
注意：这里邮箱的填写要留心，我第一次填写的是QQ邮箱，不知道怎么回事，在登录的时候一直提示说邮箱验证失败，然后登录进去后，界面很奇怪简单，一直找不到应用设置，也就是没有appid。后来我换了新浪邮箱，就可以了，登录成功后，后面界面上出现了应用设置。

2.获取appid
注册成功后，第一次登录，会弹出一个窗口，填完相关信息后。点击应用设置，点击安装到网站，然后就可以找到我们需要的appid了。
![](https://upload-images.jianshu.io/upload_images/2405826-2018869fbe46c723.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.配置hexo
在next主题的配置文件中（\themes\next\_config.yml），新增如下内容：
```
# Online contact
daovoice: true
daovoice_app_id: 这里替换成你DaoVoice上的appid
```
在\themes\next\layout\_partials\head.swig文件的最后，新增如下内容：
```
{% if theme.daovoice %}
  <script>
  (function(i,s,o,g,r,a,m){i["DaoVoiceObject"]=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;a.charset="utf-8";m.parentNode.insertBefore(a,m)})(window,document,"script",('https:' == document.location.protocol ? 'https:' : 'http:') + "//widget.daovoice.io/widget/0f81ff2f.js","daovoice")
  daovoice('init', {
      app_id: "{{theme.daovoice_app_id}}"
    });
  daovoice('update');
  </script>
{% endif %}
```

4.如下就是最终配置完成的效果。
![](https://upload-images.jianshu.io/upload_images/2405826-017f9c46046d7e81.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)