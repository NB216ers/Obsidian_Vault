## 1. 阻塞与同步
[对于IO同步和阻塞，好像很多人不理解？_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1XW4y1K7aZ/?spm_id_from=333.337.search-card.all.click&vd_source=f6f37c6b90a47159317abf5341571133)
视频从 IO 操作的两个部分，发起 IO 和实际的 IO 读写，来讲解了阻塞和同步。
发起 I/O 操作的一方如果不能去做其他事，要等，叫做阻塞。
实际的 I/O 读写，操作系统帮你完成，然后通知调用方，叫异步。


## [深度长文：从bio到nio到aio，再到响应式编程 (qq.com)](https://mp.weixin.qq.com/s?__biz=MzA4MTc4NTUxNQ==&mid=2650524542&idx=1&sn=dc32eef9e033be79ad122a2ccbe88c2b&chksm=8780ccbab0f745ac325f0ab4351e1e6cfab8ab986e983cdc77a4df73dc8a18ae59b5888cd81b&scene=178&cur_album_id=1338361705327394818#rd)
1. Java 的 NIO，在 Linux 上底层是使用 epoll 实现的。epoll 是一个高性能的多路复用 I/O 工具，改进了 select 和 poll 等工具的一些功能。
> epoll 的数据结构是直接在内核上进行支持的。通过 epoll_create 和 epoll_ctl 等函数的操作，可以构造描述符（fd）相关的事件组合（event）
>-   `fd` 每条连接、每个文件，都对应着一个描述符，比如端口号。内核在定位到这些连接的时候，就是通过 fd 进行寻址的
>- -   `event` 当 fd 对应的资源，有状态或者数据变动，就会更新 `epoll_item` 结构。在没有事件变更的时候，epoll 就阻塞等待，也不会占用系统资源；一旦有新的事件到来，epoll 就会被激活，将事件通知到应用方

2. 相对于 select，epoll 有哪些改进？
>  1. epoll 不再需要像 select 一样对 fd 集合进行轮询，也不需要在调用时将 fd 集合在用户态和内核态进行交换
>  2. 应用程序获得就绪 fd 的事件复杂度，epoll 时 O (1)，select 是 O (n)
>  3. select 最大支持约 1024 个 fd，epoll 支持 65535 个
>  4. select 使用轮询模式检测就绪事件，epoll 采用通知方式，更加高效


## 2. 进程和线程的关系？
[操作系统-清华_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1uW411f72n/?p=50&spm_id_from=333.788.top_right_bar_window_history.content.click&vd_source=f6f37c6b90a47159317abf5341571133)
第 7 章详细阐述了进程的定义、组成、特点、控制结构、生命周期、状态变化模型和挂起等内容。线程相关内容，比如什么是线程？线程的实现，上下文切换等。
## 3. JVM 线程和通用操作系统线程状态
[在阻塞式io中，如果一个线程在等待io操作，那么cpu还会分配时间片给该线程吗？ - Boblim - 博客园 (cnblogs.com)](https://www.cnblogs.com/fnlingnzb-learner/p/15090360.html)
![[Pasted image 20230214093907.png]]
### 线程状态分析
1.可运行（就绪）：线程被创建之后，调用 Start（）函数就到了这个状态。

2.运行：Start（）函数之后，CPU 切换到了这个线程开始执行里面的 Run 方法就称为运行状态。

3.阻塞：阻塞状态是指线程因为某种原因放弃了 cpu 执行权，暂时停止运行。直到线程进入可运行 (runnable) 状态，才有机会再次获得 cpu 执行权转到运行 (running) 状态。阻塞的情况分三种。

(一). 等待阻塞：运行 (running) 的线程执行o.wait () 方法，JVM 会把该线程放入等待队列 (waitting queue) 中。

(二). 同步阻塞：运行 (running) 的线程在获取对象的同步锁时，若该同步锁被别的线程占用，则 JVM 会把该线程放入锁池 (lock pool) 中。

(三). 其他阻塞：运行 (running) 的线程执行 Thread. sleep (long ms) 或t.join () 方法，或者发出了 I/O 请求时，JVM 会把该线程置为阻塞状态。当 sleep () 状态超时、join () 等待线程终止或者超时、或者 I/O 处理完毕时，线程重新转入可运行 (runnable) 状态。

4.结束

线程 run ()、main () 方法执行结束，或者因异常退出了 run () 方法，则该线程结束生命周期。死亡的线程不可再次复生。

- seelp（）和 wait () 的区别
	- sleep（）和 wait () 这两个函数被调用之后线程都应该放弃执行权，不同的是 sleep（）不释放锁而 wait（）的话是释放锁。直白的意思是一个线程调用 Sleep（）之后进入了阻塞状态中的其他阻塞，它的意思就是当 sleep () 状态超时、join () 等待线程终止或者超时，线程重新转入可运行 (runnable) 状态。而 Wait（）是不同的在释放执行权之后 wait 也把锁释放了进入了线程等待阻塞，它要运行的话还是要和其他的线程去竞争锁，之后才可以获得执行权



[notify()是随机唤醒线程么? )](https://www.jianshu.com/p/99f73827c616)

## AQS
[初识Lock与AbstractQueuedSynchronizer(AQS) - 掘金 (juejin.cn)](https://juejin.cn/post/6844903601534418958)
- 同步器和锁的关系？锁和同步器很好的隔离了使用者和实现者所需关注的领域,**锁是面向使用者，它定义了使用者与锁交互的接口，隐藏了实现细节；同步器是面向锁的实现者，它简化了锁的实现方式，屏蔽了同步状态的管理，线程的排队，等待和唤醒等底层操作**。
- JUC 整体结构；底层基座，**Volatile 变量**、**CAS**。中层，**AQS**、**非阻塞数据结构**和**原子变量类**。上层，Lock、阻塞队列、Executor 和并发容器。[JUC的整体结构_六公里路的博客-CSDN博客](https://blog.csdn.net/weixin_38394991/article/details/105023356)


[深入理解AbstractQueuedSynchronizer(AQS) - 掘金 (juejin.cn)](https://juejin.cn/post/6844903601538596877)
比较通俗的语言讲解了 AQS 独占锁和共享锁主要方法。


[从ReentrantLock的实现看AQS的原理及应用 - 美团技术团队 (meituan.com)](https://tech.meituan.com/2019/12/05/aqs-theory-and-apply.html)
这篇文章更全面的介绍了AQS 