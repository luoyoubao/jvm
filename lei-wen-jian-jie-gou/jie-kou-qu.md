###接口区###
包含两部分：
- 接口计数器(interfaces_count)
- 接口信息数据区(interfaces[interfaces_count])

####接口计数器 ####
接口计数器，interfaces_count的值表示当前类或接口的直接父接口数量

#### 接口信息数据区 ####
接口表，interfaces[]数组中的每个成员的值必须是一个对constant_pool表中项目的一个有效索引值， 它的长度为 interfaces_count。每个成员 interfaces[i]  必须为 CONSTANT_Class_info类型常量，其中 0 ≤ i <interfaces_count。在interfaces[]数组中，成员所表示的接口顺序和对应的源代码中给定的接口顺序（从左至右）一样，即interfaces[0]对应的是源代码中最左边的接口
