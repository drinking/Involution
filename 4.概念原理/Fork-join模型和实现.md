在并行计算中，fork–join模型是设置和执行并行程序的一种方式，使得程序在指定一点上“分叉”（fork）而开始并行执行，在随后的一点上“合并”（join）并恢复顺序执行。并行区块可以递归的fork，直到达到特定的任务粒度（granularity）。Fork–join可以被视为是一种并行设计模式.

### 参考资料
- https://zh.wikipedia.org/wiki/Fork-join%E6%A8%A1%E5%9E%8B