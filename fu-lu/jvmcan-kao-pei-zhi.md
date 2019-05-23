### JVM参数设置

| 参数 | 内容 |
| :--- | :--- |
| -Xms | 初始堆大小。如：-Xms256m；默认物理内存 1/64 |
| -Xmx | 最大堆大小。如：-Xmx512m；默认物理内存 1/4 |
| -Xmn:\[g\|m\|k\] | 新生代大小。新生代 = Eden + 2 个 Survivor 空间。实际可用空间为 = Eden + 1 个 Survivor，即 90%；整个JVM内存大小=年轻代大小 + 年老代大小 + 持久代大小。持久代一般固定大小为64m，所以增大年轻代后，将会减小年老代大小；如果Xms和Xmx没有设置为同一个值时，堆空间扩展或收缩时，新生代大小是不会随着调整的，是固定的，只有Xms和Xmx是同一个值得时候，才使用Xmn选项 |
| -Xss | 设置每个线程的堆栈大小；JDK1.5+ 每个线程堆栈大小为 1M，一般来说如果栈不是很深的话， 1M 是绝对够用了的。 |
| -XX:NewRatio | 新生代与老年代的比例，如 –XX:NewRatio=2，则新生代占整个堆空间的1/3，老年代占2/3 |
| -XX:SurvivorRatio | 新生代中 Eden\(8\) 与 Survivor\(1+1\) 的比值。默认值为 8。即 Eden 占新生代空间的 8/10，另外两个 Survivor 各占 1/10 |
| -XX:PermSize | 永久代\(方法区\)的初始大小 |
| -XX:MaxPermSize | 永久代\(方法区\)的最大值 |
| -XX:+PrintGCDetails | 打印 GC 信息 |
| -XX:+HeapDumpOnOutOfMemoryError | 让虚拟机在发生内存溢出时 Dump 出当前的内存堆转储快照，以便分析用 |
| -XX:NewSize=\[g\|m\|k\] | 设置新生代最小空间大小 |
| -XX:MaxNewSize | 设置新生代最大空间大小 |
| -XX:MetaspaceSize | class metadata的初始空间配额，以bytes为单位，达到该值就会触发垃圾收集进行类型卸载，同时GC会对该值进行调整 |
| XX:MaxMetaspaceSize | 可以为class metadata分配的最大空间。默认是没有限制的 |
| MinHeapFreeRatio | GC后如果发现空闲堆内存占到整个预估堆内存的N%\(百分比\), 则放大堆内存的预估最大值 |
| MaxHeapFreeRatio | GC后如果发现空闲堆内存占到整个预估堆内存的N%\(百分比\)，则收缩堆内存的预估最大值, 预估堆内存是堆大小动态调控的重要选项之一. 堆内存预估最大值一定小于或等于固定最大值\(-Xmx指定的数值\). 前者会根据使用情况动态调大或缩小, 以提高GC回收的效率 |

_注意：java8去掉了-XX:PermSize和-XX:MaxPermSize，新增了-XX:MetaspaceSize和-XX:MaxMetaspaceSize_

虚拟机会根据堆的空闲情况动态调整推大小，空余大于 70%，会减少到 -Xms，空余小于 40%，会增大到 -Xmx；服务器如果配置 -Xms = -Xmx，则可以避免堆自动扩展；

### 参考配置\(QC\)

```
JAVA_OPTS="-server -Xss256k $JAVA_OPTS"
JAVA_OPTS="${JAVA_OPTS} -XX:SurvivorRatio=10"
JAVA_OPTS="${JAVA_OPTS} -XX:+UseConcMarkSweepGC  -XX:CMSMaxAbortablePrecleanTime=5000 -XX:+CMSClassUnloadingEnabled -XX:CMSInitiatingOccupancyFraction=80"
JAVA_OPTS="${JAVA_OPTS} -XX:+UseCMSInitiatingOccupancyOnly"
JAVA_OPTS="${JAVA_OPTS} -XX:+DisableExplicitGC"
JAVA_OPTS="${JAVA_OPTS} -verbose:gc -Xloggc:/root/logs/app-gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps"
JAVA_OPTS="${JAVA_OPTS} -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/root/logs/app-java.hprof"
JAVA_OPTS="${JAVA_OPTS} -Djava.awt.headless=true"
JAVA_OPTS="${JAVA_OPTS} -Dsun.net.client.defaultConnectTimeout=10000"
JAVA_OPTS="${JAVA_OPTS} -Dsun.net.client.defaultReadTimeout=30000"
java -Djava.security.egd=file:/dev/./urandom $JAVA_OPTS -jar ./app.jar  $*
```

### 其它

* -Xint

解释执行不对代码进行编译，这种模式抛弃了 JIT 可能带来的性能优势，毕竟解释器（interpreter）是逐条读入，逐条解释运行的；

* -Xcomp

关闭解释器，不要进行解释执行，或者叫作最大优化级别；“-Xcomp”会导致 JVM 启动变慢非常多，同时有些JIT 编译器优化方式，比如分支预测，如果不进行 profiling，往往并不能进行有效优化

