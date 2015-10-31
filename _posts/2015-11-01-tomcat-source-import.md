---
layout: post
title:  "java tomcat eclipse."
category: tomcat
tags:  tomcat源码导入eclipse
---

##tomcat 源码导入eclipse
tomcat web容器，开发中经常用到，下面介绍tomcat如何导入到eclipse调试
参考tomcat官方文档：http://tomcat.apache.org/tomcat-8.0-doc/building.html
###1、准备工具
####1.1安装jdk
tomcat8 对应的jdk7，tomcat9对饮jdk8以上。
具体参考：http://tomcat.apache.org/tomcat-8.0-doc/building.html#Introduction
####1.2安装ant
ant需要1.95以上的版本
参考：http://tomcat.apache.org/tomcat-8.0-doc/building.html#Install_Apache_Ant_1.9.5_or_later
####1.3 下载源码
可以直接通过官网下载源码：http://tomcat.apache.org/download-80.cgi 最下面下载源码
或者通过版本管理工具下载：
svn地址： http://svn.apache.org/repos/asf/tomcat/tc8.0.x/trunk/

###2、ant编译导入eclipse
####2.1 ant编译
#####2.1.1 
切换到tomcat的源码目录：这里叫tomcat_home=F:\dev\apache\apache-tomcat-8.0.28-src
#####2.1.2
修改build.properties 文件中的base.path=F:\dev\apache\apache-tomcat-8.0.28-src
#####2.1.3
dos窗口切换到tomcat_home目录，执行ant ide-eclipse
如果执行过程中失败，可能是没有翻墙，导致jar包下载不下来，我这里使用旗舰vpn，可以免费使用1g流量，开启vpn
然后，在执行：ant ide-eclipse 编译成功

####2.2
#####2.2.1
在eclipse 里新建两个classpath：window-->preferences--->java--->bulid path-->classpath variable
新增两个变量：1、TOMCAT_LIBS_BASE=tomcat_home（F:\dev\apache\apache-tomcat-8.0.28-src）
2:、ANT_HOME = 指向ant的目录

#####2.2.2
在eclipse 里直接导入 已存在的java 项目找到tomcat_home 路径，导入即可。














