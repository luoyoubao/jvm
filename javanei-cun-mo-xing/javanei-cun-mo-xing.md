### JAVA内存模型\(JMM\)

定义：Java内存模型即Java Memory Model，简称JMM；

> **JMM定义了Java虚拟机\(JVM\)在计算机内存\(RAM\)中的工作方式**

简单的讲，java内存模型指的就是一套规范，现在最新的规范为JSR-133。

这套规范包含：

* 线程之间如何通过内存通信
* 线程之间通过什么方式通信才合法，才能得到期望的结果

JSR133为Java语言定义了一个新的内存模型，它修复了早期内存模型中的缺陷

在编译器各种优化及多种类型的微架构平台上，Java语言规范制定者试图创建一个虚拟的概念并传递到Java程序员，让他们能够在这个虚拟的概念上写出线程安全的程序来，而编译器实现者会根据Java语言规范中的各种约束在不同的平台上达到Java程序员所需要的线程安全这个目的

在多处理器下，为了保证各个处理器的缓存是一致的，就会实现缓存一致性协议，每个处理器通过嗅探在总线上传播的数据来检查自己缓存的值是不是过期了，当处理器发现自己缓存行对应的内存地址被修改，就会将当前处理器的缓存行设置成无效状态，当处理器对这个数据进行修改操作的时候，会重新从系统内存中把数据读到处理器缓存里；

![](/assets/20180613095708001.png)![](/assets/20200608235240.png)



_在处理器层面上，内存模型定义了一个充要条件，“让当前的处理器可以看到其他处理器写入到内存的数据”以及“其他处理器可以看到当前处理器写入到内存的数据”。有些处理器有很强的内存模型\(strong memory model\)，能够让所有的处理器在任何时候任何指定的内存地址上都可以看到完全相同的值。而另外一些处理器则有较弱的内存模型（weaker memory model），在这种处理器中，必须使用内存屏障（一种特殊的指令）来刷新本地处理器缓存并使本地处理器缓存无效，目的是为了让当前处理器能够看到其他处理器的写操作或者让其他处理器能看到当前处理器的写操作。这些内存屏障通常在lock和unlock操作的时候完成。内存屏障在高级语言中对程序员是不可见的_

**Java包含了几个语言级别的关键字，包括：volatile, final以及synchronized，目的是为了帮助程序员向编译器描述一个程序的并发需求**。Java内存模型定义了volatile和synchronized的行为，更重要的是保证了同步的java程序在所有的处理器架构下面都能正确的运行

![](/assets/20180413163825001.png)

从上图来看，线程A与线程B之间如要通信的话，必须要经历下面2个步骤：

1. 首先线程A把本地内存A中更新过的共享变量刷新到主内存中去。
2. 然后线程B到主内存中去读取线程A之前已更新过的共享变量。

下面通过示意图来说明这两个步骤：

![](/assets/20180413163905001.png)

如上图所示，本地内存A和B有主内存中共享变量x的副本。假设初始时，这三个内存中的x值都为0。线程A在执行时，把更新后的x值（假设值为1）临时存放在自己的本地内存A中。当线程A和线程B需要通信时，线程A首先会把自己本地内存中修改后的x值刷新到主内存中，此时主内存中的x值变为了1。随后，线程B到主内存中去读取线程A更新后的x值，此时线程B的本地内存的x值也变为了1。

从整体来看，这两个步骤实质上是线程A在向线程B发送消息，而且这个通信过程必须要经过主内存。JMM通过控制主内存与每个线程的本地内存之间的交互，来为java程序员提供内存可见性保证。

### Java内存模型的抽象结构

在Java中，所有实例域、静态域和数组元素都存储在堆内存中，堆内存在线程之间共享；局部变量（LocalVariables），方法定义参数（Java语言规范称之为FormalMethodParameters）和异常处理器参数（ExceptionHandlerParameters）不会在线程之间共享，它们不会有内存可见性问题，也不受内存模型的影响；

Java线程之间的通信由Java内存模型（本文简称为JMM）控制，JMM决定一个线程对共享变量的写入何时对另一个线程可见。从抽象的角度来看，JMM定义了线程和主内存之间的抽象关系：线程之间的共享变量存储在主内存（MainMemory）中，每个线程都有一个私有的本地内存（LocalMemory），本地内存中存储了该线程以读/写共享变量的副本。本地内存是JMM的一个抽象概念，并不真实存在。它涵盖了缓存、写缓冲区、寄存器以及其他的硬件和编译器优化；

