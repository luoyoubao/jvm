### JVM参数设置

| 参数 | 内容 |
| :--- | :--- |
| **-Xms** | 初始堆大小。如：-Xms256m；默认物理内存 1/64 |
| -Xmx | 最大堆大小。如：-Xmx512m；默认物理内存 1/4 |
| -Xmn | 新生代大小。通常为 Xmx 的 1/3 或 1/4。新生代 = Eden + 2 个 Survivor 空间。实际可用空间为 = Eden + 1 个 Survivor，即 90% |
| -Xss | 设置每个线程的堆栈大小；JDK1.5+ 每个线程堆栈大小为 1M，一般来说如果栈不是很深的话， 1M 是绝对够用了的。 |
| -XX:NewRatio | 新生代与老年代的比例，如 –XX:NewRatio=2，则新生代占整个堆空间的1/3，老年代占2/3 |
| **-XX:SurvivorRatio** | 新生代中 Eden\(8\) 与 Survivor\(1+1\) 的比值。默认值为 8。即 Eden 占新生代空间的 8/10，另外两个 Survivor 各占 1/10 |
| -XX:PermSize | 永久代\(方法区\)的初始大小 |
| **-XX:MaxPermSize** | 永久代\(方法区\)的最大值 |
| -XX:+PrintGCDetails | 打印 GC 信息 |
| -XX:+HeapDumpOnOutOfMemoryError | 让虚拟机在发生内存溢出时 Dump 出当前的内存堆转储快照，以便分析用 |

### 

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

PS：参考配置

