### JIT

即时编译（Just-in-time Compilation，JIT）是一种通过在运行时将字节码翻译为机器码，从而改善字节码编译语言性能的技术。在HotSpot实现中有多种选择：C1、C2和C1+C2，分别对应client、server和分层编译。

1. C1编译速度快，优化方式比较保守；
2. C2编译速度慢，优化方式比较激进；
3. C1+C2在开始阶段采用C1编译，当代码运行到一定热度之后采用C2重新编译；

在1.8之前，分层编译默认是关闭的，可以添加-server -XX:+TieredCompilation参数进行开启；

### 编译阈值

即时编译JIT只在代码段执行足够次数才会进行优化，在执行过程中不断收集各种数据，作为优化的决策，所以在优化完成之前，例子中的User对象还是在堆上进行分配。

那么一段代码需要执行多少次才会触发JIT优化呢？通常这个值由-XX:CompileThreshold参数进行设置：

1. 使用client编译器时，默认为1500；
2. 使用server编译器时，默认为10000；

意味着如果方法调用次数或循环次数达到这个阈值就会触发标准编译，更改CompileThreshold标志的值，将使编译器提早（或延迟）编译。

除了标准编译，还有一个叫做OSR（On Stack Replacement）栈上替换的编译，如上述例子中的main方法，只执行一次，远远达不到阈值，但是方法体中执行了多次循环，OSR编译就是只编译该循环代码，然后将其替换，下次循环时就执行编译好的代码，不过触发OSR编译也需要一个阈值，可以通过以下公式得到。

```
-XX:CompileThreshold = 10000 
-XX:OnStackReplacePercentage = 140
-XX:InterpreterProfilePercentage = 33
OSR trigger = (CompileThreshold * (OnStackReplacePercentage - InterpreterProfilePercentage)) / 100 = 10700
```

其中trigger即为OSR编译的阈值

参考资料

[https://www.jianshu.com/p/20bd2e9b1f03](https://www.jianshu.com/p/20bd2e9b1f03)

http://www.infoq.com/cn/articles/OpenJDK-HotSpot-What-the-JIT

