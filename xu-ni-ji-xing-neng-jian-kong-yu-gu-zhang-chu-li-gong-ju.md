### -server and -client

* 客户端的VM只在32位系统中可用,可以使用-server和-client参数来设置使用服务端或客户端的VM；
* Server模式下才可以启动逃逸分析；

### 常用命令

```
jps -lv         ##查看JVM进程
jmap -heap 1436       ##查看JVM进程heap详情
Jstack [pid]:查看jvm线程运行状态，是否有死锁现象等等信息
jstat:一个极强的监视VM内存工具。可以用来监视VM内存内的各种堆和非堆的大小及其内存使用量
```

#### CPU相关工具

* top
* jstack
* perf

#### 

#### 

#### 内存相关工具

* BTrace
* Jstat
* Jmap
* gcore
* mat
* zprofiler
* jprofiler
* gperf



其它：

VisualVM及其扩展插件VisualGC



