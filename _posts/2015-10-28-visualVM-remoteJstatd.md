---
layout: post
title:  "visualVM 远程监控."
category: eclipse
tags:  visualVM tomcat 远程监控.
---

##visualVM tomcat 远程监控.
###1、在jdk的bin目录下新建文件>>>>$JAVA_HOME/bin/jstatd.all.policy 内容如下:
```javascript
      grant codebase "file:${java.home}/../lib/tools.jar" {
               permission java.security.AllPermission;
          };
```

###2、启动jstatd
####2.1
```javascript
jstatd -J-Djava.security.policy=jstatd.all.policy -J-Djava.rmi.server.hostname=192.168.0.109 &
(192.168.0.109  为你服务器的ip地址,&表示用守护线程的方式运行，默认端口号为1099)
```

####2.2
```javascript
此命令是一个RMI Server应用程序，提供了对JVM的创建和结束监视，也为远程监视工具提供了一个可以attach的接口

options 
-nr 当一个存在的RMI Registry没有找到时，不尝试创建一个内部的RMI Registry
-p port 端口号，默认为1099
-n rminame 默认为JStatRemoteHost；如果多个jstatd服务开始在同一台主机上，rminame唯一确定一个jstatd服务
-J jvm选项


```


###3、visual Vm

####3.1 连接
```javascript
在visual vm 中新建远程主机，填上主机名，新建jstatd连接，默认即可.
```

![](https://ywendy.github.io/img/visualvm_remote_jstatd.png)	

####3.2插件安装

```javascript
在visual vm 中点击工具，选择插件，然后就可以安装了。 visual GC 一般需要安装.安装过程很快.
```












