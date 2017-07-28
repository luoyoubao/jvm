###案例一:递归方法##
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
output(jvm默认参数)============================================
stack length==>6745
stack length==>6746Exception in thread "main" java.lang.StackOverflowError
	at sun.nio.cs.UTF_8$Encoder.encodeLoop(UTF_8.java:691)
	at java.nio.charset.CharsetEncoder.encode(CharsetEncoder.java:579)
	at sun.nio.cs.StreamEncoder.implWrite(StreamEncoder.java:271)
	at sun.nio.cs.StreamEncoder.write(StreamEncoder.java:125)
	at java.io.OutputStreamWriter.write(OutputStreamWriter.java:207)
	at java.io.BufferedWriter.flushBuffer(BufferedWriter.java:129)
	at java.io.PrintStream.write(PrintStream.java:526)
	at java.io.PrintStream.print(PrintStream.java:669)
	at java.io.PrintStream.println(PrintStream.java:806)
	at com.quancheng.jvm.oom.StackOverflowTest.println(StackOverflowTest.java:9)
	at com.quancheng.jvm.oom.StackOverflowTest.println(StackOverflowTest.java:10)
	
output(-Xss200k)============================================

```

