#input 

# Java 线程的生命周期
![[Pasted image 20230302160255.png]]

其实在操作系统层面，Java 线程中的 BLOCKED、WAITING、TIMED_WAITING 是一种状态，即前面我们提到的休眠状态。也就是说只要 Java 线程处于这三种状态之一，那么这个线程就永远没有 CPU 的使用权。

1. RUNNABLE -> BLOCKED 
	1. 线程等待 synchronized 的隐式锁。
	2. 当等待线程获得锁后，BLOCKED ->RUNNABLE
![[Pasted image 20230302160808.png]]


2. RUNNABLE -> WAITING
![[Pasted image 20230302161247.png]]
3. RUNNABLE -> TIMED_WAITING
![[Pasted image 20230302161327.png]]


4. RUNNABLE -> TERMINATED
	1. Stop () 不建议使用
	2. Interrupt ()


![[Pasted image 20230302161703.png]]


## 观察线程状态的工具

### Jstack 命令或者 Java VisualVM

![[Pasted image 20230302161901.png]]






# 创建多少线程才算合适？

![[多线程#多线程的好处]]

![[多线程#线程数如何定呢？]] 


# 线程安全
[[线程安全]]
