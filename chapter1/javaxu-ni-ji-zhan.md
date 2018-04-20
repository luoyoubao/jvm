### JAVA虚拟机栈\(Java Virtual Machine Stacks\)

定义：Java虚拟机栈\(栈帧/针栈\)是线程私有的，它的生命周期与线程相同

#### 特性

* 虚拟机栈描述的是JAVA方法执行的内存模型；
* 每个方法执行时都会创建一个栈帧\(Stack Frame\)；
* 每个方法从调用到执行完成的过程，对应着一个栈帧在虚拟机栈中入栈到出栈的过程；
* 后进先出\(LIFO\)栈
* 线程私有；

#### 存储内容

* 局部变量表\(Local Variables\)：以变量槽\(Slot\)为单位，存有this引用，方法参数，定义的局部变量；字节码指令使用从0开始索引来使用其中的数据，而0Slot 都默认为当前方法所属的实例的引用，即this；分配多大的局部变量空间在编译期间已经确定；int，float，reference，returnAddress占一个Slot；byte，short，char会被转成int；long，double占两个连续Slot
* 动态链接\(Dynamic Linking\)：指向运行时常量池中栈帧所属方法的引用，用来支持方法调用中的动态连接。常量池的方法的符号引用，一部分在类加载的时候转化为直接引用，被称为静态解析。而动态连接指的是在每一次运行期间转化为直接引用
* 操作数栈：以变量槽\(Slot为单位\)字节码指令从操作数栈弹出数据，执行计算，再把结果入操作数栈，操作数栈的深度在编译期已经决定，在方法的 Code 属性的 max\_stacks 数据项中
* 方法出口\(方法返回地址：Return Address\)：返回地址（Return Address），正常返回时PC计数器的值作为返回地址保存；异常返回时通过异常处理表获得返回地址，栈帧一般不会保存这部分信息
* 额外附加信息

#### 动态链接

**动态链接：**一个指向运行时常量池中该栈帧所属方法的引用，包含这个引用的目的就是为了支持当前方法的代码能够实现动态链接

#### returnAddress

![](/assets/20170807090817.png)

#### Exception

* StackOverflowError：如果线程请求的栈深度大于虚拟机所允许的深度，抛出StackOverflowError异常；
* OutOfMemoryError：如果虚拟机栈动态扩展时无法申请到足够的内存，抛出OutOfMemoryError异常；



