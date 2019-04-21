---
title: Hexo增加APlayer音乐播放功能
categories: 
- Hexo
tags:
- hexo
---

#### 关于
在个人的站点上，如果有音乐播放的功能，那么读者可以一遍阅读文章，一边欣赏音乐，是一件很愉快的事情。下面就以本站点为案例，分享增加音乐播放功能的步骤。

#### 具体操作
1.先上效果图
![](https://upload-images.jianshu.io/upload_images/2405826-36c16d3adfd8a12b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.准备
[APlayer](https://github.com/MoePlayer/APlayer)，下载github压缩包，解压后把dist文件夹复制到\themes\next\source目录中。
![](https://upload-images.jianshu.io/upload_images/2405826-c3377343703fcaee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在dist目录里，新建music.js文件，并把如下代码粘贴进去。
```
const ap = new APlayer({
    container: document.getElementById('aplayer'),
    fixed: true,
    autoplay: false,
    audio: [
      {
        name: "你一定要幸福",
        artist: '简弘亦',
        url: 'http://www.ytmp3.cn/down/51689.mp3',
        cover: 'http://img.ytmp3.cn/image/52.jpg',
      },
      {
        name: '一百万个可能(Live)',
        artist: '摩登兄弟',
        url: 'http://www.ytmp3.cn/down/52772.mp3',
        cover: 'http://img.ytmp3.cn/image/53.jpg',
      },
      {
        name: 'The Rose',
        artist: 'Westlife',
        url: 'http://www.ytmp3.cn/down/56694.mp3',
        cover: 'http://img.ytmp3.cn/image/51.jpg',
      },
	  {
        name: 'In The Eyes',
        artist: '江映东',
        url: 'http://www.ytmp3.cn/down/53053.mp3',
        cover: 'http://img.ytmp3.cn/image/10.jpg',
      }
    ]
});
```
![](https://upload-images.jianshu.io/upload_images/2405826-044bcba879a918bb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.在\themes\next\layout\_layout.swig文件中，<body>里新增如下代码：
```
<!-- 音频播放 -->
<link rel="stylesheet" href="/dist/APlayer.min.css">
<div id="aplayer"></div>
<script type="text/javascript" src="/dist/APlayer.min.js"></script>
<script type="text/javascript" src="/dist/music.js"></script>
```
重新发布就可以看到效果了。

4.补充
[Aplayer 中文文档](https://aplayer.js.org/#/zh-Hans/)
[mp3音乐外链网站](http://up.mcyt.net/ )
