### jstat

jstat:一个极强的监视VM内存工具。可以用来监视VM内存内的各种堆和非堆的大小及其内存使用量

* jstat -class pid:显示加载class的数量，及所占空间等信息。
* jstat -compiler pid:显示VM实时编译的数量等信息。
* jstat -gc pid:可以显示gc的信息，查看gc的次数，及时间。
* jstat -gcnew pid: new对象的信息。
* jstat -gcnewcapacity pid: new对象的信息及其占用量。
* jstat -gcold pid: old对象的信息。
* jstat -gcoldcapacity pid: old对象的信息及其占用量。
* jstat -gcpermcapacity pid: perm对象的信息及其占用量。
* jstat -util pid:统计gc信息统计。
* jstat -printcompilation pid:当前VM执行的信息。
* jstat -gcutil pid 1000 10 : 1000ms统计一次gc情况统计10次；

**查看内存使用情况**：

```
jstat -gcutil pid
```

示例：

```
jstat -gcutil 38141

  S0     S1     E      O      M     CCS    YGC     YGCT    FGC    FGCT     GCT
 69.31   0.00  32.37  45.65  97.67  95.47     20    0.160     2    0.169    0.329
```

* S0：Survivor 0区的空间使用率
* S1：Survivor 1区的空间使用率
* E：Eden区的空间使用率
* O：老年代的空间使用率
* M：元数据的空间使用率
* CCS：类指针压缩空间使用率
* YGC：新生代GC次数
* YGCT：新生代GC总时长
* FGC：Full GC次数
* FGCT：Full GC总时长
* GCT：总共的GC时长



