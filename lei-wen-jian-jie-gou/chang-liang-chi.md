### 常量池

**常量池**可以理解为Class文件的资源仓库

#### 特性

* Class文件结构中与其他项目关联最多的数据类型
* Class文件空间最大的数据项目之一
* Class文件中第一个出现的表类型数据项目
* 常量池入口u2类型数据表示常量池容量计数值\(constant\_pool\_count\)，从1开始
* 常量池的第0项常量空出来用于表示"不引用任何一个常量池项目"
* 常量池中的每一项常量都是一个表

#### 常量池存储对象

**字面量\(Literal\)**  
**符号引用\(Symbolic References\)**

* 类和接口的全限定名\(Fully Qualified Name\)
* 字段的名称和描述符\(Descriptor\)
* 方法的名称和描述符

**JAVA标识符与CONSTANT\_Utf8\_info**

![](/assets/201708030029.png)

