#### 本机直接内存溢出 ####
DirectMemory容量可通过-XX:MaxDirectMemorySize指定，如果不指定则默认与JAVA堆最大值(-Xmx)一样

#### DirectMemory溢出 ####
```
package com.quancheng.jvm.oom;

import java.lang.reflect.Field;

import sun.misc.Unsafe;

// -Xmx20M -XX:MaxDirectMemorySize=10M
public class DirectMemoryTest {

    public static void main(String[] args) throws IllegalArgumentException, IllegalAccessException {
        Field field = sun.misc.Unsafe.class.getDeclaredFields()[0];
        field.setAccessible(true);
        sun.misc.Unsafe unsafe = (Unsafe) field.get(null);
        while (true) {
            unsafe.allocateMemory(64 * 1024 * 1024);
        }
    }
}

output============================================

```