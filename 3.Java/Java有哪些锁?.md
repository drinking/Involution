### ReentrantLock
1. 支持公平抢占和非公平抢占
2. 支持condition,通过await()和signal()来触发线程条件的等待.
3. 有尝试机制的锁,避免等待

关于condition生效逻辑
1. await()会释放当前所持有的锁.
2. siginal()需要等锁unlock()才算生效.
3. 多个condition都调用signal()时,依据FIFO的逻辑执行.

```java 

public static void tryLock() throws InterruptedException {  
  
    ReentrantLock lock = new ReentrantLock();  
    Condition condition = lock.newCondition();  
    Condition condition2 = lock.newCondition();  
  
    new Thread(()->{  
        lock.lock();  
        try {  
            System.out.println("1 wait");  
            condition.await();  
            System.out.println("1 after wait");  
        } catch (InterruptedException e) {  
            e.printStackTrace();  
        }  
        lock.unlock();  
        System.out.println("1 after lock");  
  
    }).start();  
  
    new Thread(()->{  
        lock.lock();  
        try {  
            System.out.println("3 wait");  
            condition2.await();  
            System.out.println("3 after wait");  
        } catch (InterruptedException e) {  
            e.printStackTrace();  
        }  
        lock.unlock();  
        System.out.println("3 after lock");  
  
    }).start();  
  
    new Thread(()->{  
        lock.lock();  
        System.out.println("2 before signal");  
        condition2.signal();  
        condition.signal();  
        System.out.println("2 signal");  
        try {  
            Thread.sleep(2000);  
        } catch (InterruptedException e) {  
            e.printStackTrace();  
        }  
  
        lock.unlock();  
        System.out.println("2 after lock");  
    }).start();  
  
    System.out.println("###sleep wait");  
    Thread.sleep(10000);  
  
  
}

```




### ReadWriteLock
区分读写的锁,提高读写性能

### StampedLock
比ReadWirteLock更乐观锁,更乐观进行读操作,如果发现读后有写操作,则真正加读写互斥的锁.


### 参考资料
- https://www.liaoxuefeng.com/wiki/1252599548343744/1309138673991714