### 对象头(Header)组成 ####
+ 存储对象自身的运行时数据
+ Java数组(记录数组长度以确定数组大小)
+ 类型指针(即对象指向它的类元数据的指针，虚拟机通过该指针确定该对象是那个类的实例)

####特性###
* Header长度必须是8字节的倍数
* 查找对象的元数据不一定要经过对象本身