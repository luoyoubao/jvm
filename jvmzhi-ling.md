| invokevirtual |
| :--- |


| invokevirtual | Invoke instance method; dispatch based on class | 执行一般实例方法，创建完实例对象后，obj.method\(\)调用的 |
| :--- | :--- | :--- |
| invokespecial | Invoke instance method; special handling for superclass, private, and instance initialization method invocations | 实例初始化方法（构造函数）、父类的方法（super.method\(\)方式调用）、私有方法 |
| invokeinterface | Invoke interface method | 执行接口方法 |
| invokestatic | Invoke a class \(static\) method | 执行静态方法 |
| invokedynamic | Invoke dynamic method | jdk1.7新增，执行动态方法，不需要在编译时确定 |



