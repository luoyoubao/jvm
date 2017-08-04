###定义###
类加载器的主要任务就是根据一个类的全限定名读取类的二级制字节流到JVM，然后转换为一个与目标类对应的java.lang.Class对象实例

#### JVM类加载器类型 ####
- 引导类加载器(Bootstrap Classloader)
- 自定义类加载器(User Defined Classloader)

###知识点###
* JAVA虚拟机规范定义：所有派生于抽象类Classloader的类加载器都划分为自定义类加载器

