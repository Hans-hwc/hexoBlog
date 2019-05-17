---
title: Vue入门及上手教程
categories: 
- Vue
tags:
- vue
---
#### 故事背景
我所在的部门的职能是提高其他业务部门在产品交付上的更好、更快。以前，公司内部与三方公司签订了协议，购买了别人家一套开发软件，帮助我们更好地落地这个流水线的概念。后来，由于软件升级及需求限制，产品战略转型，转成自建流水线，再后来就有了这次Vue前端界面技术选型经历。

由于内部团队，包括三方支持公司的驻场人员对Vue都不是很熟悉，后来经过考虑，还是由我来主导和负责Vue前端界面的开发工作。其实，对于前端，我是有一定的基础的，但由于Vue这个框架以前我也没怎么接触过，那么后来我是如何在两个星期入门并上手Vue开发，这期间我的一些做法希望可以给你带来一点启发。

#### 故事经历

当时，我们的目标和开发任务还是挺重的，我们给业务部门承诺的是两个星期把流水线的流程基本呈现出来，并基础可用。

刚开始，我的考虑是这样的。由于Vue我不熟悉，那么可以理解为零基础。对于零基础的我，怎么能更快的打通Vue的天地线呢？

我的做法就是开始两天死磕[Vue语法](https://www.runoob.com/vue2/vue-tutorial.html)和[官网案例](https://cn.vuejs.org/v2/guide/)，我的目的也是很明确的，为了尽可能少的避免认知盲区，基础的语法和概念性的东西，我是一定要知道的。

好了，经过两天的语法和案例的学习，期间我也做了不少笔录，作为记忆索引。

接下来，我需要找一个比较完备的Vue实战案例，经过在github上的一番搜索和选择，最后我决定使用[vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/blob/master/README.zh-CN.md), vue-element-admin是一个比较完备的案例了，上面有很多基础的功能，可以减少不少的重复造轮子的时间。

那么，这个demo怎么使用呢？

记住以下几个步骤就可以启动起来了。

步骤：
1.安装node.js环境
2.安装Visual Studio开发工具，顺带也可以安装一下vue语法插件，帮助编写和提示代码。
3.依次执行如下命令，大概就是拉取demo，初始化基础依赖，最后的npm run dev执行完毕后会自动打开本地网页。
```
# 克隆项目
git clone https://github.com/PanJiaChen/vue-element-admin.git

# 进入项目目录
cd vue-element-admin

# 安装依赖
npm install

# 建议不要用 cnpm 安装 会有各种诡异的bug 可以通过如下操作解决 npm 下载速度慢的问题
npm install --registry=https://registry.npm.taobao.org

# 启动服务
npm run dev
```
4.现在可以在src目录下随便找一个.vue文件来修改，界面会实时更新。

经过上面一番操作后，现在基本可以修改界面了。

那么，再接下来就是熟悉demo的项目结构（例如项目的加载入口，加载结构等），基础的配置文件（例如开发环境，测试环境，打包配置等）。

下面，我框红一些关键性的点，这是项目开发到上线必经之路。

项目截图一览，框红部分需要特别注意。
![](https://upload-images.jianshu.io/upload_images/2405826-557b7698b063a7b1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

经过一段时间的努力，项目可以打包发布到线上了。

那么，重点需要关注的就是config目录。
dev.env.js修改开发环境请求的baseUrl
![](https://upload-images.jianshu.io/upload_images/2405826-a68225176e7c879b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
prod.env.js修改生产环境请求的baseUrl
![](https://upload-images.jianshu.io/upload_images/2405826-ddbf5929912f538a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
index.js文件，修改打包的配置。
![](https://upload-images.jianshu.io/upload_images/2405826-18b592f339ae5169.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

上面都配置好了之后，执行打包命令。
```
npm run build
```
打包结束后，把打包好的dist文件夹上传到服务器指定的目录中。
![](https://upload-images.jianshu.io/upload_images/2405826-69cea5da75e567ee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

最后，通过浏览器访问一下就可以看到Vue开发的前端界面了。

#### 汇总相关资料
上面故事的经历，只是大概介绍了主要流程，其实期间还发生了很多细小的故事。例如，跨域的解决、开发过程中问题点等。下面把过去解决和参考过的资料汇总一下，当然也包括上面提到的资源地址。

**基础语法**
[Vue语法](https://www.runoob.com/vue2/vue-tutorial.html)
[官网案例](https://cn.vuejs.org/v2/guide/)

**demo案例及开发**
[vue-element-admin](https://github.com/PanJiaChen/vue-element-admin/blob/master/README.zh-CN.md), 
[Vue知识点总结](https://github.com/sunseekers/Vue)
[Vue使用的element元素组件官网](https://element.faas.ele.me/#/zh-CN/component/button)

[基于Vue2.0+Vue-router构建一个简单的单页应用](https://www.cnblogs.com/fozero/p/6185492.html)
[如何搭建一个vue项目(完整步骤)](http://www.cnblogs.com/haitaoli/p/10304193.html)
[所谓的跨域（Cross-Origin），究竟是什么？——你所不知道浏览器跨域的小知识](https://blog.csdn.net/u011037503/article/details/78025072)
[跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)

**往期文章推荐**
[Vue安装浏览器开发工具](https://huangweicai.github.io/2019/05/12/Vue%E5%AE%89%E8%A3%85%E6%B5%8F%E8%A7%88%E5%99%A8%E5%BC%80%E5%8F%91%E5%B7%A5%E5%85%B7/)
