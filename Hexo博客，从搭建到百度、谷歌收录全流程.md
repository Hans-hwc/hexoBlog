---
title: Hexo博客，从搭建到百度、谷歌收录全流程
categories: 
- Hexo
tags:
- hexo
---
#### 前言
hexo静态博客很早就耳闻了，鉴于时间和精力，之前一直没决心要做一个自己的个人网站。在使用hexo搭建静态博客之前，还有一个小插曲，之前曾经考虑过使用wordpress搭建个人网站，阿里云服务器和域名都已经购买，并且已经在服务器上配置好了相关内容，但是域名备案需要服务器运行3个月，只能通过ip地址访问wordpress博客，这个点就很影响个人网站的使用，并且阿里云服务器一年的费用达到2000多，也是一笔不小的开销。综合权衡对比之后，转而投向谷歌github、百度coding的hexo静态个人网站，好处是免费并且有平台提供的特定域名地址，并且hexo可以满足目前这些所有的需要，个性化定制型强，搭配目前使用人数最多的next主题，简直是帅到不要。并且现在很多搜索到的个人博客，基本都是hexo+next主题的搭配，可见其受欢迎程度。言归正传，下面就把玩hexo从搭建到收录全过程分享给大家，很多坑点网上是找不到的，千篇一律的内容很难分析问题。

