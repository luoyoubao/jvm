###字段信息区###
包含两部分：
- 字段计数器(fields_count)
- 字段信息数据区(fields[fields_count])


####字段计数器(fields_count)####
字段计数器，fields_count的值表示当前 Class 文件 fields[]数组的成员个数。 fields[]数组中每一项都是一个field_info结构的数据项，它用于表示该类或接口声明的类字段或者实例字段

#### 字段信息数据区(fields[fields_count]) ####