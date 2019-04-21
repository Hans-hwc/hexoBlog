---
title: SpringBoot邮件发送css样式在手机邮件中显示失效问题
categories: 
- SpringBoot
tags:
- springboot
---

#### 关于
下面分享一个本人在开发邮件服务遇到的一个小插曲，在使用SpringBoot的邮件发送FreeMarker模板时，发现在模板上设置的style样式，在手机端邮件显示部分会失效，例如字体颜色的样式失效等。针对这种情况，这里分享一下我的一个处理方式，仅供参考，不一定是最佳的解决方式。

#### 具体步骤
1.注释掉顶部style的与颜色相关的样式，测试貌似宽度，居中这些生效。
![image.png](https://upload-images.jianshu.io/upload_images/2405826-8433367dfb73a782.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.在具体需要设置颜色的table、tr或者tb中，直接设置style样式。这样子，在手机上显示，颜色等就生效了。
![image.png](https://upload-images.jianshu.io/upload_images/2405826-ac7a7cbfd11a7c78.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 小结
由于公司工作，平时工作通知沟通，都是会通过电脑的outlook邮件。电脑端上的outlook对style样式支持比较好，无需上面的处理能正常显示，只是同样的做法在手机端显示支持就显得不友好，样式没生效。凡是遇到这种样式不生效的情况，可以尝试直接在需要设置样式的地方，如tr或tb上，直接设置样式，多测试几次。