### AOT（Ahead-of-TimeCompilation\)

除了我们日常最常见的Java使用模式，其实还有一种新的编译方式，即所谓的AOT（Ahead-of-TimeCompilation\)，直接将字节码编译成机器码，这样就避免了JIT预热等各方面的开销；

OracleJDK9就引入了实验性的AOT特性，并且增加了新的jaotc工具。利用下面的命令把某个类或者某个模块编译成为AOT库。

```
jaotc--outputlibHelloWorld.soHelloWorld.class
jaotc--outputlibjava.base.so--modulejava.base
```

启动：

```
java -XX:AOTLibrary=./libHelloWorld.so,./libjava.base.so HelloWorld
```

OracleJDK支持分层编译和AOT协作使用，这两者并不是二选一的关系。如果你有兴趣，可以参考相关文档：[http://openjdk.java.net/jeps/295；](http://openjdk.java.net/jeps/295；AOT也不仅仅是只有这一种方式，业界早就有第三方工具（如GCJ、ExcelsiorExcelsiorJET）提供相关功能)

AOT也不仅仅是只有这一种方式，业界早就有第三方工具（如GCJ、ExcelsiorExcelsiorJET）提供相关功能

