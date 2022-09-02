# 什么是mvcc

* Mvcc是一种基于"数据版本"的并发控制手段，是一种无锁的并发控制，适用于innodb的RC和RR隔离级别，在快照读的时候会生成ReadView，根据readview从版本链（undo log）中就可以读取到数据，可以解决RR的快照读不可重复读以及幻读问题