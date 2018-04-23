## OSR编译 {#articleHeader10}

除了C1、C2外，还有OSR（On Stack Replace）编译，只替换循环代码体的入口，C1、C2替换的是方法调用的入口。因此OSR编译后会出现的现象是方法的整段代码被编译了，但是只有循环体部分才执行编译后的机器码，其他部分仍是解释执行。

当机器配置CPU超过2核且内存超过2G，默认为server模式，32位的windows始终选择的是client模式。

  


