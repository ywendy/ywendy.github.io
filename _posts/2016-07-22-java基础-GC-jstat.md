---
layout: post
title:  "jstat"
category: java基础
tags:  java openjdk openjdk7
---

#jstat

##1、jstat -help
```java
    jstat -<option> [-t] [-h<lines>] <vmid> [<interval> [<count>]]
```

参数|说明
---|----
option|选项，通过jstat -options 查看，包含gcutil、gc、class 等
vmid|进程id，通过jps 可以查看到
interval|时间周期，支持秒和毫秒 ,默认是秒 1s 1000ms
count | 打印次数

eg:
jstat -gcutil 1198 5s 100
对1198 进程 5s钟打印一次信息，打印100次

##2、jstat -option

```java
    jstat -options
```

参数|说明
---|---
–class | 监视类装载、卸载数量、总空间及类装载所耗费的时间
–gc | 监视Java堆状况，包括Eden区、2个Survivor区、老年代、永久代等的容量
–gccapacity | 监视内容与-gc基本相同，但输出主要关注Java堆各个区域使用到的最大和最小空间
–gcutil | 监视内容与-gc基本相同，但输出主要关注已使用空间占总空间的百分比
–gccause | 与-gcutil功能一样，但是会额外输出导致上一次GC产生的原因
–gcnew | 监视新生代GC的状况
–gcnewcapacity | 监视内容与-gcnew基本相同，输出主要关注使用到的最大和最小空间
–gcold | 监视老年代GC的状况i
–gcoldcapacity | 监视内容与——gcold基本相同，输出主要关注使用到的最大和最小空间
–gcpermcapacity | 输出永久代使用到的最大和最小空间
–compiler | 输出JIT编译器编译过的方法、耗时等信息
–printcompilation | 输出已经被JIT编译的方法

##3、jstat -class <pid> :显示class信息（加载卸载时间）
    Loaded  Bytes    Unloaded  Bytes     Time   
    9591    19186.1      61    95.6      6.08

输出参数|说明
---|---
Loaded|加载类的数量
Bytes|加载类的字节数
Unloaded|卸载类的数量
Bytes|卸载类的字节数
Time|加载和卸载类的总时间

##4、jstat -compiler <pid> :显示实时编译（JIT）信息

    Compiled Failed Invalid   Time   FailedType FailedMethod
      3086     2       0      42.99       1      org/aspectj/weaver/JoinPointSignatureIterator findSignaturesFromSupertypes

输出参数|说明
---|---
Compiled|编译任务执行总次数
Failed|编译失败总数量
Invalid|编译任务失效数量
Time| 编译总耗时
FailedType|最后一次编译失败的任务类型
FailedMethod|最后一次编译失败的类、方法信息

##5、jstat -gc <pid> :显示gc信息

    S0C     S1C     S0U     S1U   EC       EU        OC         OU        PC        PU       YGC    YGCT    FGC    FGCT    GCT 
    4096.0  4608.0  3536.6  0.0   44544.0  27802.0   451584.0   259577.6  111616.0 57980.6  166    9.627   1      0.463   10.090

输出参数|说明
---|---
S0C | 年轻代Servisor（幸存区）中s0的当前容量
S1C  |年轻代Servisor（幸存区）中s1的当前容量
S0U  |年轻代Servisor（幸存区）中s0的当前已使用空间（字节数）
S1U  |年轻代Servisor（幸存区）中s1的当前已使用空间（字节数）
EC   |年轻代中Eden（伊甸园）的容量 (字节)
EU   |年轻代中Eden（伊甸园）目前已使用空间 (字节)
OC   |老年代 Old 的容量 (字节)
OU |老年代 Old 的使用量(字节)
PC|持久代Perm的容量
PU|Perm(持久代)目前已使用空间 (字节)
YGC|从应用程序启动到采样时年轻代中gc次数
YGCT|从应用程序启动到采样时年轻代中gc所用时间(s)
FGC|从应用程序启动到采样时old代(全gc)gc次数
FGCT|从应用程序启动到采样时old代(全gc)gc所用时间(s)
GCT|从应用程序启动到采样时gc用的总时间(s)


























