
## MVCC (Multi Version Currency control)
详见《从根上理解MySQL》MVCC篇
https://juejin.cn/post/6855129007336521741




##  [InnoDB Locking](https://dev.mysql.com/doc/refman/8.0/en/innodb-locking.html)

#### 意向锁——表锁
> Intention locks are **table-level locks** that indicate which type of lock (shared or exclusive) a transaction requires later for a row in a table. There are two types of intention locks: An intention shared lock ( IS ) indicates that a transaction intends to set a shared lock on individual rows in a table.

对于需要获取表锁的事务时,能够快速判断该表内是否有互斥的锁.


#### 插入意向锁

插入意向锁的作用是为了提高并发插入的性能，多个事务同时写入不同数据至同一索引范围（区间）内，并不需要等待其他事务完成，不会发生锁等待。

插入意向锁本质上可以看成是一个Gap Lock：

-   普通的Gap Lock _不允许_ 在（上一条记录，本记录）范围内插入数据
-   插入意向锁Gap Lock _允许_ 在（上一条记录，本记录）范围内插入数据

所以，插入意向锁是`表级别`的。



### 参考资料
- [Innodb中的事务隔离级别和锁的关系](https://tech.meituan.com/2014/08/20/innodb-lock.html)