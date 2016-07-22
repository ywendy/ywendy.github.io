---
layout: post
title:  "jstat"
category: java基础-GC
tags:  java GC jstat
---

#jstat

##1、jstat -help
```java
    jstat -<option> [-t] [-h<lines>] <vmid> [<interval> [<count>]]
```

参数|说明
---|----
<font color="#FF00FF">option  </font>|选项，通过jstat -options 查看，包含gcutil、gc、class 等
<font color="#FF00FF">vmid    </font>|进程id，通过jps 可以查看到
<font color="#FF00FF">interval</font>|时间周期，支持秒和毫秒 ,默认是秒 1s 1000ms
<font color="#FF00FF">count   </font>| 打印次数

eg:
jstat -gcutil 1198 5s 100
对1198 进程 5s钟打印一次信息，打印100次

##2、jstat -option

```java
    jstat -options
```

参数|说明
---|---
<font color="#FF00FF">–class              </font>| 监视类装载、卸载数量、总空间及类装载所耗费的时间
<font color="#FF00FF">–gc                 </font>| <font color="#FF00FF">监视Java堆状况，包括Eden区、2个Survivor区、老年代、永久代等的容量
<font color="#FF00FF">–gccapacity         </font>| 监视内容与-gc基本    相同，但输出主要关注</font><font color="#FF00FF">Java堆各个区域使用到的最大和最小空间
<font color="#FF00FF">–gcutil             </font>| <font color="#FF00FF">监视内容与-gc基本相同，但输出主要关注已使用空间占总空间的百分比
<font color="#FF00FF">–gccause            </font>|   与-gcutil功能一样，但是会额外输出导致上一次GC产生的原因
<font color="#FF00FF">–gcnew              </font>| 监视新生代GC的状况
<font color="#FF00FF">–gcnewcapacity      </font>| <font color="#FF00FF">监视内容与-gcnew基本相同，输出主要关注使用到的最大和最小空间
<font color="#FF00FF">–gcold              </font>| 监视老年代GC的状况i
<font color="#FF00FF">–gcoldcapacity      </font>| <font color="#FF00FF">监视内容与——gcold基本相同，输出主要关注使用到的最大和最小空间
<font color="#FF00FF">–gcpermcapacity     </font>| 输出永久代使用到的最大和最小空间
<font color="#FF00FF">–compiler           </font>| 输出JIT编译器编译过的方法、耗时等信息
<font color="#FF00FF">–printcompilation   </font>| 输出已经被JIT编译的方法

##3、jstat -class <pid> :显示class信息（加载卸载时间）
    Loaded  Bytes    Unloaded  Bytes     Time   
    9591    19186.1      61    95.6      6.08

输出参数|说明
---|---
<font color="#FF00FF">Loaded  </font>|加载类的数量
<font color="#FF00FF">Bytes   </font>|加载类的字节数
<font color="#FF00FF">Unloaded</font>|卸载类的数量
<font color="#FF00FF">Bytes   </font>|卸载类的字节数
<font color="#FF00FF">Time    </font>|加载和卸载类的总时间

##4、jstat -compiler <pid> :显示实时编译（JIT）信息

    Compiled Failed Invalid   Time   FailedType FailedMethod
      3086     2       0      42.99       1      org/aspectj/weaver/JoinPointSignatureIterator findSignaturesFromSupertypes

输出参数|说明
---|---
<font color="#FF00FF">Compiled    </font>|编译任务执行总次数
<font color="#FF00FF">Failed      </font>|编译失败总数量
<font color="#FF00FF">Invalid     </font>|编译任务失效数量
<font color="#FF00FF">Time        </font>| 编译总耗时
<font color="#FF00FF">FailedType  </font>|最后一次编译失败的任务类型
<font color="#FF00FF">FailedMethod</font>|最后一次编译失败的类、方法信息

