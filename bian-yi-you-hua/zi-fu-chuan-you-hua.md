### 编译器对字符串的优化

* String通过"+"拼接时如果拼接的对象是常量，则在编译期被合并优化；

  ```
  String st = "a" + "b" + "c"; // 或者final String s = "a";编译器认为它是不可变的常量会自动合并优化
  javap out==============>
  Code:
  stack=1, locals=2, args_size=1
  0: ldc           #19                 // String abc
  2: astore_1
  3: return
  ```

* Stirng通过"+"拼接的对象是变量，则编译器通过StringBuilder进行append

```
public static void main(String[] args){
    String name = "luoyobao";
    String sb = name + "hello";
}

javap -v AppTest.class==>
  public static void main(java.lang.String[]);
    descriptor: ([Ljava/lang/String;)V
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=2, locals=3, args_size=1
         0: ldc           #2                  // String luoyobao
         2: astore_1
         3: new           #3                  // class java/lang/StringBuilder
         6: dup
         7: invokespecial #4                  // Method java/lang/StringBuilder."<init>":()V
        10: aload_1
        11: invokevirtual #5                  // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
        14: ldc           #6                  // String hello
        16: invokevirtual #5                  // Method java/lang/StringBuilder.append:(Ljava/lang/String;)Ljava/lang/StringBuilder;
        19: invokevirtual #7                  // Method java/lang/StringBuilder.toString:()Ljava/lang/String;
        22: astore_2
        23: return
      LineNumberTable:
        line 5: 0
        line 6: 3
        line 7: 23
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0      24     0  args   [Ljava/lang/String;
            3      21     1  name   Ljava/lang/String;
           23       1     2    sb   Ljava/lang/String;
```



