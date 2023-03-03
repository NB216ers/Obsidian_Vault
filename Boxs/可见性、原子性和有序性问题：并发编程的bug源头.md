#input

## 并发编程的核心矛盾
CPU、内存、I/O 设备三者的速度差异。三者速度关系：CPU >> 内存 >> I/O, 根据木桶理论，程序整体的性能取决于最慢的操作（I/O），单方面提高 CPU 性能是无效的。

为了合理利用 CPU 的高性能，平衡这三者的速度差异，计算机体系机构、操作系统和编译程序都做出了贡献，主要体现为：
1. CPU 增加了缓存，很好的平衡了与内存的速度差异。
2. 操作系统增加了进程、线程，以分时复用 CPU，进而均衡 CPU 和 I/O 设备的速度差异；[[多线程#多线程的好处]]
3. 编译程序优化指令执行次序，使得缓存能够得到更加合理地利用。

## 并发编程 BUG 源头
### CPU 缓存导致可见性问题

可见性：一个线程对共享变量的修改，另外一个线程能够立刻看到。

多核时代，每颗 CPU 都有自己的缓存，这为计算机系统带来了更高的复杂度，它也引入了一个新问题：缓存一致性（Cache Coherence）

### 切换线程带来的原子性问题

[[原子性]]



### 编译优化带来的有序性问题

有序性指的是程序按照代码的先后顺序执行。

编译器为了优化性能，在不影响程序的最终结果，会调整语句的顺序。Java 领域中有一个双重检查创建单例对象的经典案例：

```java
// 
public class Singleton{
	static Singleton instance;
	static Singleton getInstance(){
		if(instance == null){
			synchronized(Singleton.class){
				if(instance == null){
					instance = new Singleton();
				}
			}
		}
	}
}

```

new Singleton ()，我们认为应该是：
1. 分配一块内存 M
2. 在内存 M 上初始化 Singleton 变量
3. 然后 M 的地址赋值给 instance 变量

但实际上经过重排序之后：
1. 分配一块内存 M
2. 将 M 的地址赋值给 instance 变量
3. 在内存 M 上初始化 Singleton 变量

当线程 A 进入第二个判空条件，将 M 地址赋值给 instance 变量时，发生了时间片切换，即使没有释放锁，线程 B 刚要进入第一个判空条件时，发现条件不成立，直接返回了 instance 引用，此时 instance 还未初始化，只是一块内存。

如果对 instance 进行 Volatile 语义声明，就可以禁止指令重排序，避免该情况发生。