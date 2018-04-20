### 最常见的类加载器分类

* Bootstrap ClassLoader
* ExtClassLoader
* AppClassLoader
* User Defined Classloader\(自定义类加载器\)

#### Bootstrap ClassLoader

* 称为启动类加载器，主要负责加载主要是用于加载JDK核心类，包括JRE\_HOME\lib下的rt.jar等，或者由"-Xbootclasspath"指定路径中的所有类型
* 启动类加载器由C++编写并嵌在JVM内部，加载器名称为Null

#### ExtClassLoader

ExtClassLoader派生于ClassLoader\(Java语言编写\)，负责加载"JAVA\_HOME/lib/ext"扩展目录中的所有类型

#### AppClassLoader

ExtClassLoader派生于ClassLoader\(Java语言编写\)，负责加载ClassPath目录中的所有类型

```
package com.quancheng.jvm;

public class Appliction {

    public static void main(String[] args) {
        ClassLoader bootstrap = System.class.getClassLoader();
        System.err.println(null != bootstrap ? bootstrap.getClass().getName() : null);

        ClassLoader ext = sun.security.ec.SunEC.class.getClassLoader();
        System.err.println(ext);

        ClassLoader app = Appliction.class.getClassLoader();
        System.err.println(app.getClass().getName());
    }
}
```



