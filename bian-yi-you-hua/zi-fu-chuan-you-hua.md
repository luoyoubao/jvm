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



