### 最常见的类加载器分类

* Bootstrap ClassLoader
* ExtClassLoader
* AppClassLoader
* User Defined Classloader\(自定义类加载器\)

#### Bootstrap ClassLoader

* 称为启动类加载器，主要是用于加载JDK核心类，包括JRE\_HOME\lib下的**rt.jar、resources.jar、charsets.jar**等，或者由"-Xbootclasspath"指定路径中的所有类型
* 启动类加载器由C++编写并嵌在JVM内部，加载器名称为Null

可通过如下程序获得该类加载器从哪些地方加载了相关的jar或class文件：

```
URL[] urls = sun.misc.Launcher.getBootstrapClassPath().getURLs();
for (int i = 0; i < urls.length; i++) {
    System.out.println(urls[i].toExternalForm());
}
output==>
file:/Library/Java/JavaVirtualMachines/jdk1.8.0_60.jdk/Contents/Home/jre/lib/resources.jar
file:/Library/Java/JavaVirtualMachines/jdk1.8.0_60.jdk/Contents/Home/jre/lib/rt.jar
file:/Library/Java/JavaVirtualMachines/jdk1.8.0_60.jdk/Contents/Home/jre/lib/sunrsasign.jar
file:/Library/Java/JavaVirtualMachines/jdk1.8.0_60.jdk/Contents/Home/jre/lib/jsse.jar
file:/Library/Java/JavaVirtualMachines/jdk1.8.0_60.jdk/Contents/Home/jre/lib/jce.jar
file:/Library/Java/JavaVirtualMachines/jdk1.8.0_60.jdk/Contents/Home/jre/lib/charsets.jar
file:/Library/Java/JavaVirtualMachines/jdk1.8.0_60.jdk/Contents/Home/jre/lib/jfr.jar
file:/Library/Java/JavaVirtualMachines/jdk1.8.0_60.jdk/Contents/Home/jre/classes
```

其实上述结果也是通过查找**sun.boot.class.path**这个系统属性所得知的。

```
System.out.println(System.getProperty("sun.boot.class.path"));
```

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



