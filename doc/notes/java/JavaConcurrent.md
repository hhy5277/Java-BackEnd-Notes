# TODO
* 多线程的通信，同步方式
* volatile和synchronized的区别
* 乐观锁与悲观锁?
* 乐观锁它是怎么实现的?
* 悲观锁呢?

# Java并发

## CAS
* CAS, CPU指令，在大多数处理器架构，包括IA32、Space中采用的都是CAS指令，CAS的语义是“我认为V的值应该为A，如果是，那么将V的值更新为B，否则不修改并告诉V的值实际为多少”，
* CAS是项乐观锁技术，当多个线程尝试使用CAS同时更新同一个变量时，只有其中一个线程能更新变量的值，而其它线程都失败，失败的线程并不会被挂起，而是被告知这次竞争中失败，并可以再次尝试。
* CAS有3个操作数，内存值V，旧的预期值A，要修改的新值B。当且仅当预期值A和内存值V相同时，将内存值V修改为B，否则什么都不做。

## synchronized 使用场景

线程具有五大状态:
* 新建状态：新建线程对象，并没有调用start()方法之前。
* 就绪状态：调用start()方法之后线程就进入就绪状态，但是并不是说只要调用start()方法线程就马上变为当前线程。
* 运行状态：线程被设置为当前线程，开始执行run()方法。就是线程进入运行状态
* 阻塞状态：线程被暂停，比如说调用sleep()方法后线程就进入阻塞状态
* 死亡状态：线程执行结束

![](http://www.blogjava.net/images/blogjava_net/santicom/360%E6%88%AA%E5%9B%BE20110901211600850.jpg)

锁类型:
* 可重入锁（synchronized和ReentrantLock）：在执行对象中所有同步方法不用再次获得锁
* 可中断锁（synchronized就不是可中断锁，而Lock是可中断锁）：在等待获取锁过程中可中断
* 公平锁（ReentrantLock和ReentrantReadWriteLock）： 按等待获取锁的线程的等待时间进行获取，等待时间长的具有优先获取锁权利
* 读写锁（ReadWriteLock和ReentrantReadWriteLock）：对资源读取和写入的时候拆分为2部分处理，读的时候可以多线程一起读，写的时候必须同步地写


Synchronized与Lock的区别

* synchronized关键字 Lock是接口
* Synchronized获取锁的线程执行完同步代码，释放锁，线程执行发生异常，jvm会让线程释放锁。Lock 在finally中必须释放锁，不然容易造成死锁。
* Synchronized无法判断锁状态，Lock可以判断。
* synchronized 少量同步，Lock可以提高线程进行读操作的效率（读写分离）

## 什么是线程不安全
非线程安全是指多线程操作同一个对象可能会出现问题。