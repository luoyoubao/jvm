### Jstat

查看内存使用情况：

```
jstat -gcutil pid
```

示例：

```
jstat -gcutil 38141

  S0     S1     E      O      M     CCS    YGC     YGCT    FGC    FGCT     GCT
 69.31   0.00  32.37  45.65  97.67  95.47     20    0.160     2    0.169    0.329
```

* S0:Survivor 0区的空间使用率
* S1: Survivor 1区的空间使用率
* E: Eden区的空间使用率
* O: 老年代的空间使用率
* M: 元数据的空间使用率
* CCS: 类指针压缩空间使用率
* YGC: 新生代GC次数
* YGCT: 新生代GC总时长
* FGC: Full GC次数
* FGCT: Full GC总时长
* GCT: 总共的GC时长



