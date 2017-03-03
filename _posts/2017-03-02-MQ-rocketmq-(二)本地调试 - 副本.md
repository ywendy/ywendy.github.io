---
layout: post
title:  "rocketmq"
category: MQ
tags:  rocketmq 本地调试 debug
---


#使用rocketmq源码在本地debug

####1. [RocketMQ github地址](https://github.com/apache/incubator-rocketmq)
+ git clone https://github.com/apache/incubator-rocketmq.git
+ cd incubator-rocketmq
+ mvn clean install -Prelease-all assembly:assembly -U -Dmaven.test.skip=true

####2.使用IDEA打开

![](https://ywendy.github.io/img/rocketmq/idea打开rocketmq源码.png)

####3.启动nameserver
+ 查看rocketmq的启动脚本mqnameser,发现里面有个rocketmq的环境变量，配置到rocketmq的源代码的地址即可${ROCKETMQ_HOME},配置过程略过，<font color="red">环境变量</font>,在Win7下设置貌似一直不管用，所以看下面我的做法
![](https://ywendy.github.io/img/rocketmq/rocketmq设置rocketmqHome.png)
+ 这样直接启动org.apache.rocketmq.namesrv.NamesrvStartup 即可.
+ 启动时要设置一些参数参考runserver.sh
+ 需要制定 -n参数： <font color="red">-n 10.69.6.54:9876</font>
+ 这样rocketmq的nameserver 就启动了，nameserver的作用可以暂时理解为zk一样的注册中心

####4.启动broker
+ 启动broker的过程和nameserver差不多，主要是配置broker的地址：-n 10.69.6.54:9876






























