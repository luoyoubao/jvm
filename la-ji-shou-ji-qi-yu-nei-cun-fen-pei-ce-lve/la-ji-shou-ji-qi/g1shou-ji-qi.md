### G1\(Garbage First\)

G1 GC，全称Garbage-First Garbage Collector，通过-XX:+UseG1GC参数来启用，作为体验版随着JDK 6u14版本面世，在JDK 7u4版本发行时被正式推出，相信熟悉JVM的同学们都不会对它感到陌生。在JDK 9中，G1被提议设置为默认垃圾收集器（JEP 248）

G1是一种服务器端的垃圾收集器，应用在多处理器和大容量内存环境中，在实现高吞吐量的同时，尽可能的满足垃圾收集暂停时间的要求。它是专门针对以下应用场景设计的:

* 像CMS收集器一样，能与应用程序线程并发执行
* 整理空闲空间更快
* 需要GC停顿时间更好预测
* 不希望牺牲大量的吞吐性能
* 不需要更大的Java Heap

#### 特性

* 面向服务端应用的垃圾收集器
* **并行与并发：**G1能充分利用多CPU、多核环境使用多个CPU或CPU核心来缩短Stop-The-World停顿时间
* 分代收集
* 空间整合：不会产生内存空间碎片，收集后可提供规整的可用内存，整理空闲空间更快
* 可预测的停顿\(它可以有计划的避免在整个JAVA堆中进行全区域的垃圾收集\)
* **JAVA堆内存布局与其它收集器存在很大差别**，它将整个JAVA堆划分为多个大小相等的独立区域\(Region\)，虽然还保留了新生代和老年代的概念，但新生代和老年代不再是物理隔离，它们都是一部分Region\(不需要连续\)的集合
* G1收集器中，虚拟机使用Remembered Set来避免全堆扫描

#### 运作步骤

* 初始标记：Initial Marking
* 并发标记：Concurrent Marking
* 最终标记：Final Marking
* 筛选回收：Live Data Counting And Evacuation

【参考资料】

【美团--Java Hotspot G1 GC的一些关键技术】-- [https://tech.meituan.com/g1.html](#)

