### 相关概念

* Minor GC：新生代GC，指发生在新生代空间（包括Eden和Survivor区域）的垃圾收集动作，所有的Minor GC都会触发全世界的暂停（stop-the-world），停止应用程序的线程，不过这个过程非常短暂。

* Major GC：针对所有分代区域（新生代、年老代）的GC

* Full GC：而Full GC是对整个堆来说的，在最近几个版本的JDK里默认包括了对永久代\(Hotspot GC覆盖了永久代\)即方法区的回收（JDK8移除了PermGen）；

我们可以认为Major GC == Full GC，他们是一个概念，就是针对老年代/永久代进行GC。因为取名叫Full就会让人疑惑，到底会不会先Minor GC。事实上Full GC本身不会先进行Minor GC，我们可以配置，让Full GC之前先进行一次Minor GC，因为老年代很多对象都会引用到新生代的对象，先进行一次Minor GC可以提高老年代GC的速度。比如老年代使用CMS时，设置CMSScavengeBeforeRemark优化，让CMS remark之前先进行一次Minor GC；

特性：

* 出现Full GC的时候经常伴随至少一次的Minor GC,但非绝对的；
* Major GC的速度一般会比Minor GC慢10倍以上；

#### 老年代内存溢出

老年代空间只有在新生代对象转入及创建为大对象、大数组时才会出现不足的现象，当执行Full GC后空间仍然不足，则抛出如下错误：java.lang.OutOfMemoryError: Java heap space

为避免以上两种状况引起的Full GC，调优时应尽量做到让对象在Minor GC阶段被回收、让对象在新生代多存活一段时间及不要创建过大的对象及数组

#### 永久代内存溢出

JVM规范中运行时数据区域中的方法区，在HotSpot虚拟机中又被习惯称为永生代或者永生区，Permanet Generation中存放的为一些class的信息、常量、静态变量等数据，当系统中要加载的类、反射的类和调用的方法较多时，Permanet Generation可能会被占满，在未配置为采用CMS GC的情况下也会执行Full GC。如果经过Full GC仍然回收不了，那么JVM会抛出如下错误信息：java.lang.OutOfMemoryError: PermGen space

为避免Perm Gen占满造成Full GC现象，可采用的方法为增大Perm Gen空间或转为使用CMS GC

