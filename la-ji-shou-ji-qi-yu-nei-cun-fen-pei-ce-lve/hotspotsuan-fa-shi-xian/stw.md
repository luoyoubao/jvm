### STW\(Stop The World\)

> 只有标记阶段才需要STW

标记完成以后，需要清除的对象已经确定，无论此时是否产生新的垃圾，都不影响对这些对象的清理。也就是说，清除阶段是可以设计成和用户线程并发执行的

JVM在暂停的时候，需要选准一个时机，由于JVM系统运行期间的复杂性，不可能做到随时暂停，因此引入了安全点（safepoint）的概念：程序只有在运行到安全点的时候，才可以暂停下来。HotSpot采用主动中断的方式，让执行线程在运行期轮询是否需要暂停的标志，若需要则中断挂起。HotSpot使用了几条短小精炼的汇编指令便可完成安全点轮询以及触发线程中断，因此对系统性能的影响几乎可以忽略不计

