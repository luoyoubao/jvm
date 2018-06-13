### 内存屏障\(Memory Barrier\)

内存屏障（Memory Barrier，或叫做内存栅栏，Memory Fence）是一种CPU指令，用于控制特定条件下的重排序和内存可见性问题。Java编译器也会根据内存屏障的规则禁止重排序，内存屏障可以禁止特定类型处理器的重排序，从而让程序按我们预想的流程去执行。内存屏障是一条这样的指令：

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

_**参考资料**_

【Java内存模型Cookbook（二）内存屏障】[http://ifeve.com/jmm-cookbook-mb/](http://ifeve.com/jmm-cookbook-mb/)

