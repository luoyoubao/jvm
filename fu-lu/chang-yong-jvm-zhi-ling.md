### 常用JVM指令
|指令|助记符|指令描述|
|:--:|:--:|:--:|
|0xac|ireturn|从当前方法返回int(当返回值是boolean/byte/char/short/int类型时使用)|
|0xad|lreturn|从当前方法返回long|
|0xac|freturn|从当前方法返回float|
|0xaf|dreturn|从当前方法返回double|
|0xb0|areturn|从当前方法返回对象引用|
|0xb1|return|从当前方法返回void(声明为void的方法、实例初始化方法、类和接口的初始化方法使用)|
|0xbb|new|创建一个对象，并将其引用值压入栈顶|
|0xbc|newarray|创建一个指定原始类型(如int/float/char)的数组，并将其引用值压入栈顶|
|0xbf|athrow|将栈顶的异常抛出|
|0xc2|monitorenter|获取对象的监视锁，用于同步方法或同步块|



