### 实例数据

存储对象有效信息，即程序代码中定义的各种类型的字段内容，无论是从父类继承下来的还是在子类中定义的，都需要记录

#### 特性

* 存储顺序受虚拟机分配策略参数\(FieldsAllocationStyle\)和字段在JAVA源码中定义的顺序的影响
* HotSpot默认的分配策略、longs/doubles、ints、shorts/chars、bytes/booleans、oops\(Ordinary Object Pointers\)，相同宽度的字段总是被分配到一起
* 满足条件二的情况下，父类中定义的变量在子类之前
* CompactFields=true，子类较窄的变量也可能插入到父类变量的空隙中



