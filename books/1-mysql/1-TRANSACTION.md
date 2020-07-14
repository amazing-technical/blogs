# InnoDB Trancation

## 1. 满足**ACID**的原则

### a. 原子性 (Atomicity)

  一个事务中的所有操作，要么全部成功，要么全部回滚。

  事例
  
  A 给 B 转账 100 元，分为两个操作，第一步 A 的账户扣掉 100 元，第二步 B 的账户添加 100 元。原子性保证了不会出现 A 扣钱成功，B 加钱失败的情况。

### b. 一致性 (Consistency)

#### 定义

一致性的目的是为了保证最终的存储数据是 **valid**。

%accordion%Wiki 对 Consistency 的定义%accordion%

Consistency ensures that a transaction can only bring the database from one valid state to another, maintaining database invariants: **any data written to the database must be valid according to all defined rules, including constraints, cascades, triggers, and any combination thereof**. This prevents database corruption by an illegal transaction, but does not guarantee that a transaction is correct. Referential integrity guarantees the primary key – foreign key relationship.

%/accordion%
  

#### 事例

  每个账户都有多条消费记录，并且给消费记录通过外键指向账户。在添加消费记录的时候，外键关系保证每条消费记录都能找到对应的账户。一致性保证了不会出现找不到账户的消费记录。

### c. 隔离性 (Isolation)

  多个事务之间的隔离，分为四个等级（其中 X,Y 为两个事务）。

  1. Read uncommitted


  

  <!-- |隔离级别|详情|
  |-|-|
  |Read uncommitted|X 可以读到 Y 还未 Commit 的修改|
  |Read committed|X 只能读到 Y 已经 Commit 的修改|
  |Repeatable read| X 读了一次 A 账户 100 元， Y 把 A 账户修改为 200 元，X 再次读取 A 账户，得到的还是 100 元|
  |Serializable|| -->

### d. 持久性 (Durability)

  事务提交成功之后，即使MySQL崩溃了，修改也会被永久保存

  A 消费 100 元，刚刚保存结束，MySQL 服务就崩溃了，再次启动 MySQL 服务之后，仍然能看到 A 消费的 100 元。
  