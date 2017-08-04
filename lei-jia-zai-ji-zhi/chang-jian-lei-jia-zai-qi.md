### 最常见的类加载器分类 ###
* Bootstrap ClassLoader
* ExtClassLoader
* AppClassLoader

####Bootstrap ClassLoader####
称为启动类加载器，主要负责加载"JAVA_HOME/lib"目录下的所有类型，或者由"-Xbootclasspath"指定路径中的所有类型

#### ExtClassLoader ####
ExtClassLoader派生于ClassLoader(Java语言编写)，负责加载"JAVA_HOME/lib/ext"扩展目录中的所有类型