Java 内存模型规范了 JVM 如何按需禁用缓存和编译优化的方法。

Happens-Before: 前一个操作的结果对后续操作是可见的。

Happens-Before 约束了编译器的优化行为，虽然允许编译器优化，但是优化后一定要遵守 Happens-Before 规则。

对一个 volatile 变量的写操作，Happens-Before 后续对这个变量的读操作。

如果 A Happens-Before B，B Happens-Before C ，那么 A Happens-Before C 。

对一个锁的解锁 Happens-Before 后续对这个锁的加锁。

线程 A 启动子线程 B 后，子线程 B 能够看到主线程在启动子线程 B 前的操作。

指主线程 A 等待子线程 B 完成（主线程 A 通过调用子线程 B 的 join() 方法实现），当子线程 B 完成后（主线程 A 中 join() 方法返回），主线程能够看到子线程的操作。当然所谓的“看到”，指的是对共享变量的操作。