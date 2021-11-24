
### 线程模型
![[Pasted image 20211110120351.png]]

![[Pasted image 20211118143526.png]]

### happens-before规则
happens-before规则非常重要，它是**判断**数据是否存在竞争、线程是否安全的主要依据。JSR-133S使用happens-before概念阐述了两个操作之间的内存可见性。在JMM中，如果一个操作的结果需要对另一个操作可见，那么这两个操作则存在happens-before关系。

1.  程序顺序规则：一个线程中的每一个操作，happens-before于该线程中的任意后续操作。
2.  [[监视器(monitor)]]规则：对一个锁的解锁，happens-before于随后对这个锁的加锁。
3.  volatile规则：对一个volatile变量的写，happens-before于任意后续对一个volatile变量的读。
4.  传递性：若果A happens-before B，B happens-before C，那么A happens-before C。
5.  线程启动规则：Thread对象的start()方法，happens-before于这个线程的任意后续操作。
6.  线程终止规则：线程中的任意操作，happens-before于该线程的终止监测。我们可以通过Thread.join()方法结束、Thread.isAlive()的返回值等手段检测到线程已经终止执行。
7.  线程中断操作：对线程interrupt()方法的调用，happens-before于被中断线程的代码检测到中断事件的发生，可以通过Thread.interrupted()方法检测到线程是否有中断发生。
8.  对象终结规则：一个对象的初始化完成，happens-before于这个对象的finalize()方法的开始。


### 内存屏障

> 内存屏障，也称内存栅栏，内存栅障，屏障指令等，是一类同步屏障指令，它使得CPU 或编译器在对内存进行操作的时候, 严格按照一定的顺序来执行, 也就是说在内存屏障之前的指令和之后的指令不会由于系统优化等原因而导致乱序。 大多数现代计算机为了提高性能而采取乱序执行，这使得内存屏障成为必须。--- wiki


**屏障两个作用:**
*1* 防止屏障两侧的指令重排
对于写屏障之前的代码不会重排到屏障之后,但代码之间可能会重排.
对于读屏障之后的代码不会重排到屏障之前,但代码之间可能会重排.
参考[Java Happens Before Guarantee](http://tutorials.jenkov.com/java-concurrency/java-happens-before-guarantee.html)

*2* load屏障强制从内存中读取,store强制写入内存


内存可见性问题，主要是高速缓存与内存的一致性问题。一个处理器上的线程修改了某数据，而在另一处理器上的线程可能仍然使用着该数据在专用cache中的老值，这就是可见性出了问题。解决办法是令该数据为volatile属性，或者读该数据之前执行内存屏障。

**volatile的屏障作用:**
> 在每个volatile写操作前插入StoreStore屏障，在写操作后插入StoreLoad屏障；  
> 在每个volatile读操作前插入LoadLoad屏障，在读操作后插入LoadStore屏障；

由于内存屏障的作用，避免了volatile变量和其它指令重排序、线程之间实现了通信，使得volatile表现出了锁的特性。

**final中存在的内存屏障:**
> 新建对象过程中，构造体中对final域的初始化写入和这个对象赋值给其他引用变量，这两个操作不能重排序；
> 初次读包含final域的对象引用和读取这个final域，这两个操作不能重排序；


### 参考资料
- [JVM符号引用和直接引用](https://juejin.cn/post/6844903785416884231)
- [TODO Read: Java内存模型（JMM）总结](https://zhuanlan.zhihu.com/p/29881777)
- [内存屏障](https://www.jianshu.com/p/2ab5e3d7e510)
- [final关键字的底层原理是什么？](https://cloud.tencent.com/developer/article/1379380)
- [volatile内存屏障及实现原理分析(JMM和MESI)](https://juejin.cn/post/6876395693854949389)
- [什么是重排序](https://tech.meituan.com/2014/09/23/java-memory-reordering.html)
- [happens-before规则解析](https://zhuanlan.zhihu.com/p/77157725)
- [Java内存访问重排序的研究](https://tech.meituan.com/2014/09/23/java-memory-reordering.html)]
- [Locks实现:背后不为人知的故事](https://www.hitzhangjie.pro/blog/2021-04-17-locks%E5%AE%9E%E7%8E%B0%E9%82%A3%E4%BA%9B%E4%B8%8D%E4%B8%BA%E4%BA%BA%E7%9F%A5%E7%9A%84%E6%95%85%E4%BA%8B/)
- [The JSR-133 Cookbook for Compiler Writers](http://gee.cs.oswego.edu/dl/jmm/cookbook.html)


@Override
	protected final void refreshBeanFactory() throws BeansException {
		if (hasBeanFactory()) {
			destroyBeans();
			closeBeanFactory();
		}
		try {
			DefaultListableBeanFactory beanFactory = createBeanFactory();
			beanFactory.setSerializationId(getId());
			customizeBeanFactory(beanFactory);
			loadBeanDefinitions(beanFactory);
			synchronized (this.beanFactoryMonitor) {
				this.beanFactory = beanFactory;
			}
		}
		catch (IOException ex) {
			throw new ApplicationContextException("I/O error parsing bean definition source for " + getDisplayName(), ex);
		}
	}
