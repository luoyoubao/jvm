在虚拟机层面，为了尽可能减少内存操作速度远慢于CPU运行速度所带来的CPU空置的影响，虚拟机会按照自己的一些规则将程序编写顺序打乱——即写在后面的代码在时间顺序上可能会先执行，而写在前面的代码会后执行——以尽可能充分地利用CPU

### JVM **Happen-Before规则**

* **程序次序规则\(Program Order Rule\)**

在一个线程内，按照代码顺序，书写在前面的操作先行发生于书写在后面的操作。准确地说应该是控制流顺序而不是代码顺序，因为要考虑分支、循环等结构。

* **监视器锁定规则\(Monitor Lock Rule\)**

一个unlock操作先行发生于后面对同一个对象锁的lock操作。这里强调的是同一个锁，而“后面”指的是时间上的先后顺序，如发生在其他线程中的lock操作。

* **volatile变量规则\(Volatile Variable Rule\)**

volatile变量的写先发生于读，这保证了volatile变量的可见性

* **线程启动规则\(Thread Start Rule\)**

Thread独享的start\(\)方法先行于此线程的每一个动作。

* **线程终止规则\(Thread Termination Rule\)**

线程中的每个操作都先行发生于对此线程的终止检测，我们可以通过Thread.join\(\)方法结束、Thread.isAlive\(\)的返回值检测到线程已经终止执行。

* **线程中断规则\(Thread Interruption Rule\)**

对线程interrupte\(\)方法的调用优先于被中断线程的代码检测到中断事件的发生，可以通过Thread.interrupted\(\)方法检测线程是否已中断。

* **对象终结原则\(Finalizer Rule\)**

一个对象的初始化完成\(构造函数执行结束\)先行发生于它的finalize\(\)方法的开始。

* **传递性\(Transitivity\)**

如果操作A先行发生于操作B，操作B先行发生于操作C，那就可以得出操作A先行发生于操作C的结论。

说明：正是以上这些规则保障了happen-before的顺序，如果不符合以上规则，那么在多线程环境下就不能保证执行顺序等同于代码顺序，也就是“如果在本线程中观察，所有的操作都是有序的；如果在一个线程中观察另外一个线程，则不符合以上规则的都是无序的”，因此，如果我们的多线程程序依赖于代码书写顺序，那么就要考虑是否符合以上规则，如果不符合就要通过一些机制使其符合，最常用的就是synchronized、Lock以及volatile修饰符。

参考资料

【happens-before俗解】[http://ifeve.com/easy-happens-before/](http://ifeve.com/easy-happens-before/)

