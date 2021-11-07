1. 阻塞
2. 非阻塞
3. 多路复用
4. 信号驱动
5. 异步


Tomcat的NioEndPoint组件流程
![[Pasted image 20211107141316.png]]

select多路复用的流程
![[Pasted image 20211107141531.png]]

## 多路复用实现方案比较

### epoll相比select的优点

-   解决select三个缺点
    -   **对于第一个缺点**：epoll的解决方案在epoll_ctl函数中。每次注册新的事件到epoll句柄中时（在epoll_ctl中指定EPOLL_CTL_ADD），会把所有的fd拷贝进内核，而不是在epoll_wait的时候重复拷贝。epoll保证了每个fd在整个过程中只会拷贝一次(epoll_wait不需要复制)
    -   **对于第二个缺点**：epoll为每个fd指定一个回调函数，当设备就绪，唤醒等待队列上的等待者时，就会调用这个回调函数，而这个回调函数会把就绪的fd加入一个就绪链表。epoll_wait的工作实际上就是在这个就绪链表中查看有没有就绪的fd(不需要遍历)
    -   **对于第三个缺点**：epoll没有这个限制，它所支持的FD上限是最大可以打开文件的数目，这个数字一般远大于2048，举个例子，在1GB内存的机器上大约是10万左右，一般来说这个数目和系统内存关系很大
-   epoll的高性能
    -   epoll使用了红黑树来保存需要监听的文件描述符事件，epoll_ctl增删改操作快速
    -   epoll不需要遍历就能获取就绪fd，直接返回就绪链表即可
    -   linux2.6 之后使用了mmap技术，数据不在需要从内核复制到用户空间，零拷贝


### epoll的两种触发模式

 epoll有EPOLLLT和EPOLLET两种触发模式，LT是默认的模式，ET是“高速”模式（只支持no-block socket）
 -   LT（水平触发）模式下，只要这个文件描述符还有数据可读，**每次epoll_wait都会触发它的读事件**
 -   ET（边缘触发）模式下，检测到有I/O事件时，通过 epoll_wait 调用会得到有事件通知的文件描述符，对于文件描述符，如可读，则必须将该文件描述符一直读到空（或者返回EWOULDBLOCK），**否则下次的epoll_wait不会触发该事件**

- [见识一下linux高性能网络IO+Reactor模型](https://juejin.cn/post/6892687008552976398#heading-17)
- [【IO】IO设计模式：TPR模式，Reactor模式、Proactor模式_A minor-程序员宅基地](https://www.cxyzjd.com/article/weixin_43935927/111824093)
- [深入拆解Tomcat&Jetty(十一)](https://juejin.cn/post/6844903708979904526)
- [深度解读Tomcat中的NIO模型](https://www.jianshu.com/p/76ff17bc6dea)
- [[彻底学会使用epoll(一)——ET模式实现分析](http://blog.chinaunix.net/uid-28541347-id-4273856.html)](http://blog.chinaunix.net/uid-28541347-id-4273856.html)
- [ [Linux下的I/O复用与epoll详解](https://www.cnblogs.com/lojunren/p/3856290.html)](https://www.cnblogs.com/lojunren/p/3856290.html)
- [epoll manual page](https://man7.org/linux/man-pages/man7/epoll.7.html)
- [Epoll 实现原理](https://github.com/liexusong/linux-source-code-analyze/blob/master/epoll-principle.md)