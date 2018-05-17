### 数据库

---

##### ！1、范式

1. 第一范式（确保每列保持原子性）

   数据库表中的所有字段值都是不可分解的原子值

2. 第二范式（确保表中的每列都和主键相关）

   确保数据库表中的每一列都和主键相关，而不能只与主键的某一部分相关，也就是说在一个数据库表中，一个表中只能保存一种数据，不可以把多种数据保存在同一张数据库表中

3. 第三范式（确保每列都和主键列直接相关,而不是间接相关）

   确保数据表中的每一列数据都和主键直接相关，而不能间接相关

##### ！2、数据库事务和隔离级别

| 事务隔离级别              | 脏读 | 不可重复读 | 幻读 |
| ------------------------- | ---- | ---------- | ---- |
| 读未提交 read-uncommitted | 是   | 是         | 是   |
| 不可重复读 read-committed | 否   | 是         | 是   |
| 可重复读 repeatable-read  | 否   | 否         | 是   |
| 串行化 serializable       | 否   | 否         | 否   |

**读未提交**：另一个事务修改了数据，但尚未提交，而本事务中的SELECT会读到这些未被提交的数据**脏读**

**不可重复读**：事务 A 多次读取同一数据，事务 B 在事务A多次读取的过程中，对数据作了更新并提交，导致事务A多次读取同一数据时，结果因此本事务先后两次读到的数据结果会不一致。

**可重复读**：在同一个事务里，SELECT的结果是事务开始时时间点的状态，因此，同样的SELECT操作读到的结果会是一致的。但是，会有**幻读**现象

**串行化**：最高的隔离级别，在这个隔离级别下，不会产生任何异常。并发的事务，就像事务是在一个个按照顺序执行一样

**MySQL默认的事务隔离级别为repeatable-read** 


##### ！3、为什么需要锁，锁定分类，锁粒度


##### %4、乐观锁，悲观锁的概念及实现方式


##### ！5、分页如何实现（Oracle，MySql） 

##### ！6、Mysql引擎

常见的两种存储引擎的区别

|                        | **MyIASM**             | **Innodb** |
| ---------------------- | ---------------------- | ---------- |
| 事务支持               | 不支持                 | 支持       |
| 锁粒度                 | 表级                   | 行级       |
| 存储容量（一张表空间） | 默认256TB 最大 65536TB | 64TB       |
| 哈希索引               | 不支持                 | 支持       |
| 全文索引               | 支持                   | 不支持     |
| 外键                   | 不支持                 | 支持       |

MEMORY： 不支持事务 存放在内存中多用于临时表 处理速度快 如果断电数据将会丢失

TokuDB：   支持事务 有着出色的数据压缩功能和快速写入性能 但是不适合读取 因为需要进行解压缩操作

Archive：    不支持事务 不支持事务 使用行锁来实现高并发插入操作 适合数据归档例如历史记录


##### ？7、MYSQL语句优化


##### %8、从一张大表读取数据，如何解决性能问题


##### ！9、内连接，左连接，右连接作用及区别 

##### ！10、Statement和PreparedStatement之间的区别 

1. Statement 用于通用执行静态SQL语句
2. PreparedStatement  用于参数化执行SQL语句并且将会将SQL转为二进制（预编译），可以防止SQL注入式攻击，在SQL执行时跳过了校验语法的预处理器，执行效率要比Statement高。[benmark](https://github.com/jOOQ/jOOQ/issues/1625)
3. CallableStatement 用于执行存储过程

##### %11、索引以及索引的实现(B+树介绍、和B树、R树区别

##### ？12、什么是数据库连接池

程序启动时建立足够的数据库连接，并将这些连接组成一个连接池，由程序动态地对池中的连接进行申请，使用，释放


##### 参考资料


>Contributes: https://juejin.im/post/5ab50d9b6fb9a028c812cc78
>
>Reviewers : Hollis, Kevin Lee