#### 相关资料
1.关键地址
[NexT主题官方文档](http://theme-next.iissnan.com/getting-started.html) hexo的一些部署配置可以简单参看，主要看NexT主题怎么在hexo中配置，定制个性化内容。
[leancloud网站](https://leancloud.cn) 博客集成阅读数，valine评论系统都需要用到。
[hexo个性化icon网站](https://fontawesome.com) 里面的icon名称可以使用到hexo中，替换并定制化icon，hexo的图标都是关联到这里的。
[coding网站](https://coding.net) 国内存放静态博客界面代码
[github网站](https://github.com) 国外存放静态博客界面代码
注意：个人把静态博客分别上传到coding、github，方便国内和国外的搜索引擎爬取到内容。自己可以酌情选用。
[百度收录站点](https://ziyuan.baidu.com/site/index) 提交coding域名
[谷歌收录站点](https://www.google.com/webmasters/tools/home?hl=zh-CN) 提交github域名

2.相关地址
[valine评论系统](https://valine.js.org/)用于博客集成评论系统
[Node.js](http://nodejs.cn/) hexo需要先安装node.js环境
[Git](https://git-scm.com/downloads) hexo在上传时需要用到git
5.1: git@github.com:iissnan/hexo-theme-next.git （个人使用版本）
6.0: git@github.com:theme-next/hexo-theme-next.git

#### 正文
3.准备工作
本地环境需要安装Node.js和Git，可以在上面的地址找到安装下载界面。

4.安装并初始化hexo
上面两个准备工作完成后，可以选择一个目录，右键选择Git Bash Here打开终端，依次执行如下命令：
（使用cmd的终端也行，不过需要配置git的环境变量，这里直接使用git自带的终端方便）
```
npm install -g hexo-cli
hexo init Hexo
cd Hexo
npm install
```
都执行成功后，会在目录生成一个Hexo文件夹，以后Hexo文件夹就是本地静态网站配合和文章存放的地方。接下来启动本地hexo，先本地预览hexo，执行如下命令：
```
hexo s
```
当看到命令行窗口出现，INFO Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.的内容时，说明启动成功了，然后在浏览器输入网址：http://localhost:4000/ 即可看到本地hexo网站了。

另外，补充几个hexo关键的操作命令：
```
hexo clean #清空hexo，主要删除Hexo根目录下的public文件夹
hexo g #重新成功public文件夹内容
hexo s #启动本地hexo服务
hexo d #发布到远程仓库
```
以后每次同步远程仓库，基本都是上面的命令顺序。

5.替换默认的hexo主题（landscape-->NexT）
hexo默认的主题是landscape，目前NexT主题是使用最多的，个性化定制性都很好，使用NexT主题替换landscape默认主题，我们需要先把NexT主题拷贝到Hexo本地，在终端输入：
```
git clone https://github.com/iissnan/hexo-theme-next themes/next
```
拷贝成功后，使用编辑器打开Hexo根目录下的_config.yml文件，把里面的landscape主题替换成next主题，然后hexo clean，hexo g，hexo s，接着刷新浏览器就可以看到新配置的NexT主题了。
```
# Site
title: Hexo         # 此处改为你站点的标题
subtitle:           # 此处改为你站点的副标题
description:        # 此处改为你站点的说明
keywords:           # 此处改为你站点的关键字
author: John Doe    # 此处改为你的名字
language:           # 此处改为 zh-CN
timezone:           # 此处改为 Asia/Shanghai

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://yoursite.com
root: /
permalink: :year/:month/:day/:title/   # 此处可以改为 :title/
permalink_defaults:

# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: landscape   # 此处改为 next
```

6.上传本地博客到github或者coding
把本地静态代码上传到远程仓库，如github、coding等。首先我们需要在两个平台上有账号，并且分别创建项目仓库，注意，新建的项目名称是有特定要求的，github上的名称必须是：{user_name}.github.io，coding上的名称必须是：{user_name}.coding.me，这样子上传到远程仓库的静态文件，在访问的时候才不会出现样式混乱和404问题，每个平台只提供一个这样的pages页面，而格式也是固定的，按照人家平台的规定来就行了。其中，用户名就是当时注册的时候用的是那个名称，别搞乱了，不是后面修改资料的昵称，用户名一般修改不了。

上传之前，先把ssh在本地配置一下，打开Hexo根目录下的_config.yml文件，找到deploy并如下修改：
（把其中的github和coding的ssh替换成自己的就行了，注意一下，需要先在平台上配置好publickey，玩git的应该都知道）
```
deploy:
  type: git
  repo:
    github: git@github.com:xxx/xxx.github.io.git,master
    coding: git@git.coding.net:xxx/xxx.coding.me.git,master
```
修改好了之后，执行命令，上传到远程仓库：
```
hexo g -d
```
最后，浏览器打开远程仓库地址，查看代码，然后分别把github或coding的pages打开，等待一会，然后访问pages地址就可以看到你提交的个人网站了。

7.百度、谷歌收录操作
让百度、谷歌收录个人网站，需要两个平台上的验证文件放在博客的根目录下（这里选择推荐的一种验证方式）。打开上面提到的百度收录，谷歌收录的网址，统一选择文件验证的方式，百度这边的话在添加地址的时候，第一次可能需要填写个人信息，补充完毕后，添加网站，然后根据提示下一步操作即可，谷歌的也是类似。
这里提一个坑点：百度、谷歌的验证方式都是使用文件验证，从平台上下载的验证文件在放根目录的说法中，网上大多数的说法都是说直接把文件放到Hexo根目录的source目录下，然后上传到远程仓库，但是实验证明这种做法是有问题的，当我们执行hexo g生成静态界面的时候，hexo会把多余的内容添加到source目录下的验证文件中，导致百度或者谷歌验证一直失败。
解决方法：在hexo g操作之前，验证文件先不加入到source目录中，等待hexo g执行成功后，手动把验证文件copy到Hexo根目录下的public目录中，然后执行hexo d上传到远程仓库，最后再测试平台上的验证文件，可以看到百度、谷歌都验证成功了。最后就等待收录通过后，输入site:地址，测试一下是否搜索到博客地址。谷歌的收录速度很快，上传到仓库后几个小时就可以搜索到我的网站了，而百度则慢点，可能要一两个星期，有备案填入在百度上则会加快收录速度。

#### 结语
上面就是Hexo网站从配置到谷歌、百度收录的全过程了，另外关于Hexo的个性化配置，评论系统的配置等这些还是有很多细节和坑点，可以持续关注，晚些时间会放出关于hexo主题个性化定制的相关内容。可以以本博客显示作为参考。
最后，如果在搭建hexo博客过程中，有解决不了的问题或者想让熟悉的人快速帮你配置并指导，可以添加wechat596有偿服务，添加好友时备注：昵称-hexo服务。



