### AOT（Ahead-of-TimeCompilation\)

除了我们日常最常见的Java使用模式，其实还有一种新的编译方式，即所谓的AOT（Ahead-of-TimeCompilation\)，直接将字节码编译成机器码，这样就避免了JIT预热等各方面的开销；

OracleJDK9就引入了实验性的AOT特性，并且增加了新的jaotc工具。利用下面的命令把某个类或者某个模块编译成为AOT库。

```
jaotc--outputlibHelloWorld.soHelloWorld.class
jaotc--outputlibjava.base.so--modulejava.base
```



