
在读多写少的场景,变更CopyOnWriteArrayList都是在复制的新list上操作,不影响旧数据上既有的读取和迭代操作.当复制完成后取代旧list.读取之间不用加锁,只有在写操作时需要考虑并发场景.

### 参考资料
- https://www.jianshu.com/p/ceede734434b