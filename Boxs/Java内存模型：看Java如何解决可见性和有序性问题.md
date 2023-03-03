#input 
## [[Java 内存模型（JMM）]]

# 可见性
指当一个线程修改了共享变量的值时，其他线程能够立即得知这个修改。

## Volatile (可见性)
一个声明 volatile 的变量，不能使用 cpu 缓存，新值能立即同步到主内存，以及每次使用前立即从主内存刷新。

## synchronized (可见性)
synchronized 包裹的代码段，只有一个线程能进入修改共享变量。其他线程进入后自然能得知这个修改。

## final (可见性)
被 final 修饰的字段在构造器中一旦被初始化完成，并且构造器没有把“this”引用逸出（this 引用逸出，其他线程有可能通过这个引用访问到初始化了一半的对象），那么其他线程就能看见 final 字段的值。

```java
//this 引用逸出
final int x;
// 错误的构造函数
public FinalFieldExample(){
	x = 3;
	y =4
	// this 逸出
	global.obj = this;
}
```

# 有序性
## Voiatile (有序性)
Voiatile 本身就包含了禁止指令重排序的语义。主要是通过内存屏障来实现。

## synchronized (有序性)

持有同一个锁的两个同步块只能串行地进入

# Happens-Before 规则

## Happens-Before 原则真正要表达的是：前面一个操作的结果对后续操作是【可见的】

Happens-Before 规则约束了编译器的优化行为，要求编译器优化后一定遵守 Happens-before 规则。
- Program Order Rule，程序次序规则：在一个线程中，按照程序的顺序，前面的操作 HB 后面的操作；
- Volatile Variable Rule, Volatile 变量规则：对于一个 volatile 变量的写操作 HB 后面（时间上的后面）对这个变量的读操作；
- Transitivity, 传递性：如果操作 A HB 操作 B, 操作 B HB 操作 C，那就可以得出操作 A HB 操作 C ；
- Monitor Lock Rule, 管程锁定规则：一个 unlock 操作 HB 后面（时间上的后面）对同一个锁的 lock 操作。
- Thread Start Rule, 线程启动规则：Thread 对象的 start ()方法 HB 此线程的每一个动作。
- Thread Termination Rule, 线程终止规则：线程中的所有操作都 HB 对此线程的终止检测，我们可以通过 Thread:: join ()方法是否结束，Thread:: iaAlive ()的返回值等手段检测线程是否已经终止；
- Thread Interruption Rule, 线程中断规则：对线程 interrupt () 方法的调用 HB 被中断线程的代码检测到中断事件的发生，可以通过 Thread:：interrupted () 方法检测到是否有中断发生。
- Finalizer Rule，对象终结规则：一个对象的初始化完成（构造函数执行结束） HB 它的 finalize () 方法的开始。
