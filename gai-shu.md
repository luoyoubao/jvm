## 基本概念

JVM是可运行Java代码的假想计算机 ，包括一套字节码指令集、一组寄存器、一个栈、一个垃圾回收，堆 和 一个存储方法域。JVM是运行在操作系统之上的，它与硬件没有直接的交互

运行过程：Java源文件 -&gt; 编译器 -&gt; 字节码文件 -&gt; JVM -&gt; 机器码

## 当前主流的JVM

* HotSpot   \#Sun
* J9             \#IBM
* JRockit    \#BEA

### JVM主要子系统

\* 类加载器子系统（Class Loader Subsystem）

\* 运行时数据区（Runtime Data Area）

\* 执行引擎（Execution Engine）

## 64位JVM

* 由于指针膨胀和各种数据类型对齐补白的原因，运行于64位系统上的JAVA应用需要消耗更多的内存空间，通常要比32位系统额外增加10%~30%的内存消耗

## 指令集架构

* ARM
* x86
* x64
* Sparc

## JAVA体系结构图

![](/assets/201707272228.png)  
![](/assets/20170921234101.png)

```
SPECjvm2008:基准测试套件。它的测试用例涵盖了大部分java基础应用场景，是架构选型和VM性能评测不可多得的利器
```



