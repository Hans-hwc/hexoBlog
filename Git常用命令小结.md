---
title: Git常用命令小结
categories: 
- 工具
tags:
- git
---
### 前言
平时我们经常使用到git，有些朋友喜欢使用git的窗口界面来操作，我个人也蛮喜欢的。不过git命令是学习git的根本，和机器打交道最近的方式，所以学好git对理解git的工作流是很有帮助的。下面梳理一下本人常用的git操作命令。


### 正文

#### git提交操作流程
（进入到项目目录中，然后执行如下命令）
＃初始化本地仓库
git init
＃将本地内容添加至git索引中（注意：每次提交最好都执行一下）
git add .      （git add --all）
＃将索引添加至本地仓库中（日志log，注意新增文件内容需要该命令才能提交到本地仓库，才能push到远程）
git commit -m "first commit"    注意：日志不能为空字符串等
#添加远程仓库路径
git remote add origin ssh://git@git.infinitus.com.cn:7999/han/gittestdemo.git
＃将本地内容push至远程仓库中
git push -u origin master
（push之前，确保公钥已经放上去了）

#### 子分支与主分支master合并流程
1.首先我们在子分支上开发，完成后提交代码到子分支
git add .
git commit -m ‘dev'
git push -u origin dev
2.把分支的代码合并到主分支master上
步骤一览：先切换到master上，保险起见先拉取一下远程仓库master，然后再在合master的主分支上合并dev分支，最后把合并成的master分支提交到远程仓库。
git checkout master
git pull origin master   (同是master分支，pull回来就会自动本地merge)
git merge dev
git push origin master
补充：
1.git status可以查看状态
2.远程仓库有子分支，也不可以直接拉取子分支，先拉取主分支再切换到子分支
3.git hook 在使用git窗口操作，git base命令窗口不会打印内容。
4.注意，本地commit的时候存在冲突的情况，即使git push成功，但远程并没有更新到内容。需要把冲突去掉再次重新操作流程。git add .   git commit git push···
5.pull master回来时，如果远程仓库没有t1之类的子分支，则本地git branch -a是看不到该子分支的。该命令只是看本地仓库的分支信息。

#### git常用命令
＃查看本地分支
git branch
＃查看远程分支（好像也包含本地分支）
git branch -a
＃创建本地分支，并切换到分支（test是分支名称，可替换）
git branch test
git checkout test
注：也可以一次性写法git checkout -b dev
＃提交到远程仓库
1.git push origin test:remoteTest    本地test分支提交到远程remoteTest分支（如果远程没有则新建该分支）
2.git push origin test		       本地test分支提交到远程test分支（如果远程没有则新建该分支）
（push操作，就算当前分支是test1，也可以直接把test2 push到远程，再push test1都ok）
＃从远程拉取分支
git pull origin test:test
注：如果不写本地分支名称，则默认和远程分支同名，这时命令为：$ git pull origin test

注意：
1.操作git的过程中，在子分支test1中git branch testMerge分支，发现子分支还可以拉取子子分支，test1与testMerge内容一样。

＃clone远程仓库到指定目录
git clone ssh://git@git.infinitus.com.cn:7999/han/gittestdemo.git  "E:\git_workplace\newdemo"
（注意：目录需要用""包起来）
cd E:

＃git 删除本地分支
git branch -d br
＃git 删除远程分支（删除分支与提交分支类似，区别就是在分支名前加上:）
git push origin :br  (origin 后面有空格)

git代码库回滚: 指的是将代码库某分支退回到以前的某个commit id
【本地代码库回滚】：
git reset --hard commit-id :回滚到commit-id，讲commit-id之后提交的commit都去除
git reset --hard HEAD~3：将最近3次的提交回滚



#### git配置信息相关
查看用户名和邮箱地址：
git config user.name
git config user.email
修改用户名和邮箱地址：
git config --global user.name  "xxxx"
git config --global user.email  "xxxx"

查看公钥：cat ~/.ssh/id_rsa.pub


