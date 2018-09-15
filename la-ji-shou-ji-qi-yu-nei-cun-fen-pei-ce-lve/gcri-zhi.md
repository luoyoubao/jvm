### GC日志

![](/assets/201708022158.png)  
**说明**

* "33.125":代表GC发生的时间\(从虚拟机启动以来经过的秒数\)
* "\[GC"/"\[Full GC":说明垃圾收集停顿类型\(Full表示GC发生时发生了Stop-The-World\)
* "\[DefNew"/"\[Tenured"/"\[Perm":表示GC发生的区域
* 3324K-&gt;152K\(3712K\):GC前该内存区域已使用容量-&gt;GC后该内存区域已使用容量\(该内存区域总容量\)
* 0.0031680 secs:表示GC所用时间\(单位秒\)

#### Minor GC和Full GC区别

![](/assets/201708022217.png)**YGC:Minor GC**

**FGC:Full GC**

#### GC日志分析工具

* GCHisto
* GCLogViewer
* HPjmeter
* GCViewer



