---
title: SpringBoot项目的jar包在服务器上启动的正确姿势
categories: 
- SpringBoot
tags:
- springboot
---
#### 关于
一般上来说，我们在服务器上启动一个jar，最简单的方式就是java -jar xx.jar，虽然这种方式简单但有时候我们的场景需要更多，例如常驻后台运行，在命令行窗口关闭的时候不中断项目，指定端口，并且输出日志到文件中等。所以这个时候我们通常会采用脚本启动和关闭项目，方便项目的统一管理。

#### 脚本启动和关闭的案例
1.启动脚本
```
nohup java -jar ../webapp/xxx.jar --server.port=9002 >> ../logs/xxx.log  &

tail -f ../logs/xxx.log 
```

2.关闭脚本
```
pid=`ps -ef|grep java|grep xxx.jar |awk '{print $2}'`

if [ -z $pid ]; then
    echo 'app not runing'
else
    echo 'kill pid ' $pid
    kill $pid
    sleep 5
    ps -ef|grep java
fi
```
3.最后一步，执行脚本。（cd到脚本目录并执行）
```
sh xxx.sh
```

#### 补充
1.命令后加&符号，可以使命令在后台执行。
2.tail -f 实时查看日志文件。
3.如果要先关闭项目再启动，尽量不要使用Ctrl+z退出命令行窗口的当前状态，最好新开一个命令行窗口，然后执行关闭脚本，再执行启动脚本。这样操作，可以避免应用莫名其妙没有关闭到的情况，反复执行关闭脚本却没有杀死应用进程的奇怪问题，需要杀多次。

