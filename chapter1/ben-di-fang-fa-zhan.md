### Native Method Stack\(本地方法栈\)

定义：本地方法栈为虚拟机使用到的Native方法服务，虚拟机规范未对本地方法栈中方法使用的语音、使用方式与数据结构进行强制规定，因此具体的虚拟机可以自由实现

特性

* 线程私有
* 后进先出(LIFO)栈
* 作用是支撑Native方法的调用、执行和退出
* 可能出现OutOfMemoryError异常和StackOverflowError异常
* 有一些虚拟机（如HotSpot）将Java虚拟机栈和本地方法栈合并实现

#### Exception

* StackOverflowError\(栈溢出\)
* OutOfMemoryError



