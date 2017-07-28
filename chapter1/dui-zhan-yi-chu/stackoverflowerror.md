如果线程请求的栈深度大于虚拟机允许的最大深度则抛出StackOverflowError异常

#####案例一:方法递归##
```
package com.quancheng.jvm.oom;

public class StackOverflowTest {

    private static int stackLength = 0;

    private static void println() {
        stackLength++;
        System.err.println("stack length==>" + stackLength);
        println();
    }

    public static void main(String[] args) {
        println();
    }
}
```

