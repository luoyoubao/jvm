### 多层编译

多层编译是指在-server的模式下采用如下方式进行编译：

* 解释器不再收集运行状况信息，只用于启动并触发C1编译；

* C1编译后生成带收集运行信息的代码；

* C2编译基于C1编译后代码收集的运行信息来进行激进优化，当激进优化的假设不成立时，再退回使用C1编译的代码；

![](/assets/20180404151034001.png)


