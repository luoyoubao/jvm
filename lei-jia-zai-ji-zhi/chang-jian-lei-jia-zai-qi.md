### 最常见的类加载器分类

* Bootstrap ClassLoader
* ExtClassLoader
* AppClassLoader
* User Defined Classloader\(自定义类加载器\)

#### Bootstrap ClassLoader

* 称为启动类加载器，主要是用于加载JDK核心类，包括JRE\_HOME\lib下的rt.jar等，或者由"-Xbootclasspath"指定路径中的所有类型
* 启动类加载器由C++编写并嵌在JVM内部，加载器名称为Null

#### ExtClassLoader

ExtClassLoader派生于ClassLoader\(Java语言编写\)，负责加载JAVA\_HOME/lib/ext目录下的类

#### SystemClassLoader

SystemClassLoader派生于ClassLoader\(Java语言编写\)，用于加载当前应用classpath下的所有类，也被称作AppClassLoader

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
output==>
null
sun.misc.Launcher$ExtClassLoader@eed1f14
sun.misc.Launcher$AppClassLoader
```



