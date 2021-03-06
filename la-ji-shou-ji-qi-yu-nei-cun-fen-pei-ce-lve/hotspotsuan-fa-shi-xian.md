### HotSpot算法实现

* GC停顿\(Stop The World\)
* OopMap存放全局对象引用，利用它可以快速准确完成GC Roots枚举

#### 安全点\(Safepoint\)

意思就是一个点, 在这个点, 所有GC Root的状态都是已知并且heap里的对象是一致的; 在这个点进行GC时, 所有的线程都需要block住, 这就是\(STW\)Stop The World

#### GC停顿方案

* 抢先式中断\(Preemptive Suspension\)    
* 主动式中断\(Voluntary Suspension\)

#### 安全区域\(Safe Region\)

**安全区域**是指在一段代码片段之中，引用关系不会发生变化，在这个区域的任意地方开始GC都是安全的

#### 重点

* 线程处于Sleep状态或Blocked状态时无法响应JVM的中断请求
* JVM发起GC时会忽略已标识为SafeRegion状态的线程
* 如果线程要离开Safe Region，需要检查系统是否已完成根节点枚举\(或GC过程\)，如果已完成则线程继续执行，否则继续等待直到收到可以安全离开Safe Region的信号