JVM中运行的每个线程都拥有自己的线程栈，线程栈包含了当前线程执行的方法调用相关信息，我们也把它称作调用栈。随着代码的不断执行，调用栈会不断变化。

线程栈还包含了当前方法的所有本地变量信息。一个线程只能读取自己的线程栈，也就是说，线程中的本地变量对其它线程是不可见的。即使两个线程执行的是同一段代码，它们也会各自在自己的线程栈中创建本地变量，因此，每个线程中的本地变量都会有自己的版本。

所有原始类型\(boolean,byte,short,char,int,long,float,double\)的本地变量都直接保存在线程栈当中，对于它们的值各个线程之间都是独立的。对于原始类型的本地变量，一个线程可以传递一个副本给另一个线程，但它们之间是无法共享的。

堆区包含了Java应用创建的所有对象信息，不管对象是哪个线程创建的，其中的对象包括原始类型的封装类（如Byte、Integer、Long等等）。不管对象是属于一个成员变量还是方法中的本地变量，它都会被存储在堆区。

下图展示了调用栈和本地变量都存储在栈区，对象都存储在堆区：

![](/assets/20180413164322001.png)

特性

* 一个本地变量如果是原始类型，那么它会被完全存储到栈区；
* 一个本地变量也有可能是一个对象的引用，这种情况下，这个本地引用会被存储到栈中，但是对象本身仍然存储在堆区。
* 对于一个对象的成员方法，这些方法中包含本地变量，仍需要存储在栈区，即使它们所属的对象在堆区。
* 对于一个对象的成员变量，不管它是原始类型还是包装类型，都会被存储到堆区。
* static类型的变量以及类本身相关信息都会随着类本身存储在方法区；

堆中的对象可以被多线程共享。如果一个线程获得一个对象的引用，它便可访问这个对象的成员变量。如果两个线程同时调用了同一个对象的同一个方法，那么这两个线程便可同时访问这个对象的成员变量，但是对于本地变量，每个线程都会拷贝一份到自己的线程栈中，下图展示了上面描述的过程：

![](/assets/20180413164636001.png)

### 支撑Java内存模型的基础原理

* **指令重排序**
* **数据依赖性**

如果两个操作访问同一个变量，其中一个为写操作，此时这两个操作之间存在数据依赖性。 编译器和处理器不会改变存在数据依赖性关系的两个操作的执行顺序，即不会重排序。

| 名称 | 代码示例 | 说明 |
| :--- | :--- | :--- |
| 写后读 | a = 1;b = a; | 写一个变量之后，再读这个位置。 |
| 写后写 | a = 1;a = 2; | 写一个变量之后，再写这个变量。 |
| 读后写 | a = b;b = 1; | 读一个变量之后，再写这个变量。 |

* **as-if-serial**

不管怎么重排序，单线程下的执行结果不能被改变，编译器、runtime和处理器都必须遵守as-if-serial语义

```
double pi  = 3.14;    //A  
double r   = 1.0;     //B  
double area = pi * r * r; //C
```

```
上面三个操作的数据依赖关系如下图所示：
```

![](http://img.my.csdn.net/uploads/201302/06/1360143739_6151.png)

如上图所示，A和C之间存在数据依赖关系，同时B和C之间也存在数据依赖关系。因此在最终执行的指令序列中，C不能被重排序到A和B的前面（C排到A和B的前面，程序的结果将会被改变）。但A和B之间没有数据依赖关系，编译器和处理器可以重排序A和B之间的执行顺序。下图是该程序的两种执行顺序：

![](http://img.my.csdn.net/uploads/201302/06/1360143751_3794.png)

as-if-serial语义把单线程程序保护了起来，遵守as-if-serial语义的编译器，runtime 和处理器共同为编写单线程程序的程序员创建了一个幻觉：单线程程序是按程序的顺序来执行的。**as-if-serial语义使单线程程序员无需担心重排序会干扰他们，也无需担心内存可见性问题**。

_**参考资料**_

【Java内存模型FAQ（一） 什么是内存模型】  [http://ifeve.com/memory-model](http://ifeve.com/memory-model)

【全面理解Java内存模型】[https://blog.csdn.net/suifeng3051/article/details/52611310](https://blog.csdn.net/suifeng3051/article/details/52611310)

【深入理解Java内存模型（一）——基础】 [http://www.infoq.com/cn/articles/java-memory-model-1](http://www.infoq.com/cn/articles/java-memory-model-1)

【Java内存模型FAQ】 [http://ifeve.com/jmm-faq/](http://ifeve.com/jmm-faq/)

