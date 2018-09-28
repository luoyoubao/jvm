### 内存屏障\(Memory Barrier\)

内存屏障（Memory Barrier，或叫做内存栅栏，Memory Fence）是一种CPU指令，用于控制特定条件下的重排序和内存可见性问题。Java编译器也会根据内存屏障的规则禁止重排序，内存屏障可以禁止特定类型处理器的重排序，从而让程序按我们预想的流程去执行。

内存栅栏\(Memory Barrier\)：内存栅栏可以刷新缓存，使缓存无效，刷新硬件的写缓冲，以及停止执行管道

内存屏障是一条这样的指令：

* 保证特定操作的执行顺序。

* 影响某些数据（或是某条指令的执行结果）的内存可见性。

编译器和CPU能够重排序指令，保证最终相同的结果，尝试优化性能。插入一条Memory Barrier会告诉编译器和CPU：不管什么指令都不能和这条Memory Barrier指令重排序。

Memory Barrier所做的另外一件事是强制刷出各种CPU cache，如一个Write-Barrier（写入屏障）将刷出所有在Barrier之前写入 cache 的数据，因此，任何CPU上的线程都能读取到这些数据的最新版本。

```
“这和java有什么关系？上面java内存模型中讲到的volatile是基于Memory Barrier实现的”
```

如果一个变量是volatile修饰的，JMM会在写入这个字段之后插进一个Write-Barrier指令，并在读这个字段之前插入一个Read-Barrier指令。这意味着，如果写入一个volatile变量，就可以保证：

* 一个线程写入变量a后，任何线程访问该变量都会拿到最新值。

* 在写入变量a之前的写入操作，其更新的数据对于其他线程也是可见的。因为Memory Barrier会刷出cache中的所有先前的写入。

### 内存屏障类型

* LoadLoad屏障：对于这样的语句Load1; LoadLoad; Load2，在Load2及后续读取操作要读取的数据被访问前，保证Load1要读取的数据被读取完毕。

* StoreStore屏障：对于这样的语句Store1; StoreStore; Store2，在Store2及后续写入操作执行前，保证Store1的写入操作对其它处理器可见。

* LoadStore屏障：对于这样的语句Load1; LoadStore; Store2，在Store2及后续写入操作被刷出前，保证Load1要读取的数据被读取完毕。

* StoreLoad屏障：对于这样的语句Store1; StoreLoad; Load2，在Load2及后续所有读取操作执行前，保证Store1的写入对所有处理器可见。它的开销是四种屏障中最大的。在大多数处理器的实现中，这个屏障是个万能屏障，兼具其它三种内存屏障的功能

基于保守策略的JMM内存屏障插入策略：

* 在每个volatile写操作的前面插入一个StoreStore屏障；
* 在每个volatile写操作的后面插入一个StoreLoad屏障；
* 在每个volatile读操作的后面插入一个LoadLoad屏障；
* 在每个volatile读操作的后面插入一个LoadStore屏障；

基于保守策略下，volatile写插入内存屏障后生成的指令序列示意图

![](/assets/20180928155831001.png)

上图中的StoreStore屏障可以保证在volatile写之前，其前面的所有普通写操作已经对任意处理器可见了。这是因为StoreStore屏障将保障上面所有的普通写在volatile写之前刷新到主内存

_**参考资料**_

【Java内存模型Cookbook（二）内存屏障】[http://ifeve.com/jmm-cookbook-mb/](http://ifeve.com/jmm-cookbook-mb/)

