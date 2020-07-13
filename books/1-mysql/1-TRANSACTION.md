# Trancation

## 1. 满足**ACID**的原则

- **原子性 (Atomicity)** 

  一个事务中的所有操作，要么全部成功，要么全部回滚。

  事例
  
  A 给 B 转账 100 元，分为两个操作，第一步 A 的账户扣掉 100 元，第二步 B 的账户添加 100 元。原子性保证了不会出现 A 扣钱成功，B 加钱失败的情况。

- **一致性 (Consistency)** 

  [MySQL的官方文档](https://dev.mysql.com/doc/refman/5.7/en/mysql-acid.html)解释如下
  
  >The consistency aspect of the ACID model mainly involves internal InnoDB processing to protect data from crashes. Related MySQL features include:
  > - InnoDB doublewrite buffer.
  > - InnoDB crash recovery.

  [Wiki](https://en.wikipedia.org/wiki/ACID#Consistency) 上的解释如下

  > Consistency ensures that a transaction can only bring the database from one valid state to another, maintaining database invariants: any data written to the database must be valid according to all defined rules, including constraints, cascades, triggers, and any combination thereof. This prevents database corruption by an illegal transaction, but does not guarantee that a transaction is correct. Referential integrity guarantees the primary key – foreign key relationship.

  上述的两种解释，都是为了保证最终的存储数据是 **valid**，MySQL文档是从崩溃的角度看待一致性，而 Wiki 是从约束的角度出发看待一致性。

  事例

  每个账户都有自己的消费记录，并且给消费记录通过外键指向账户。在删除 A 账户的时候必须，先删除 A 账户的消费记录。一致性保证了每条消费记录都能找到对应的账户。
