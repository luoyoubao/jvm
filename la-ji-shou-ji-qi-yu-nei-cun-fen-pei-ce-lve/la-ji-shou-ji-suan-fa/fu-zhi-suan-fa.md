### 复制算法\(Copying\)

**原理：**复制算法，它将堆上的内存分为两个大小相等的区域，一个是空闲区域，一个是活动区域。在程序运行中，实际使用的是活动区域，也就是有50%的空间被浪费掉

#### 复制算法的实现过程：

1. 找出活动空间中所有存活的对象
2. 将这些存活的对象复制到空闲区域
3. 将之前的活动空间清空变为空闲空间，而存活对象所在的区域则变为活动空间

#### 优缺点

优点：实现简单，运行高效  
缺点：内存缩小了一半

#### 重点

* 现在的商业JVM都采用这种收集算法来回收新生代
* Eden:Survivor=8:1\(HotSpot默认\)
* 分配担保\(Handle Promotion\)，当Survivor空间不够时，需要老年代进行分配担保

#### HotSpot新生代的内存划分

* HotSpot新生代的内存划分比例为80%:10%:10%
* HotSpot新生代的可用内存空间为整个新生代容量的90%\(80%+10%\)，只有10%的内存闲置\("浪费"\)



