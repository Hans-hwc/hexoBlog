---
title: Android Studio发布项目到Jcenter仓库步骤
categories: 
- Android Studio
tags:
- jcenter
- android studio
---

#### 前言
Android Studio中把项目的lib库提交到Jcenter仓库中，需要使用到Bintray，Bintray是jCenter的提供商，他支持上传lib到多个平台，jCenter只是众多平台中的一个，形象的说jCenter是位于某地的仓库，Bintray是送货的卡车，你写的库就是货了。

#### 注册准备
1.在Bintray上注册账号，并创建package。
[注册bintray](https://bintray.com/)，注意：注册时尽量使用国外的邮箱，避免接收不到验证码。例如我使用雅虎邮箱。

2.完成注册之后，登录网站，然后点击maven。
![image.png](https://upload-images.jianshu.io/upload_images/2405826-2293489b837bca35.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.点击Add New Package，为我们的library创建一个新的package。
![image.png](https://upload-images.jianshu.io/upload_images/2405826-775b9521d6514838.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.假设你已经注册账你并按照上面步骤操作，或者使用我提供的账号，登陆成功后会出现如下界面，点击maven进入该仓库，并点击Add New Package创建新的包。
![image.png](https://upload-images.jianshu.io/upload_images/2405826-fb9664ce7e75a5b2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/2405826-8238da0433b597f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.填写package相关信息，如下：
![image.png](https://upload-images.jianshu.io/upload_images/2405826-fdf03c12a0c49e4f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### Android Studio配置部分
6.操作AS项目，配置相关信息，命令行操作lib包上传。
Android Studio安装上传Bintray插件和填写相关信息：（下面选用我测试通过并且操作路径最短的方式）
在项目的根build文件中补充如下标红内容
![image.png](https://upload-images.jianshu.io/upload_images/2405826-087c0349e09877c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这是根build源文件：
```
// Top-level build file where you can add configuration options common to all sub-projects/modules.
buildscript {
  
repositories {
google()
jcenter()
}
dependencies {
classpath 'com.android.tools.build:gradle:3.1.3'
 classpath 'com.novoda:bintray-release:+' // 新增
// NOTE: Do not place your application dependencies here; they belong
// in the individual module build.gradle files
 }
}
allprojects {
repositories {
google()
jcenter()
}
 tasks.withType(Javadoc) { // 新增
 options.addStringOption('Xdoclint:none', '-quiet')
 options.addStringOption('encoding', 'UTF-8')
}
}
task clean(type: Delete) {
delete rootProject.buildDir
}
```
7.然后在lib的build文件中补充如下内容：
![image.png](https://upload-images.jianshu.io/upload_images/2405826-33a4377f7296d511.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这是lib的源build文件：
```
`apply plugin: ``'com.android.library'`

`apply plugin: ``'com.novoda.bintray-release'` `// 新增`

`android {`

`compileSdkVersion ``28`

`defaultConfig {`

`minSdkVersion ``15`

`targetSdkVersion ``28`

`versionCode ``2`

`versionName ``"1.0.2"`

`testInstrumentationRunner ``"android.support.test.runner.AndroidJUnitRunner"`

`}`

`buildTypes {`

`release {`

`minifyEnabled ``false`

`proguardFiles getDefaultProguardFile(``'proguard-android.txt'``), ``'proguard-rules.pro'`

`}`

`}`

`lintOptions { ``// 新增`

`abortOnError ``false`

`}`

`}`

`dependencies {`

`implementation fileTree(dir: ``'libs'``, include: [``'*.jar'``])`

`implementation ``'com.android.support:appcompat-v7:28.0.0-rc02'`

`testImplementation ``'junit:junit:4.12'`

`androidTestImplementation ``'com.android.support.test:runner:1.0.2'`

`androidTestImplementation ``'com.android.support.test.espresso:espresso-core:3.0.2'`

`}`

`publish { ``// 新增`

`userOrg = ``'huangweicai'` `// 注册bintray时的username`

`groupId = ``'com.infinitus_demo_lib'` `// 项目包名`

`artifactId = ``'infinitus_demo_lib'` `// 项目名`

`publishVersion = ``'1.0.2'` `// 发布版本号`

`desc = ``'Summarize the tools or methods commonly used in routine development'` `// 项目描述，可选项`

`website = ``'[https://github.com/huangweicai/infinitus_demo_lib'](https://github.com/huangweicai/infinitus_demo_lib')` `// 项目站点，可选项`

`}`

```
8.在Android Studio的命令行窗口依次输入如下命令：
```
gradlew generatePomFileForReleasePublication
gradlew publishReleasePublicationToMavenLocal
gradlew bintrayUpload -PbintrayUser=xxx -PbintrayKey=xxx -PdryRun=false
```

其中，PbintrayUser是Bintray的用户名，PbintrayKey是Bintray的API Key。（API Key在注册成功后，可以在修改信息的界面找到，最好在第一次注册成功后就记录好）
![image.png](https://upload-images.jianshu.io/upload_images/2405826-e3ec2aff2fbe541f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
等待执行，看到BUILD SUCCESSFUL说明上传Bintray成功。

9.进入Bintray，可以找到我们上传的包，在页面的左下角看到maven地址说明上传内容正确，第一次在页面的右下角会看到add to jcenter，需要我们手动点击一下这个add to jcenter按钮，然后等待lib包审核通过后，我们就可以引用jcenter上的包了。
![image.png](https://upload-images.jianshu.io/upload_images/2405826-d1dfff8ee4387cd2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
以上就是Android Studio打包上传到Jcenter的完整流程。

#### 最后测试
AS引入implementation 'com.infinitus_demo_lib:infinitus_demo_lib:1.0.2'，代码中调用演示工具类TestUtil.test(context);查看吐司是否提示，提示成功说明已经成功发布并引入jcenter包。