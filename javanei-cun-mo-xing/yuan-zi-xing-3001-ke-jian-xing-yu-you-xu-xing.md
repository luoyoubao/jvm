##### 原子性（Atomicity）

由Java内存模型来直接保证的原子性变量操作包括read、load、assign、use、store和write这六个， 我们大致可以认为，基本数据类型的访问、读写都是具备原子性的（例外就是long和double的非原子性 协定，读者只要知道这件事情就可以了，无须太过在意这些几乎不会发生的例外情况）。

如果应用场景需要一个更大范围的原子性保证（经常会遇到），Java内存模型还提供了lock和 unlock操作来满足这种需求，尽管虚拟机未把lock和unlock操作直接开放给用户使用，但是却提供了更 高层次的字节码指令monitorenter和monitorexit来隐式地使用这两个操作。这两个字节码指令反映到Java 代码中就是同步块——synchronized关键字，因此在synchronized块之间的操作也具备原子性

可见性（Visibility）

