### JAVA内存模型\(JMM\)

定义：Java内存模型即Java Memory Model，简称JMM；JMM定义了Java虚拟机\(JVM\)在计算机内存\(RAM\)中的工作方式

简单的讲，java内存模型指的就是一套规范，现在最新的规范为JSR-133。这套规范包含：

* 线程之间如何通过内存通信
* 线程之间通过什么方式通信才合法，才能得到期望的结果

在编译器各种优化及多种类型的微架构平台上，Java语言规范制定者试图创建一个虚拟的概念并传递到Java程序员，让他们能够在这个虚拟的概念上写出线程安全的程序来，而编译器实现者会根据Java语言规范中的各种约束在不同的平台上达到Java程序员所需要的线程安全这个目的

![](/assets/20180413143521001.png)

为了方便线程之间的通信，java 提供了 volatile, synchronized, final 三个关键字供我们使用

参考资料

【全面理解Java内存模型】[https://blog.csdn.net/suifeng3051/article/details/52611310](https://blog.csdn.net/suifeng3051/article/details/52611310)

