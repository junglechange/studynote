# Mysql
## Lock
ref:http://dev.mysql.com/doc/refman/5.5/en/innodb-locking.html
http://blog.csdn.net/xifeijian/article/details/20313977
### Shared and Exclusive Locks

InnoDB implements standard row-level locking where there are two types of locks, shared (S) locks and exclusive (X) locks.

A shared (S) lock permits the transaction that holds the lock to read a row.

An exclusive (X) lock permits the transaction that holds the lock to update or delete a row.

If transaction T1 holds a shared (S) lock on row r, then requests from some distinct transaction T2 for a lock on row r are handled as follows:

- A request by T2 for an S lock can be granted immediately. As a result, both T1 and T2 hold an S lock on r.

- A request by T2 for an X lock cannot be granted immediately.

If a transaction T1 holds an exclusive (X) lock on row r, a request from some distinct transaction T2 for a lock of either type on r cannot be granted immediately. Instead, transaction T2 has to wait for transaction T1 to release its lock on row r.
### 共享锁(S锁,Shared Locks)
读锁 表级锁，被加了S的数据，只能再加S，不能加X。
共享锁允许其他事务读取使用共享锁锁定的数据，但不能修改数据。
### 排他锁(X锁,Exclusive Locks)
写锁 表级锁或行级锁
排他锁不允许其他事务读取和修改使用排他锁锁定的数据。
### 意向锁(Intention Locks)
意向锁是一种表锁，锁定的粒度是整张表，分为：**意向共享锁（IS）** 和**意向排它锁（IX）**两类。意向共享锁表示一个事务有意对数据上共享锁或者排它锁，但是还没真去获取共享锁或排他锁
- SELECT ... LOCK IN SHARE MODE sets an IS lock
- SELECT ... FOR UPDATE sets an IX lock.
## 引擎锁区别
- MyISAM：只支持表级锁。    
- InnoDB：既支持表级锁，也支持行级锁，默认为行级锁。 
## 查看命令
- show status like 'innodb_row_lock%';
- show status like 'Table%';
## 测试
开启两个连接mysql的客户端可以测试加锁的情况。

![image](D:\jungle-study-note\mysql学习\win.png)
