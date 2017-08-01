### 死亡标记(内存回收标记) ###
* F-Queue
* finalize()

#### 标记 ####
* finalize()方法是对象逃脱死亡命运的最后一次机会
* 如果对象要在finalize()中成功拯救自己，只要重新与引用链上的任何一个对象建立关联即可(如把this赋值给类变量或者对象的成员变量)
* 任何一个对象的finalize()方法都只会被系统自动调用一次