##5、jstat -gc <pid> :显示gc信息

    S0C     S1C     S0U     S1U   EC       EU        OC         OU        PC        PU       YGC    YGCT    FGC    FGCT    GCT 
    4096.0  4608.0  3536.6  0.0   44544.0  27802.0   451584.0   259577.6  111616.0 57980.6  166    9.627   1      0.463   10.090

输出参数|说明
---|---
<font color="#FF00FF">S0C </font> | 年轻代Servisor（幸存区）中s0的当前容量
<font color="#FF00FF">S1C </font> |年轻代Servisor（幸存区）中s1的当前容量
<font color="#FF00FF">S0U </font> |年轻代Servisor（幸存区）中s0的当前已使用空间（字节数）
<font color="#FF00FF">S1U </font> |年轻代Servisor（幸存区）中s1的当前已使用空间（字节数）
<font color="#FF00FF">EC  </font> |年轻代中Eden（伊甸园）的容量 (字节)
<font color="#FF00FF">EU  </font> |年轻代中Eden（伊甸园）目前已使用空间 (字节)
<font color="#FF00FF">OC  </font> |老年代 Old 的容量 (字节)
<font color="#FF00FF">OU  </font> |老年代 Old 的使用量(字节)
<font color="#FF00FF">PC  </font> |持久代Perm的容量
<font color="#FF00FF">PU  </font> |Perm(持久代)目前已使用空间 (字节)
<font color="#FF00FF">YGC </font> |从应用程序启动到采样时年轻代中gc次数
<font color="#FF00FF">YGCT</font> |从应用程序启动到采样时年轻代中gc所用时间(s)
<font color="#FF00FF">FGC </font> |从应用程序启动到采样时old代(全gc)gc次数
<font color="#FF00FF">FGCT</font> |从应用程序启动到采样时old代(全gc)gc所用时间(s)
<font color="#FF00FF">GCT </font> |从应用程序启动到采样时gc用的总时间(s)

##6、jstat -gccapacity <pid> : 

     NGCMN    NGCMX     NGC     S0C   S1C       EC      OGCMN      OGCMX       OGC         OC      PGCMN    PGCMX     PGC       PC     YGC    FGC 
    172032.0 2752000.0  53248.0 4608.0 3584.0  44032.0   343552.0  5503488.0   451584.0   451584.0  21504.0 169984.0 111616.0 111616.0    167 

输出参数|说明
---|---
<font color="#FF00FF">NGCMN</font> | 年轻代(young)中初始化(最小)的大小(字节)
<font color="#FF00FF">NGCMX</font> | 年轻代(young)的最大容量 (字节)
<font color="#FF00FF">NGC  </font> | 年轻代(young)中当前的容量 (字节)
<font color="#FF00FF">S0C  </font> | 年轻代中第一个survivor（幸存区）的容量 (字节)
<font color="#FF00FF">S1C  </font> | 年轻代中第二个survivor（幸存区）的容量 (字节)
<font color="#FF00FF">EC   </font> | 年轻代中Eden（伊甸园）的容量 (字节)
<font color="#FF00FF">OGCMN</font> | old代中初始化(最小)的大小 (字节)
<font color="#FF00FF">OGCMX</font> | old代的最大容量(字节)
<font color="#FF00FF">OGC  </font> | old代当前新生成的容量 (字节)
<font color="#FF00FF">OC   </font> | Old代的容量 (字节)
<font color="#FF00FF">PGCMN</font> | perm代中初始化(最小)的大小 (字节)
<font color="#FF00FF">PGCMX</font> | perm代的最大容量 (字节)
<font color="#FF00FF">PGC  </font> | perm代当前新生成的容量 (字节)
<font color="#FF00FF">PC   </font> | Perm(持久代)的容量 (字节)
<font color="#FF00FF">YGC  </font> | 从应用程序启动到采样时年轻代中gc次数
<font color="#FF00FF">FGC  </font> | 从应用程序启动到采样时old代(全gc)gc次数

##7、jstat -gcutil <pid>:统计gc信息

      S0     S1     E      O      P     YGC     YGCT    FGC    FGCT     GCT   
    95.55   0.00  21.88  57.49  51.95    168    9.642     1    0.463   10.105

