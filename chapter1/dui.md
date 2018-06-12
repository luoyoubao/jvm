### JAVA堆\(Heap\)

定义：JAVA堆是被所有线程共享的内存区域，在虚拟机启动时创建，是虚拟机管理的内存中最大的一块空间

堆中对象存储的是该对象以及对象所有超类的实例数据\(但不是静态数据\)；

一个对象的引用可能在整个运行时数据区中的很多地方存在，比如Java栈，堆，方法区等；

#### JAVA虚拟机规范描述

所有的对象实例以及数组都要在堆上分配

#### 特性

* 线程共享
* 内存最大的一块
* 目的：存放对象实例和数组，但随着JIT的发展和逃逸分析技术成熟，栈上分配、标量替换，对象实例开始不一定分配在堆上
* JAVA堆是垃圾收集器管理的主要区域
* 也被称为GC堆\(Garbage Collected Heap\)
* 根据JAVA虚拟机规范规定，JAVA堆物理上可以位于不连续的内存空间中，只要逻辑上连续即可

#### 知识点

* 基于OpenJDK深度定制的TaoBaoVM,使用GCIH\(GC invisible heap\)技术实现off-heap，将生命周期较长的JAVA对象从heap中移至heap外，且GC不能管理GCIH内部的JAVA对象，以此达到降低GC回收频率和提升GC回收效率的目的
* 逃逸分析
* 栈上分配
* JAVA Heap将不再是JAVA对象内存分配的唯一选择

#### JAVA Heap分代

![](/assets/201708040028.png)

* 新生代\(Young Generation\)
* 老生代\(Old Generation\)：Tenured
* Survivor Space通常又称为S0和S1，或者From和To



