### 去虚拟化

去虚拟化是指在装载class文件后，进行类层次分析，如果发现类中的方法只提供一个实现类，那么对于调用了此方法的代码，也可以进行方法内联，从而提升执行性能

### 逆优化

运行后C1/C2编译出来的机器码如果不符合优化条件，则会进行逆优化\(deoptimization\)，也就是回到解释执行的方式，例如基于类层次分析编译的代码，当有新的接口实现类加入时，就会执行逆优化；



