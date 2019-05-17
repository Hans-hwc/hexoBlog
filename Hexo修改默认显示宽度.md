---
title: Hexo修改默认显示宽度
categories: 
- Hexo
tags:
- hexo
---
#### 背景
在我们安装完next主题后，默认的界面宽度比较窄。这时可以选择手动修改样式，增加默认显示宽度。

#### 步骤
1.首先在next主题的_config文件上查看Schemes对应的是哪个主题。
![](https://upload-images.jianshu.io/upload_images/2405826-f681c343019eca84.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.打开themes\next\source\css\_schemes\Gemini\index.styl文件，在最底部增加如下代码。
```
header{ width: 90% !important; }
header.post-header {
  width: auto !important;
}
.container .main-inner { width: 90%; }
.content-wrap { width: calc(100% - 260px); }

.header {
  +tablet() {
    width: auto !important;
  }
  +mobile() {
    width: auto !important;
  }
}

.container .main-inner {
  +tablet() {
    width: auto !important;
  }
  +mobile() {
    width: auto !important;
  }
}

.content-wrap {
  +tablet() {
    width: 100% !important;
  }
  +mobile() {
    width: 100% !important;
  }
}
```
3.上面两步完成后，hexo clean，hexo g，hexo d。刷新界面即可。