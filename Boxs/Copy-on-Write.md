#java 

# 写时复制

**不可变对象的写操作往往都是使用 Copy-on-Write 方法解决的**，当然 Copy-on-Write 的应用领域并不局限于 Immutability 模式。

Java 里 String 这个类在实现 replace () 方法的时候，并没有更改原字符串里面 value[] 数组的内容，而是创建了一个新字符串，这种方法在解决不可变对象的修改问题时经常用到。

## Java 领域
- CopyOnWriteArrayList
- CopyOnWriteArraySet
通过 COW ，实现读无锁，由于无锁，将读操作的性能发挥到了极致。

## 操作系统领域
- Fork () 函数
![[Pasted image 20230303154243.png]]

- 文件系统
Btrfs (B-Tree File System)
Aufs (advanced multi-layered unification fileSystem)

## Docker 容器镜像的设计是 COW

## 最大应用领域函数式编程
![[Pasted image 20230303154505.png]]


# Java 提供了 CopyOnWriteArrayList，为什么没有提供 CopyOnWriteLinkedList 呢？
![[Pasted image 20230303155942.png]]