输出参数|说明
---|---
<font color="#FF00FF">S0   </font> |  年轻代中第一个survivor（幸存区）已使用的占当前容量百分比
<font color="#FF00FF">S1   </font> |  年轻代中第二个survivor（幸存区）已使用的占当前容量百分比
<font color="#FF00FF">E    </font> |  年轻代中Eden（伊甸园）已使用的占当前容量百分比
<font color="#FF00FF">O    </font> |  old代已使用的占当前容量百分比
<font color="#FF00FF">P    </font> |  perm代已使用的占当前容量百分比
<font color="#FF00FF">YGC  </font> |  从应用程序启动到采样时年轻代中gc次数
<font color="#FF00FF">YGCT </font> |  从应用程序启动到采样时年轻代中gc所用时间(s)
<font color="#FF00FF">FGC  </font> |  从应用程序启动到采样时old代(全gc)gc次数
<font color="#FF00FF">FGCT </font> |  从应用程序启动到采样时old代(全gc)gc所用时间(s)
<font color="#FF00FF">GCT  </font> |  从应用程序启动到采样时gc用的总时间(s)


##8、jstat -gcnew <pid>:年轻代对象的信息

     S0C    S1C    S0U    S1U   TT MTT  DSS      EC       EU     YGC     YGCT  
    3584.0 4096.0 3424.6    0.0 15  15 4096.0  43520.0  16421.0    168    9.642

输出参数| 说明
---|---
<font color="#FF00FF">S0C </font> | 年轻代中第一个survivor（幸存区）的容量 (字节)
<font color="#FF00FF">S1C </font> |   年轻代中第二个survivor（幸存区）的容量 (字节)
<font color="#FF00FF">S0U </font> |   年轻代中第一个survivor（幸存区）目前已使用空间 (字节)
<font color="#FF00FF">S1U </font> |   年轻代中第二个survivor（幸存区）目前已使用空间 (字节)
<font color="#FF00FF">TT  </font> |   持有次数限制
<font color="#FF00FF">MTT </font> |   最大持有次数限制
<font color="#FF00FF">EC  </font> |   年轻代中Eden（伊甸园）的容量 (字节)
<font color="#FF00FF">EU  </font> |   年轻代中Eden（伊甸园）目前已使用空间 (字节)
<font color="#FF00FF">YGC </font> |   从应用程序启动到采样时年轻代中gc次数
<font color="#FF00FF">YGCT</font> |   从应用程序启动到采样时年轻代中gc所用时间(s)

##9、jstat -gcnewcapacity<pid>: 年轻代对象的信息及其占用量


      NGCMN      NGCMX       NGC      S0CMX     S0C     S1CMX     S1C       ECMX        EC      YGC   FGC 
      172032.0  2752000.0    52224.0 916992.0   3584.0 916992.0   4096.0  2750976.0    43520.0   168     1

输出参数|说明
---|---
<font color="#FF00FF">NGCMN  </font> | 年轻代(young)中初始化(最小)的大小(字节)
<font color="#FF00FF">NGCMX  </font> | 年轻代(young)的最大容量 (字节)
<font color="#FF00FF">NGC    </font> | 年轻代(young)中当前的容量 (字节)
<font color="#FF00FF">S0CMX  </font> | 年轻代中第一个survivor（幸存区）的最大容量 (字节)
<font color="#FF00FF">S0C    </font> | 年轻代中第一个survivor（幸存区）的容量 (字节)
<font color="#FF00FF">S1CMX  </font> | 年轻代中第二个survivor（幸存区）的最大容量 (字节)
<font color="#FF00FF">S1C    </font> | 年轻代中第二个survivor（幸存区）的容量 (字节)
<font color="#FF00FF">ECMX   </font> | 年轻代中Eden（伊甸园）的最大容量 (字节)
<font color="#FF00FF">EC     </font> | 年轻代中Eden（伊甸园）的容量 (字节)
<font color="#FF00FF">YGC    </font> | 从应用程序启动到采样时年轻代中gc次数
<font color="#FF00FF">FGC    </font> | 从应用程序启动到采样时old代(全gc)gc次数

