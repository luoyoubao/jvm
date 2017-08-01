#### CMS收集器(Concurrent Mark Sweep) ####
**CMS收集器(Concurrent Mark Sweep)**是一种以获取最短回收停顿时间为目标的收集器

#### 特性 ####
* 目标：获取最短回收停顿时间
* 适用于互联网B/S系统服务端
* 基于“标记-清除”算法实现


#### CMS"标记-清除"算法实现 ####
1. 初始标记(CMS initial mark)
2. 并发标记(CMS concurrent mark)
3. 重新标记(CMS remark)
4. 并发清除(CMS concurrent sweep)
说明：初始标记、重新标记仍然需要Stop The World