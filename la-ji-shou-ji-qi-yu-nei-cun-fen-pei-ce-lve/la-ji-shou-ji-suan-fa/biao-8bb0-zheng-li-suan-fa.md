### 标记-整理算法(Mark-Compact) ###
**标记-整理(Mark-Compact):**算法不直接对可回收对象进行清理，而是让所有可用的对象都向一端移动。然后直接清理掉边界意外的内存