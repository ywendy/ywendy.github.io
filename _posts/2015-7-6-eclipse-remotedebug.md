---
layout: post
title:  "eclipse 远程debug."
category: eclipse
tags:  tomcat eclipse 远程debug.
---

##eclipse tomcat 远程调试配置.
####1、tomcat的配置文件 ：catalina.sh 
在catalina.sh 中添加 CATALINA_OPTS="-Xdebug  -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n"
或者下面这个
-server -Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=8788

![](https://ywendy.github.io/img/linux_tomcat_remote_debug.png)	


####2、eclipse 配置

点击：Run----->Debug Configurations----> 左侧选中remote application 新建一个连接.填上主机名和端口号，选中项目，然后运行就可以了。

打断点看看效果

![](https://ywendy.github.io/img/eclipse_remote_debug.png)	












