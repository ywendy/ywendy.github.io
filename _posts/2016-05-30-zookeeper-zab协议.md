---
layout: post
title:  "zk Leader选举算法."
category: zookeeper
tags:  zookeeper FastLeaderElection
---

# 1、zookeeper 特性

- **顺序一致性**
        任何一个客户端的更新都按照他们发送的顺序执行
- **原子性**
        更新不成功就失败，更新失败没有客户端会知道
- **单系统映像**
        无论客户端连接的是哪台服务器，他与系统看见的视图一样。这就意味着，如果一个客户端在相同的会话时连接了一台新的服务器，他将不会再看见比在之前服务器上看见的更老的系统状态，当服务器系统出故障，同时客户端尝试连接ensemble中的其他机器时，故障服务器的后面那台机器将不会接受连接，直到它连接到故障服务器。
- **容错性**
        一旦更新成功后，那么在客户端再次更新他之前，他就固定了，将不再被修改，这就会保证产生下面两种结果：
        + 如果客户端成功的获得了正确的返回代码，那么说明更新已经成功。
        + 如果不能够获得返回代码（由于通信错误、超时等原因），那么客户端将不知道更新是否生效。当故障恢复的时候，任何客户端能够看到的执行成功的更新操作将不会回滚。
- **实时性**
        在任何客户端的系统视图上的的时间间隔是有限的，因此他在超过几十秒的时间内部会过期。这就意味着，服务器不会让客户端看一些过时的数据，而是关闭，强制客户端转到一个更新的服务器上。

# 2、zk ZAB 协议（zookeeper Atomic Broadcast）

## 2.1 zab 协议分两阶段：

- Leader 选举阶段
- 原子广播

## 2.2 Leader 选举算法
###2.2.1 算法列表
配置参数: **electionAlg(默认值为3 )**

算法                             |    配置      |  默认值
---------------------------------|--------------|----------------------
~~LeaderElection~~                   |      0       |new LeaderElection(this)
~~AuthFastLeaderElection~~           |      1       |new AuthFastLeaderElection(this)
~~AuthFastLeaderElection~~           |      2       |new AuthFastLeaderElection(this, true)
FastLeaderElection               |      3       | new FastLeaderElection(this, qcm)

### 2.2.2 算法创建代码

```java

    @SuppressWarnings("deprecation")
    protected Election createElectionAlgorithm(int electionAlgorithm){
        Election le=null;

        //TODO: use a factory rather than a switch
        switch (electionAlgorithm) {
        case 0:
            le = new LeaderElection(this);
            break;
        case 1:
            le = new AuthFastLeaderElection(this);
            break;
        case 2:
            le = new AuthFastLeaderElection(this, true);
            break;
        case 3:
            qcm = new QuorumCnxManager(this);
            QuorumCnxManager.Listener listener = qcm.listener;
            if(listener != null){
                listener.start();
                FastLeaderElection fle = new FastLeaderElection(this, qcm);
                fle.start();
                le = fle;
            } else {
                LOG.error("Null listener when initializing cnx manager");
            }
            break;
        default:
            assert false;
        }
        return le;
    }




```


### 2.2.3 FastLeaderElection选举关键算法

        /*
         * We return true if one of the following three cases hold:
         * 1- New epoch is higher  epoch(Logicalclock)值高的获胜--->  AtomicLong logicalclock = new AtomicLong(); 
         * 2- New epoch is the same as current epoch, but new zxid is higher  zxid 事物id（epoch相同比较zxid）
         * 3- New epoch is the same as current epoch, new zxid is the same
         *  as current zxid, but server id is higher.
         * epoch 相同，zxid 也相同，比较serverId（myid）
         */

**比较规则:**   epoch----->zxid ------>myid
