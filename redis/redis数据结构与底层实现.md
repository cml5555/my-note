## 常用数据结构

1. string

2. set

3. list

4. hash

5. ordered list

6. bitmap

7. hyperloglog

8. stream

   * 可以由stream实现消息队列

     * 其他的实现：发布订阅：不能持久化，list：不能多播

   * ```
     stream:
     	list
     	consumer gruop
     	last_deliver_id
     	pending列表：用来存储已经被读取但是为ack的消息
     ```

   * 

## 底层数据结构

1. ziplist
   	* 我们知道普通list的每个元素所占的长度是一样的，ziplist在每个元素都是一个entry，这个entry记录了数据，编码类型以及前一个entry的长度，这样就可以在一个列表里放置长度不同的元素了
2. sds
   1. O(1)复杂度读取长度
   2. 额外的buffer，减小内存分配的次数
3. quicklist
   1. 由很多个ziplist组成的链表，减小了指针占用的内存空间
4. hashtable
   1. 数组+链表
5. skiplist
   1. 跳表是一个拥有nlogn复杂度查询的数据结构，基于二分查找和链表
   2. redis对跳表的改善：
      1. 增加后退指针，方便后序遍历操作
      2. 每个节点都为一个hashEntry，由score排序
      3. 允许重复的score值

## 编码类型

* 可以简单的把编码类型理解成底层数据类型的抽象，当然，不同的编码类型可能会对应同一个底层的实现，比如字符串就有三种编码类型

## redis 对象

* redis里所有的元素都是一个redisObject

  ``` json
  redisObject{
  	type
  	encoding
  	lru
  	ptr
  }
  ```

* redis 对象类型的作用
  * 提供操作的类型检查
  * 多态

* 执行一条命令的流程，以lpush为例
  1. 首先通过key在库里寻找redisObject
  2. 根据type字段进行类型检查，看命令是否合法
  3. 根据encoding字段进行多态处理，双端列表还是ziplist？

