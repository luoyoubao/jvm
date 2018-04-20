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



