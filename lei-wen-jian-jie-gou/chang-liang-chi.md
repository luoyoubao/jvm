### 常量池

**常量池**可以理解为Class文件的资源仓库；常量池是class文件中非常重要的结构，它描述着整个class文件的字面量信息。 常量池是由一组constant\_pool结构体数组组成的，而数组的大小则由常量池计数器指定。常量池计数器constant\_pool\_count 的值 =constant\_pool表中的成员数+ 1。constant\_pool表的索引值只有在大于 0 且小于constant\_pool\_count时才会被认为是有效的。

#### 特性

* Class文件结构中与其他项目关联最多的数据类型
* Class文件空间最大的数据项目之一
* Class文件中第一个出现的表类型数据项目
* 常量池入口u2类型数据表示常量池容量计数值\(constant\_pool\_count\)，从1开始
* 常量池的第0项常量空出来用于表示"不引用任何一个常量池项目"
* 常量池中的每一项常量都是一个表

#### 常量池计数器\(constant\_pool\_count\)

常量池是class文件中非常重要的结构，它描述着整个class文件的字面量信息。 常量池是由一组constant\_pool结构体数组组成的，而数组的大小则由常量池计数器指定。常量池计数器constant\_pool\_count 的值 =constant\_pool表中的成员数+ 1。constant\_pool表的索引值只有在大于 0 且小于constant\_pool\_count时才会被认为是有效的

#### 常量池数据区\(constant\_pool\[contstant\_pool\_count-1\]\)

常量池，constant\_pool是一种表结构,它包含 Class 文件结构及其子结构中引用的所有字符串常量、 类或接口名、字段名和其它常量。 常量池中的每一项都具备相同的格式特征——第一个字节作为类型标记用于识别该项是哪种类型的常量，称为 “tag byte” 。常量池的索引范围是 1 至constant\_pool\_count−1

#### 常量池存储对象

**字面量\(Literal\)**  
**符号引用\(Symbolic References\)**

* 类和接口的全限定名\(Fully Qualified Name\)
* 字段的名称和描述符\(Descriptor\)
* 方法的名称和描述符

图示：

![](/assets/201708112310.png)



**JAVA标识符与CONSTANT\_Utf8\_info**  
![](/assets/201708030029.png)

