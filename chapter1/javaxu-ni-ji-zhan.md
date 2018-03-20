### JAVA虚拟机栈\(Java Virtual Machine Stacks\)

定义：Java虚拟机栈\(栈帧/针栈\)是线程私有的，它的生命周期与线程相同

#### 特性

* 虚拟机栈描述的是JAVA方法执行的内存模型；
* 每个方法执行时都会创建一个栈帧\(Stack Frame\)；
* 每个方法从调用到执行完成的过程，对应着一个栈帧在虚拟机栈中入栈到出栈的过程；
* 线程私有

* 后进先出（LIFO）栈

#### 存储内容

* 局部变量表
* 动态链接\(Dynamic Linking\)
* 操作数栈
* 方法出口\(方法返回地址\)
* 额外附加信息

#### 动态链接

**动态链接：**一个指向运行时常量池中该栈帧所属方法的引用，包含这个引用的目的就是为了支持当前方法的代码能够实现动态链接

#### returnAddress

![](/assets/20170807090817.png)

#### Exception

* StackOverflowError：如果线程请求的栈深度大于虚拟机所允许的深度，抛出StackOverflowError异常；
* OutOfMemoryError：如果虚拟机栈动态扩展时无法申请到足够的内存，抛出OutOfMemoryError异常；



