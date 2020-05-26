### 操作系统对单个进程的内存限制

* 32位系统下，单个进程默认来可以使用2GB内存自；如果系统开启了21133GB模式，并且程序使用了IMAGE\_FILE\_LARGE\_ADDRESS\_AWARE设置，则5261单个进程可以使用41023GB内存

### 本地内存/直接内存\(Direct Memory\)

直接内存并不是虚拟机运行时数据区的一部分，也不是Java虚拟机规范中定义的内存区域，但是这部分内存也被频繁的使用；

内存不足时抛出OutOf-MemoryError或 者OutOfMemoryError：Direct buffer memory

#### 特性

* -XX:MaxDirectMemorySize 最大值，默认和 Java 堆最大值一样

* 不属于运行时数据区

* 本机直接内存的分配不受Java堆大小的限制，仅受本机总内存大小以及处理器寻址空间的限制

说明：在JDK 1.4 中新加入了NIO（New Input/Output）类，引入了一种基于通道（Channel）与缓冲区（Buffer）的I/O 方式，它可以使用Native函数库直接分配堆外内存，然后通过一个存储在Java 堆里面的DirectByteBuffer 对象作为这块内存的引用进行操作。这样能在一些场景中显著提高性能，因为避免了在Java 堆和Native 堆中来回复制数据。

_**注意使用Native函数库分配堆外内存，通过JAVA堆DirectByteBuffer引用堆外内存**_

直接内存是一块物理内存，专门用于JVM和IO设备打交道，Java底层使用C语言的API调用操作系统与IO设备进行交互。

例如，Java内存中有一个字节数组，现在调用流将它写入磁盘文件，那么JVM首先会将这个字节数组先拷贝一份到堆外内存中，然后调用C语言API指明将某个连续地址范围的数据写入磁盘。

读操作也是类似，而JVM额外做的拷贝工作也是有意义的，因为JVM是基于自动垃圾回收机制运行的，所有内存中的数据会在GC时不停的被移动，如果你调用系统API告诉操作系统将内存某某位置的内存写入磁盘，而此时发生GC移动了该部分数据，GC结束后操作系统是不是就写错数据了。

所以，JVM对于与外围IO设备交互的情况下，都会将内存数据复制一份到堆外内存中，然后调用系统API间接的写入磁盘，读也是类似的。由于堆外内存不受GC管理，所以用完一定得记得释放

### 直接内存（堆外内存）与堆内存比较

* 直接内存申请空间耗费更高的性能，当频繁申请到一定量时尤为明显；
* 直接内存IO读写的性能要优于普通的堆内存，在多次读写操作的情况下差异明显；

### 堆外内存

* 直接内存：可通过-XX：MaxDirectMemorySize调整大小，内存不足时抛出OutOf-MemoryError或 者OutOfMemoryError：Direct buffer memory；

* 线程堆栈：可通过-Xss调整大小，内存不足时抛出StackOverflowError（如果线程请求的栈深度大 于虚拟机所允许的深度）或者OutOfMemoryError（如果Java虚拟机栈容量可以动态扩展，当栈扩展时无法申请到足够的内存）；

* Socket缓存区：每个Socket连接都Receive和Send两个缓存区，分别占大约37KB和25KB内存，连接 多的话这块内存占用也比较可观。如果无法分配，可能会抛出IOException：Too many open files异常；

* JNI代码：如果代码中使用了JNI调用本地库，那本地库使用的内存也不在堆中，而是占用Java虚 拟机的本地方法栈和本地内存的；

![](/assets/201708022310.png)

