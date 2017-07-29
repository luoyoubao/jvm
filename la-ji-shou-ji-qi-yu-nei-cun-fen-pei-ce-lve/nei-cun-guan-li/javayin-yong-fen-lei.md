### JAVA引用分类 ###
+ 强引用：StrongReference
+ 软引用：SoftReference
+ 弱引用：WeakReference
+ 虚引用：PhantomReference

####StrongReference#
GC任何时候都不会回收StrongReference，哪怕内存不足时，系统会直接抛出异常OutOfMemoryError，也不会去回收，首先要说明的是java中默认就是强引用
```
Persion p = new Persion();
```