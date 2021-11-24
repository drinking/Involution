声明此处`hashCode`为Object对象的值,自定义的不算.(见Q&A第二部分)

一个对象的`hashCode`自打计算出来后便不可改变.计算部分参考[[HashMap的hash原理]].
如果`hashCode`因为对象内容的变更而频繁改变,就会造成在`HashMap`中,通过旧的`hashCode`计算出其的位置无法再被触及,get时缓存失效,put时放到新的位置,造成字典空间的浪费和冗余.
最后也有无法释放造成内存的泄漏的风险.

因为`hashCode`是存在对象头的`head word`里.
![[Pasted image 20211119183618.png]]
在对象使用`sychronized`锁时,会复用这段内存,覆盖`hashCode`.所以为了能够在解除锁后仍然能有相同的`hashCode`值,JVM考虑了将`hashCode`值保存起来,放在线程的栈中.事后再写回去.

对于最初无锁状态的`head word`,有价值的字段除了`hashCode`就是分代年龄,而失去分代年龄的后果应该远不不及`hashCode`影响大.所以这就是在优化锁性能的时候,也仍然保存这段空间拷贝和恢复的代码.不能舍弃.

综上时我从影响和数据结构对`hashCode`不可变的揣测,仅供参考.

### Q&A
1. 为什么Object的hashCode是native方法
> The methods are native **because they concern native data**. The hashCode method returns an integer value dependent on the internal representation of a pointer to an object on the heap. The getClass method must access the internal vtbl (virtual function table) that represents the compiled program's class hierarchy.
-  https://stackoverflow.com/questions/10578764/why-are-hashcode-and-getclass-native-methods/10579701

TODO: 考证哪里说加锁是获取hashCode会崩溃!

2. 为什么使用锁的过程中还能使用`hashCode`
-   当一个对象已经计算过identity hash code，它就无法进入偏向锁状态；      
-   当一个对象当前正处于偏向锁状态，并且需要计算其identity hash code的话，则它的偏向锁会被撤销，并且锁会膨胀为重量锁；
-   重量锁的实现中，ObjectMonitor类里有字段可以记录非加锁状态下的mark word，其中可以存储identity hash code的值。或者简单说就是重量锁可以存下identity hash code。

请一定要注意，这里讨论的hash code都只针对identity hash code。用户自定义的hashCode()方法所返回的值跟这里讨论的不是一回事。

Identity hash code是未被覆写的 java.lang.Object.hashCode() 或者 java.lang.System.identityHashCode(Object) 所返回的值。

