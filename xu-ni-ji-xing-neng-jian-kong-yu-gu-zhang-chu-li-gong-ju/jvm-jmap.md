### jmap

```
jmap -histo 17592  ##查看JVM内存对象分布情况
```

### jmap -heap pid 查看目前堆情况

```
[xixicat@cloud01 ~]$ jmap -heap 22869
Attaching to process ID 22869, please wait...
Debugger attached successfully.
Server compiler detected.
JVM version is 23.21-b01
using thread-local object allocation.
Garbage-First (G1) GC with 4 thread(s)
Heap Configuration:
   MinHeapFreeRatio = 40
   MaxHeapFreeRatio = 70
   MaxHeapSize      = 5368709120 (5120.0MB)
   NewSize          = 1363144 (1.2999954223632812MB)
   MaxNewSize       = 17592186044415 MB
   OldSize          = 5452592 (5.1999969482421875MB)
   NewRatio         = 2
   SurvivorRatio    = 8
   PermSize         = 20971520 (20.0MB)
   MaxPermSize      = 268435456 (256.0MB)
   G1HeapRegionSize = 2097152 (2.0MB)
Heap Usage:
G1 Heap:
   regions  = 2560
   capacity = 5368709120 (5120.0MB)
   used     = 3826721792 (3649.4462890625MB)
   free     = 1541987328 (1470.5537109375MB)
   71.27824783325195% used
G1 Young Generation:
Eden Space:
   regions  = 1068
   capacity = 2808086528 (2678.0MB)
   used     = 2239758336 (2136.0MB)
   free     = 568328192 (542.0MB)
   79.76101568334578% used
Survivor Space:
   regions  = 29
   capacity = 60817408 (58.0MB)
   used     = 60817408 (58.0MB)
   free     = 0 (0.0MB)
   100.0% used
G1 Old Generation:
   regions  = 1000
   capacity = 2499805184 (2384.0MB)
   used     = 1524048896 (1453.4462890625MB)
   free     = 975756288 (930.5537109375MB)
   60.96670675597735% used
Perm Generation:
   capacity = 171966464 (164.0MB)
   used     = 170752872 (162.8426284790039MB)
   free     = 1213592 (1.1573715209960938MB)
   99.29428565792921% used
48213 interned Strings occupying 5246936 bytes.
```



