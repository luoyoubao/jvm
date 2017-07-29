### 内存管理算法

* 引用计数算法\(Reference Counting\)
* 可达性分析算法\(Reachability Analysis\)

##### 引用计数算法

对于创建的每一个对象都有一个与之关联的计数器，这个计数器记录着该对象被使用的次数，垃圾收集器在进行垃圾回收时，对扫描到的每一个对象判断一下计数器是否等于0，若等于0，就会释放该对象占用的内存空间,同时将该对象引用的其他对象的计数器进行减一操作

* 优点：实现简单，高效
* 缺点：无法解决对象相互循环引用问题
* 当前主流JVM没有选用引用计数法来管理内存

##### 可达性分析算法

算法的基本思路就是通过一系列的称为“GC Roots”的对象作为起始点，从这些节点开始向下搜索，搜索所走过的路径称为引用链（Reference Chain），当一个对象到GC Roots没有任何引用链相连（用图论的话来说，就是从GC Roots到这个对象不可达）时，则证明此对象是不可用的。如图3-1所示，对象object 5、object 6、object 7虽然互相有关联，但是它们到GC Roots是不可达的，所以它们将会被判定为是可回收的对象
![](/assets/20170729164201.png)


#####JAVA中的GC Roots对象#
* 虚拟机栈(栈帧中的本地变量表)中引用的对象
* 方法区类静态属性引用的对象
* 本地方法栈中的JNI(即一般说的Native方法)引用的对象
* 方法区中常量引用的对象