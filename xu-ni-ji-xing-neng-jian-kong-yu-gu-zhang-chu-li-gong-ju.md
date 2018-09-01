### -server and -client

* 客户端的VM只在32位系统中可用,可以使用-server和-client参数来设置使用服务端或客户端的VM；
* Server模式下才可以启动逃逸分析；

### 常用命令

```
jps -lv         ##查看JVM进程
jmap -heap 1436       ##查看JVM进程heap详情
Jstack [pid]:查看jvm线程运行状态，是否有死锁现象等等信息
```

#### 常用工具

BTrace

