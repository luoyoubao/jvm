## JVM运行时数据区\(JAVA内存结构\)

**JVM被分为三个主要的子系统**：

1. 类加载器子系统
2. 运行时数据区
3. 执行引擎

![](/assets/20180420112152001.png)

![](/assets/201803301358001.png)





minorGC\(Young GC\)：只针对新生代区域的GC。

majorGC\(Full GC\)：针对所有分代区域（新生代、年老代）的GC

我们可以认为Major GC == Full GC，他们是一个概念，就是针对老年代/永久代进行GC。因为取名叫Full就会让人疑惑，到底会不会先Minor GC。事实上Full GC本身不会先进行Minor GC，我们可以配置，让Full GC之前先进行一次Minor GC，因为老年代很多对象都会引用到新生代的对象，先进行一次Minor GC可以提高老年代GC的速度。比如老年代使用CMS时，设置CMSScavengeBeforeRemark优化，让CMS remark之前先进行一次Minor GC；

_**参考资料**_

[http://ifeve.com/under-the-hood-runtime-data-areas-javas-memory-model/](http://ifeve.com/under-the-hood-runtime-data-areas-javas-memory-model/)

