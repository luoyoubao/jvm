### 多层编译

Java7默认开启分层编译（tiered compilation）策略，由C1编译器和C2编译器相互协作共同来执行编译任务。C1编译器会对字节码进行简单和可靠的优化，以达到更快的编译速度；C2编译器会启动一些编译耗时更长的优化，以获取更好的编译质量。

（1）解释器不再收集运行状态信息，只用于启动并触发C1编译  
（2）C1编译后生成带收集运行信息的代码  
（3）C2编译，基于C1编译后代码收集的运行信息进行激进优化，当激进优化的假设不成立时，再退回使用C1编译的代码

程序在未编译期间解释执行有个阈值，SunJDK主要依据方法上的两个计数器是否超过阈值来判断：

* A、**调用计数器**，即方法被调用的次数，CompileThreshold，该值是指当方法被调用多少次后，就编译为机器码，client模式默认为1500次，server模式默认为1万次，可以在启动时添加-XX:CompileThreshold=10000来设置该值。

* B、**回边计数器**，即方法中循环执行部分代码的执行次数，OnStackReplacePercentage，该值用于/参与计算是否触发OSR编译的阈值，client默认为933，sever默认为140，可以通过-XX: OnStackReplacePercentage=140来设置。

client模式下的计算规则为CompileThreshold\*OnStackReplacePercentage/100，  
server模式下计算规则为CompileThreshold\*（OnStackReplacePercentage-InterpreterProfilePercentage）/100。InterpreterProfilePercentage，默认为33。

当方法上的回边计数器到达这个值时，触发后台的OSR编译，并将方法上累积的调用计数器设置为CompileThreshold 的值，同时将回边计数器设置为CompileThreshold/2的值。这样做一方面是为了避免OSR编译频繁被触发，另一方面是以便当方法被再次调用时即触发正常的编译，当累积的回边计数器的值再次达到该值时先检查OSR编译是否完成，如果已完成，则在执行循环体的代码时进入编译后的代码，如果未完成，继续把当前回边计数器的累计值再减掉一些，默认情况下，对于回边的情况，server模式下只要回边次数达到10700次（10000\*（140-33）），就会触发OSR编译。![](/assets/20180404151034001.png)

