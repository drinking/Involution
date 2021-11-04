### ReentrantLock
有尝试机制的锁,避免等待

### ReadWriteLock
区分读写的锁,提高读写性能

### StampedLock
比ReadWirteLock更乐观锁,更乐观进行读操作,如果发现读后有写操作,则真正加读写互斥的锁.


### 参考资料
- https://www.liaoxuefeng.com/wiki/1252599548343744/1309138673991714