### 栈上分配

故名思议就是在栈上分配对象，其实目前Hotspot并没有实现真正意义上的栈上分配，实际上是标量替换。

```
private static int fn(int age) {
    User user = new User(age);
    int i = user.getAge();
    return i;
}
```



