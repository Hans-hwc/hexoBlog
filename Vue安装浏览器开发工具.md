---
title: Vue安装浏览器开发工具
categories: 
- Vue
tags:
- vue
---
#### 背景
开发vue时，浏览器有一个好的开发调试工具能让开发事半功倍，磨刀不误砍柴工。

#### 步骤
1.下载工具
地址：https://github.com/vuejs/vue-devtools

2.安装依赖
cmd进入vue-devtools文件夹，安装相关依赖，依次执行npm install,再执行npm run build。

3.修改配置
打开shells>chrome>src>manifest.json，修改"persistent":false为true。
![](https://upload-images.jianshu.io/upload_images/2405826-16cbbf13800d12cc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.浏览器安装
经过前面几步，工具基本已经准备好了。接下来，打开浏览器。
· 打开里面的设置>点击拓展程序>点击开发者模式
· 再点击加载已解压的扩展程序，然后把shells>chrome这个文件夹加入即可。
![](https://upload-images.jianshu.io/upload_images/2405826-3411d635145152eb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.测试
打开一个用vue开发的网页，打开chrome调试工具查看效果。

