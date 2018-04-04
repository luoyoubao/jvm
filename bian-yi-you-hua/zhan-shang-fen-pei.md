### 栈上分配

故名思议就是在栈上分配对象，其实目前Hotspot并没有实现真正意义上的栈上分配，实际上是标量替换。

```
private static int fn(int age) {
    User user = new User(age);
    int i = user.getAge();
    return i;
}
```

User对象的作用域局限在方法fn中，可以使用标量替换的优化手段在栈上分配对象的成员变量，这样就不会生成User对象，大大减轻GC的压力，下面通过例子看看逃逸分析的影响。

```
public class JVM {
    public static void main(String[] args) throws Exception {
        int sum = 0;
        int count = 1000000;
        //warm up
        for (int i = 0; i < count ; i++) {
            sum += fn(i);
        }

        Thread.sleep(500);

        for (int i = 0; i < count ; i++) {
            sum += fn(i);
        }

        System.out.println(sum);
        System.in.read();
    }

    private static int fn(int age) {
        User user = new User(age);
        int i = user.getAge();
        return i;
    }
}

class User {
    private final int age;

    public User(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }
}

作者：占小狼
链接：https://www.jianshu.com/p/20bd2e9b1f03
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```



