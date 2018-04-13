在虚拟机层面，为了尽可能减少内存操作速度远慢于CPU运行速度所带来的CPU空置的影响，虚拟机会按照自己的一些规则将程序编写顺序打乱——即写在后面的代码在时间顺序上可能会先执行，而写在前面的代码会后执行——以尽可能充分地利用CPU

### 

**那些指令不能重排:Happen-Before规则**![](/assets/20170917225834.png)



参考资料

【happens-before俗解】http://ifeve.com/easy-happens-before/

