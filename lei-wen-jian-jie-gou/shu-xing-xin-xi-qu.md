### 属性集合 ###
包含两部分：
- 属性计数器(attributes_count)
- 属性信息数据区(attributes[attributes_count])


#### 属性计数器(attributes_count) ####
属性计数器，attributes_count的值表示当前 Class 文件attributes表的成员个数。attributes表中每一项都是一个attribute_info 结构的数据项

#### 属性信息数据区 ####
属性表，attributes 表的每个项的值必须是attribute_info结构