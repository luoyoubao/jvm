### JAVA堆\(Heap\)

定义：JAVA堆是被所有线程共享的内存区域，在虚拟机启动时创建，是虚拟机管理的内存中最大的一块空间

#### JAVA虚拟机规范描述
所有的对象实例以及数组都要在堆上分配

#### 特性 #
* 唯一目的就是存放对象实例
* JAVA堆是垃圾收集器管理的主要区域
* 也被称为GC堆\(Garbage Collected Heap\)
* 根据JAVA虚拟机规范规定，JAVA堆物理上可以位于不连续的内存空间中，只要逻辑上连续即可

#### 知识点 ####
* 基于OpenJDK深度定制的TaoBaoVM,使用GCIH(GC invisible heap)技术实现off-heap，将生命周期较长的JAVA对象从heap中移至heap外，且GC不能管理GCIH内部的JAVA对象，以此达到降低GC回收频率和提升GC回收效率的目的
* 逃逸分析
* 栈上分配
* JAVA Heap将不再是JAVA对象内存分配的唯一选择


#### JAVA Heap分代 ####
![](/assets/201708040028.png)



