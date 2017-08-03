### JAVA引用分类 ###
+ 强引用：StrongReference
+ 软引用：SoftReference
+ 弱引用：WeakReference
+ 虚引用：PhantomReference

### JVM引用类型 ###
+ 类类型(class type)
+ 数组类型(array type)
+ 接口类型(interface type)<br>
**<red>说明<red>**这些引用类型的值分别由类实例、数组实例以及实现了某个接口的派生类实例负责动态创建

####StrongReference#
GC任何时候都不会回收StrongReference，哪怕内存不足时，系统会直接抛出异常OutOfMemoryError，也不会去回收，首先要说明的是java中默认就是强引用
```
Persion p = new Persion();
```