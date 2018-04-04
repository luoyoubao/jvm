### 方法内联

如果JVM监测到一些小方法被频繁的执行，它会把方法的调用替换成方法体本身

```
private int add4(int x1, int x2, int x3, int x4) {  
    return add2(x1, x2) + add2(x3, x4);  
}  

private int add2(int x1, int x2) {  
    return x1 + x2;  
}
```

JVM会把add2方法去掉，并把你的代码翻译成：

