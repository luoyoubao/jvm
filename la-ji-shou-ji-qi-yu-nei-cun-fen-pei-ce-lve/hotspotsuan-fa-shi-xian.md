### HotSpot算法实现 ###
* GC停顿(Stop The World)
* OopMap存放全局对象引用，利用它可以快速准确完成GC Roots枚举

####安全点(Safepoint)#
意思就是一个点, 在这个点, 所有GC Root的状态都是已知并且heap里的对象是一致的; 在这个点进行GC时, 所有的线程都需要block住, 这就是(STW)Stop The World

#### GC停顿方案 ####
* 抢先式中断(Preemptive Suspension)	
* 主动式中断(Voluntary Suspension)

####安全区域(Safe Region)#

#### 重点 #
* 线程处于Sleep状态或Blocked状态时无法响应JVM的中断请求