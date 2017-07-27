#### 局部变量表 ####
定义：局部变量表存放编译期可知的基本数据类型、对象引用(reference类型，它不等同于对象本身，可能是一个指向对象起始地址的引用指针，也可能是指向代表对象的句柄或其他与此对象相关的位置)和returnAddress类型(指向一条字节码指令地址)

#### 特性 ####
+ 存放基本数据类型(boolean\byte\char\short\int\float\long\double)
+ 64位的long/double占用2个局部变量空间(Slot，变量槽)
+ 局部变量表所需的内存空间在编译器完成分配
+ 当进入一个方法时，该方法需要在帧中分配多大的局部变量空间是完全确定的，方法运行期间不会改变局部变量表的大小

#### Exception ####
+ StackOverflowError：如果线程请求的栈深度大于虚拟机所允许的深度，抛出StackOverflowError异常；
+ OutOfMemoryError：如果虚拟机栈动态扩展时无法申请到足够的内存，抛出OutOfMemoryError异常；