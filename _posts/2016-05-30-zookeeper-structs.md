---
layout: post
title:  "zk 数据存储结构."
category: zookeeper
tags:  zookeeper ZKDataBase DataTree DataNode.
---

# Zookeeper 数据结构

## 1、zk 数据结构是树状的结构
				/
			/       \
  		 dubbo       storm
  		 /  \       /   \
     			nimbus	supervisor

## 2、zk 数据结构包含的类

	DataBase 、DataTree、DataNode、StatPersisted

![Alt text](https://ywendy.github.io/img/zookeeper数据结构.png "Optional title")

## 3、StatPersisted  持久化状态中参数介绍

  参数		|	类型	| 				含义				
------------|-----------|--------------------------------------
czxid		|	long	|节点创建时的zxid
mzxid		|	long	|节点最新一次更新发生时的zxid.
ctime		|	long	|节点创建时的时间戳	
mtime		|	long	|节点最新一次更新发生时的时间戳
version		|	int 	|节点数据的更新次数
cversion 	|	int 	|其子节点的更新次数
aversion	|	int 	|节点ACL(授权信息)的更新次数
ephemeralOwner | long 	| 如果该节点为ephemeral节点, ephemeralOwner值表示与该节点绑定的session id. 如果该节点不是ephemeral节点, ephemeralOwner值为0.
pzxid		| 	long	| -----

