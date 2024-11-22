## **Java并发**

**什么是线程和进程?线程与进程的关系,区别及优缺点？⭐⭐⭐⭐**

💡 提示：可以从从 JVM 角度说进程和线程之间的关系

**为什么要使用多线程呢? ⭐⭐⭐**

💡 提示：从计算机角度来说主要是为了充分利用多核 CPU 的能力，从项目角度来说主要是为了提升系统的性能。

**说说线程的生命周期和状态? ⭐⭐⭐⭐**

💡 提示： 6 种状态（NEW、RUNNABLE、BLOCKED、WAITING、TIME_WAITING、TERMINATED）。

🌈 拓展：在操作系统中层面线程有 READY 和 RUNNING 状态，而在 JVM 层面只能看到 RUNNABLE 状态。

**什么是线程死锁?如何避免死锁?如何预防和避免线程死锁? ⭐⭐⭐⭐**

💡 提示： 这里最好能够结合代码来聊，你要确保自己可以写出有死锁问题的代码。

🌈 拓展：项目中遇到死锁问题是比较常见的，除了要搞懂上面这些死锁的基本概念之外，你还要知道线上项目遇到死锁问题该如何排查和解决。

**synchronized 关键字 ⭐⭐⭐⭐⭐**

💡 提示：synchronized 关键字几乎是面试必问，你需要搞懂下面这些 synchronized 关键字相关的问题：

- synchronized 关键字的作用，自己是怎么使用的。
-  synchronized 关键字的底层原理（重点！！！）
-  JDK1.6 之后的 synchronized 关键字底层做了哪些优化。synchronized 锁升级流程。
-  synchronized 和 ReentrantLock 的区别。
-  synchronized 和 volatile 的区别。

**并发编程的三个重要特性 ⭐⭐⭐⭐⭐**

💡 提示： 原子性、可见性、有序性

**JMM（Java Memory Model，Java 内存模型）和 happens-before 原则。 ⭐⭐⭐⭐⭐**

**volatile 关键字 ⭐⭐⭐⭐⭐**

💡 提示：volatile 关键字同样是一个重点！结合 JMM（Java Memory Model，Java 内存模型）和 happens-before 原则来回答就行了。

**ThreadLocal 关键字 ⭐⭐⭐⭐⭐**

💡 提示：关注ThreadLocal的底层原理、内存泄露问题以及自己是如何在项目中使用ThreadLocal关键字的。

**线程池 ⭐⭐⭐⭐⭐**

💡 提示：线程池有哪几种，各种线程池的优缺点，线程池的重要参数、线程池的执行流程、线程池的饱和策略、如何设置线程池的大小等等。

**ReentrantLock 和 AQS ⭐⭐⭐⭐⭐**

💡 提示： ReentrantLock 的特性、实现原理（基于 AQS）。可以从 ReentrantLock 的实现来理解 AQS。

**乐观锁和悲观锁的区别 ⭐⭐⭐⭐⭐**

**CAS 了解么？原理？什么是 ABA 问题？ABA 问题怎么解决？ ⭐⭐⭐⭐⭐**

💡 提示：多地方都用到了 CAS 比如 ConcurrentHashMap 采用 CAS 和 synchronized 来保证并发安全，再比如java.util.concurrent.atomic包中的类通过 volatile+CAS 重试保证线程安全性。和面试官聊 CAS 的时候，你可以结合 CAS 的一些实际应用来说。

**Atomic 原子类 ⭐⭐**
