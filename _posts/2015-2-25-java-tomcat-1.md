---
layout: post
title:  "编译tomcat源码与导入eclipse！"
category: java
tags: tomcat
---

所需软件
	1、jdk6（本人编译tomcat-7.0.59需要使用jdk6,官网说jdk5以上都可以不知道为什么，可能是依赖的jar包里需要的jdk版本不能高于jdk6吧）
	2、ant
	3、svn（可以不安装）
安装ant
	1、去官网下载http://ant.apache.org/bindownload.cgi 下载ant
	2、解压压缩文件
	3、在环境变量里添加变量 ANT_HOEM = E:\work\apache-ant-1.9.4(自己根据自己的环境修改)
	4、在path里添加%ANT_HOME%\bin
	5、在命令行输入ant 如果有反应就表示成功了.
![](https://ywendy.github.io/img/ant.png)	
	
	
安装jdk和svn
	自己搜索如何安装。一般都会。
下载tomcat源码
	1、如果你有svn，看这里，怎么下载自己看吧。http://tomcat.apache.org/svn.html 里面很多版本，自己折腾吧，我选择的是apache-tomcat-7.0.59
	2、如果没有安装svn软件或者插件，不要紧，直接下载源代码http://tomcat.apache.org/download-70.cgi 这里可以下载7的，自己点进去看，在页面最下
		有个Source Code Distributions ，自己看着下吧，有zip gz等
	
编译前的准备
	1、解压你下载的tomcat源码，这里叫${tomcat-source}
	2、修改解压后的文件里有个build.properties.default 的文件,改为build.properties 并且修改里面的base.path=H:/soft/apache相关/apache-tomcat-7.0.59(这里随便找个目录，可以自己定义)，这个目录是用来存放tomcat依赖包的。
	3、确认是jdk版本，jdk6（javac -version 是6就可以）
	
	
编译
	1、在命令行切换到${tomcat-source} 这个目录下，然后执行ant，稍等片刻就会编译成功.
	2、执行ant ide-eclipse 可以用来导入eclipse里面
	
导入eclipse
	1、打开eclipse，import exist project ，然后选择刚才的${tomcat-source} 这个目录就可以导入进去，导入后会有错误
		自己点开problem看看，一般都是没有ant_home 和tomcat_libs_base 变量导致的，新建这两个变量，ant选择ant的目录
		tomcat_libs_base 选择刚才的base.path的那个目录就可以了
	2、这里用jdk7也没事。
	3、找到bootstrap 这个类，然后run  会让你选择start-tomcat 或者stop-tomcat 你选择start看看是不是启动起来了。


```java



```
