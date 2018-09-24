```
jstack 31034 > ~/run/dump31034    ## dump java线程信息
grep Thread.State dump31034 | awk '{print $2$3$4$5}' | sort | uniq -c   ### 统计所有线程的状态
========>
8 RUNNABLE
1 TIMED_WAITING(onobjectmonitor)
2 WAITING(onobjectmonitor)
```



