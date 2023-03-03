java 程序占用内存的划分：
1. Java 堆
2. 方法区
3. 直接内存[^1]： 可通过 -XX:MaxDirectMemorySize 调整大小，内存不足时抛出OutOf-MemoryError 或者 OutOfMemorryError： Direct buffer memory
4. 线程堆栈：可通过-Xss 调整大小，内存不足时抛出 StackOverflowError（请求栈深度大于虚拟机所允许的深度）或者OutOfMemoryError （如果 Java 虚拟机栈容量可以动态扩展，当栈扩展时无法申请到足够的内存）
5. Socket 缓存区：每个Socket连接都 Receive 和 Send 两个缓存区，分别占大约 37kb 和 25kb 内存，连接多的话这块内存占用也比较可观。如果无法分配，可能会抛出 IOException: Too many open files 异常。
6. JNI代码： 如果代码中使用了 JNI 调用本地库，那本地库使用的内存也不再堆中，而是占用Java 虚拟机的贝蒂方法栈本地内存的。
7. 虚拟机和垃圾收集器： 虚拟机和垃圾收集器的工作也是要消耗一定数量的内存的。

[^1]: 直接内存 ：java.nio.DirectByteBuff. 只能等待老年代满后，Full GC 出现后，“顺便”帮它清理掉内存的废弃对象。否则就不得不一直等到抛出内存溢出异常时，先捕获到异常，再在Catch块里面通过System.gc()命令来触发垃圾收集。但如果Java虚拟机再打开了-XX：+DisableExplicitGC开关，禁止了人工触发垃圾收集的话，那就只能眼睁睁看着堆中还有许多空闲内存，自己却不得不抛出内存溢出异常了