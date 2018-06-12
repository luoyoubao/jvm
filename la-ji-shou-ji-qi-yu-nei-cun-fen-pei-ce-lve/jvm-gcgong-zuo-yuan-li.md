### 相关概念

* Minor GC：新生代GC，指发生在新生代空间（包括Eden和Survivor区域）的垃圾收集动作，所有的Minor GC都会触发全世界的暂停（stop-the-world），停止应用程序的线程，不过这个过程非常短暂。

* Major GC：针对所有分代区域（新生代、年老代）的GC

* Full GC：而Full GC是对整个堆来说的，在最近几个版本的JDK里默认包括了对永久代\(Hotspot GC覆盖了永久代\)即方法区的回收（JDK8移除了PermGen）；

我们可以认为Major GC == Full GC，他们是一个概念，就是针对老年代/永久代进行GC。因为取名叫Full就会让人疑惑，到底会不会先Minor GC。事实上Full GC本身不会先进行Minor GC，我们可以配置，让Full GC之前先进行一次Minor GC，因为老年代很多对象都会引用到新生代的对象，先进行一次Minor GC可以提高老年代GC的速度。比如老年代使用CMS时，设置CMSScavengeBeforeRemark优化，让CMS remark之前先进行一次Minor GC；

特性：

出现Full GC的时候经常伴随至少一次的Minor GC,但非绝对的；

Major GC的速度一般会比Minor GC慢10倍以上；

