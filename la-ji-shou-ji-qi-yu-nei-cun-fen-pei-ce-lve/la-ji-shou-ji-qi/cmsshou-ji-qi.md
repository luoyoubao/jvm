### CMS收集器(Concurrent Mark Sweep) ###
**CMS收集器(Concurrent Mark Sweep)**是一种以获取最短回收停顿时间为目标的收集器

#### 特性 ####
* 目标：获取最短回收停顿时间
* 适用于互联网B/S系统服务端
* 基于“标记-清除”算法实现
* 也称为并发低停顿收集器
* JDK1.5默认设置下CMS收集器当老年代使用了68%的空间后就会被激活
* JDK1.6CMS收集器的启动阈值提升至92%
* 如果CMS运行期间预留的内存无法满足应用程序需要，就会出现一次"Concurrent Mode Failure"失败，此时将启动后备预案：临时启用Serial Old收集器重新进行老年代的垃圾收集

#### 优缺点 ####
* 优点:并发收集、低停顿
* 缺点:
1.对CPU资源非常敏感
2.无法处理浮动垃圾(Floating Garbage)
3.“标记-清除”算法会产生大量空间碎片


#### CMS"标记-清除"算法实现 ####
1. 初始标记(CMS initial mark)
2. 并发标记(CMS concurrent mark)
3. 重新标记(CMS remark)
4. 并发清除(CMS concurrent sweep)<br>
**说明：**初始标记、重新标记仍然需要Stop The World