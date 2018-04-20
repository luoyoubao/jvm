## JVM运行时数据区\(JAVA内存结构\)

**JVM被分为三个主要的子系统**：

1. 类加载器子系统
2. 运行时数据区
3. 执行引擎

![](/assets/20180420112152001.png)

![](/assets/201803301358001.png)

**控制参数**

* -Xms设置堆的最小空间大小；默认物理内存 1/64
* -Xmx设置堆的最大空间大小；默认物理内存 1/4
* -XX:NewSize设置新生代最小空间大小
* -XX:MaxNewSize设置新生代最大空间大小
* -XX:PermSize设置永久代最小空间大小
* -XX:MaxPermSize设置永久代最大空间大小
* -Xss设置每个线程的堆栈大小
* XX:MetaspaceSize：class metadata的初始空间配额，以bytes为单位，达到该值就会触发垃圾收集进行类型卸载，同时GC会对该值进行调整
* XX:MaxMetaspaceSize：可以为class metadata分配的最大空间。默认是没有限制的
* MaxHeapFreeRatio: GC后如果发现空闲堆内存占到整个预估堆内存的N%\(百分比\)，则收缩堆内存的预估最大值, 预估堆内存是堆大小动态调控的重要选项之一. 堆内存预估最大值一定小于或等于固定最大值\(-Xmx指定的数值\). 前者会根据使用情况动态调大或缩小, 以提高GC回收的效率

* MinHeapFreeRatio: GC后如果发现空闲堆内存占到整个预估堆内存的N%\(百分比\), 则放大堆内存的预估最大值

* SurvivorRatio: Eden/Survivor的值。8表示Survivor:Eden=1:8,因为survivor区有2个, 所以Eden的占比为8/10

_注意：java8去掉了-XX:PermSize和-XX:MaxPermSize，新增了-XX:MetaspaceSize和-XX:MaxMetaspaceSize_

虚拟机会根据堆的空闲情况动态调整推大小，空余大于 70%，会减少到 -Xms，空余小于 40%，会增大到 -Xmx；服务器如果配置 -Xms = -Xmx，则可以避免堆自动扩展；

我们可以认为Major GC == Full GC，他们是一个概念，就是针对老年代/永久代进行GC。因为取名叫Full就会让人疑惑，到底会不会先Minor GC。事实上Full GC本身不会先进行Minor GC，我们可以配置，让Full GC之前先进行一次Minor GC，因为老年代很多对象都会引用到新生代的对象，先进行一次Minor GC可以提高老年代GC的速度。比如老年代使用CMS时，设置CMSScavengeBeforeRemark优化，让CMS remark之前先进行一次Minor GC；

_**参考资料**_

[http://ifeve.com/under-the-hood-runtime-data-areas-javas-memory-model/](http://ifeve.com/under-the-hood-runtime-data-areas-javas-memory-model/)