##10、jstat -gcold <pid>：old代对象的信息

       PC       PU        OC          OU       YGC    FGC    FGCT     GCT   
    111616.0  57980.6    451584.0    259617.6    168     1    0.463   10.105

输出参数|说明
---|---
<font color="#FF00FF">PC  </font> | Perm(持久代)的容量 (字节)
<font color="#FF00FF">PU  </font> | Perm(持久代)目前已使用空间 (字节)
<font color="#FF00FF">OC  </font> | Old代的容量 (字节)
<font color="#FF00FF">OU  </font> | Old代目前已使用空间 (字节)
<font color="#FF00FF">YGC </font> | 从应用程序启动到采样时年轻代中gc次数
<font color="#FF00FF">FGC </font> | 从应用程序启动到采样时old代(全gc)gc次数
<font color="#FF00FF">FGCT</font> | 从应用程序启动到采样时old代(全gc)gc所用时间(s)
<font color="#FF00FF">GCT </font> | 从应用程序启动到采样时gc用的总时间(s)

##11、jstat -gcoldcapacity <pid>: old代对象的信息及其占用量。

       OGCMN       OGCMX        OGC         OC       YGC   FGC    FGCT     GCT   
      343552.0   5503488.0    451584.0    451584.0   168     1    0.463   10.105


输出参数|说明
---|---
<font color="#FF00FF">OGCMN  </font> | old代中初始化(最小)的大小 (字节)
<font color="#FF00FF">OGCMX  </font> | old代的最大容量(字节)
<font color="#FF00FF">OGC    </font> | old代当前新生成的容量 (字节)
<font color="#FF00FF">OC     </font> | Old代的容量 (字节)
<font color="#FF00FF">YGC    </font> | 从应用程序启动到采样时年轻代中gc次数
<font color="#FF00FF">FGC    </font> | 从应用程序启动到采样时old代(全gc)gc次数
<font color="#FF00FF">FGCT   </font> | 从应用程序启动到采样时old代(全gc)gc所用时间(s)
<font color="#FF00FF">GCT    </font> | 从应用程序启动到采样时gc用的总时间(s)

##12、jstat -gcpermcapacity<pid>: perm对象的信息及其占用量。

      PGCMN      PGCMX       PGC         PC      YGC   FGC    FGCT     GCT   
      21504.0   169984.0   111616.0   111616.0   169     1    0.463   10.124

输出参数|说明
---|---
<font color="#FF00FF">PGCMN  </font> | perm代中初始化(最小)的大小 (字节)
<font color="#FF00FF">PGCMX  </font> | perm代的最大容量 (字节)
<font color="#FF00FF">PGC    </font> | perm代当前新生成的容量 (字节)
<font color="#FF00FF">PC     </font> | Perm(持久代)的容量 (字节)
<font color="#FF00FF">YGC    </font> | 从应用程序启动到采样时年轻代中gc次数
<font color="#FF00FF">FGC    </font> | 从应用程序启动到采样时old代(全gc)gc次数
<font color="#FF00FF">FGCT   </font> | 从应用程序启动到采样时old代(全gc)gc所用时间(s)
<font color="#FF00FF">GCT    </font> | 从应用程序启动到采样时gc用的总时间(s)

##13、jstat -printcompilation <pid>:当前VM执行的信息。

    Compiled  Size  Type         Method
    3086      39     1           java/util/LinkedList toArray

输出参数|说明
---|---
<font color="#FF00FF">Compiled </font> |   编译任务的数目
<font color="#FF00FF">Size     </font> |   方法生成的字节码的大小
<font color="#FF00FF">Type     </font> |   编译类型
<font color="#FF00FF">Method   </font> |   类名和方法名用来标识编译的方法。类名使用/做为一个命名空间分隔符。方法名是给定类中的方法。上述格式是由-XX:+PrintComplation选项进行设置的







































