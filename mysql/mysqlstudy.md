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
### ������(S��,Shared Locks)
���� ������������S�����ݣ�ֻ���ټ�S�����ܼ�X��
�������������������ȡʹ�ù��������������ݣ��������޸����ݡ�
### ������(X��,Exclusive Locks)
д�� �������м���
���������������������ȡ���޸�ʹ�����������������ݡ�
### ������(Intention Locks)
��������һ�ֱ��������������������ű���Ϊ��**����������IS��** ��**������������IX��**���ࡣ����������ʾһ����������������Ϲ��������������������ǻ�û��ȥ��ȡ��������������
- SELECT ... LOCK IN SHARE MODE sets an IS lock
- SELECT ... FOR UPDATE sets an IX lock.
## ����������
- MyISAM��ֻ֧�ֱ�����    
- InnoDB����֧�ֱ�����Ҳ֧���м�����Ĭ��Ϊ�м����� 
## �鿴����
- show status like 'innodb_row_lock%';
- show status like 'Table%';
## ����
������������mysql�Ŀͻ��˿��Բ��Լ����������

![image](D:\jungle-study-note\mysqlѧϰ\win.png)
