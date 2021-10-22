
- 常见线程池模型
    - newCachedthreadPool
    - newFixedThreadPool
    - newSingleThreadExecutor
    - newSingleThreadScheduledExecutor
    - newSingleScheduledTreadPool
    - newWorkStealingPool
    
- Work-Stealing算法是什么?
    
    In parallel computing, work stealing is a scheduling strategy for multithreaded computer programs. It solves the problem of executing a dynamically multithreaded computation, one that can "spawn" new threads of execution, on a statically multithreaded computer, with a fixed number of processors (or cores). It does so efficiently in terms of execution time, memory usage, and inter-processor communication.
    
- Spring自动配置是配置什么?
    
    @Configuration配置类注解，由AnnotationConfigApplicationContext或AnnotationConfigWebApplicationContext在初始化扫描生成的实例，可包含@Bean注解的方法。
    
- 什么是一致性哈希?
    
    一致哈希 是一种特殊的哈希算法。在使用一致哈希算法后，哈希表槽位数的改变平均只需要对K/n 个关键字重新映射，其中 K是关键字的数量，n是槽位数量。然而在传统的哈希表中，添加或删除一个槽位的几乎需要对所有关键字进行重新映射。
    
    [https://segmentfault.com/a/1190000021199728](https://segmentfault.com/a/1190000021199728)
    
- 分布式唯一ID生成思路
    - UUID
    - 利用MySQL自增ID
    - 集中式ID生成器
    - Twitter Snowflake算法
    - [https://www.liaoxuefeng.com/article/1280526512029729](https://www.liaoxuefeng.com/article/1280526512029729)
    - [https://zhuanlan.zhihu.com/p/107939861](https://zhuanlan.zhihu.com/p/107939861)
    
- Redis 客户端 Jedis、lettuce 和 Redisson 对比
    [https://www.cnblogs.com/54chensongxia/p/13815761.html](https://www.cnblogs.com/54chensongxia/p/13815761.html)
    
- 偏向锁,轻量级锁,重量级锁
    
    区别主要在于加锁对CPU资源的消耗和线程的阻塞逐级递增.
    
    是锁等待的一种策略.
    
    [https://www.cnblogs.com/paddix/p/5405678.html](https://www.cnblogs.com/paddix/p/5405678.html)
    
- The FLP impossibility result for asynchronous deterministic consensus
    
    In a fully asynchronous message-passing distributed system, in which at least one process may have a crash failure, it has been proven in the famous FLP impossibility result that a deterministic algorithm for achieving consensus is impossible
    
    [https://en.wikipedia.org/wiki/Consensus_(computer_science)#The_FLP_impossibility_result_for_asynchronous_deterministic_consensus](https://en.wikipedia.org/wiki/Consensus_(computer_science)#The_FLP_impossibility_result_for_asynchronous_deterministic_consensus)
    
- 死锁的4个必要条件
    
    todo
    
- spring事务传播机制
    
    todo
    
- happens before规则
    
    todo