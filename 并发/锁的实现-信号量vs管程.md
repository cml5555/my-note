## 信号量

* 由一个共享变量和一个同步队列组成

* P操作：请求资源

  > 将count-1，如果小于0则放到等待队列

* V操作：释放资源

* 实现多线程对资源的互斥访问

## 管程

* 对复杂的PV操作进行了封装

* 共享资源，等待队列，同步队列，以及访问共享变量的方法

  * java中的AQS也是类似于管程的实现
    * 等待队列，每一个condition都有一个等待队列，当调用await的时候，会放在等待队列里，调用signal时候会从等待队列中唤醒，去争抢锁，也就是tryAcquire方法

  

