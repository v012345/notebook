[带你遨游银河系的 10 种分布式数据库](https://www.51cto.com/article/665674.html)

## NULL
字段定义了数据类型（整型、浮点型、字符串、日期等），以及是否允许为NULL。注意NULL表示字段数据不存在。一个整型字段如果为NULL不表示它的值为0，同样的，一个字符串型字段为NULL也不表示它的值为空串''。

 通常情况下，字段应该避免允许为NULL。不允许为NULL可以简化查询条件，加快查询速度，也利于应用程序读取数据后无需判断是否为NULL。

## 主键
选取主键的一个基本原则是：不使用任何业务相关的字段作为主键。

因此，身份证号、手机号、邮箱地址这些看上去可以唯一的字段，均不可用作主键。

## 联合主键
关系数据库实际上还允许通过多个字段唯一标识记录，即两个或更多的字段都设置为主键，这种主键被称为联合主键。

对于联合主键，允许一列有重复，只要不是所有主键列都重复即可：

没有必要的情况下，我们尽量不使用联合主键，因为它给关系表带来了复杂度的上升。

## 外键
```sql
ALTER TABLE students
ADD CONSTRAINT fk_class_id
FOREIGN KEY (class_id)
REFERENCES classes (id);
```
其中，外键约束的名称fk_class_id可以任意，FOREIGN KEY (class_id)指定了class_id作为外键，REFERENCES classes (id)指定了这个外键将关联到classes表的id列（即classes表的主键）。

要删除一个外键约束，也是通过ALTER TABLE实现的：
```sql
ALTER TABLE students
DROP FOREIGN KEY fk_class_id;
```

由于外键约束会降低数据库的性能，大部分互联网应用程序为了追求速度，并不设置外键约束，而是仅靠应用程序自身来保证逻辑的正确性。这种情况下，class_id仅仅是一个普通的列，只是它起到了外键的作用而已。

## 一对一
还有一些应用会把一个大表拆成两个一对一的表，目的是把经常读取和不经常读取的字段分开，以获得更高的性能。例如，把一个大的用户表分拆为用户基本信息表user_info和用户详细信息表user_profiles，大部分时候，只需要查询user_info表，并不需要查询user_profiles表，这样就提高了查询速度。

## 索引
在关系数据库中，如果有上万甚至上亿条记录，在查找记录的时候，想要获得非常快的速度，就需要使用索引。

索引是关系数据库中对某一列或多个列的值进行预排序的数据结构。通过使用索引，可以让数据库系统不必扫描整个表，而是直接定位到符合条件的记录，这样就大大加快了查询速度。

如果要经常根据score列进行查询，就可以对score列创建索引：
```sql
ALTER TABLE students
ADD INDEX idx_score (score);
```

使用ADD INDEX idx_score (score)就创建了一个名称为idx_score，使用列score的索引。索引名称是任意的，索引如果有多列，可以在括号里依次写上，例如：
```sql
ALTER TABLE students
ADD INDEX idx_name_score (name, score);
```

索引的效率取决于索引列的值是否散列，即该列的值如果越互不相同，那么索引效率越高。反过来，如果记录的列存在大量相同的值，例如gender列，大约一半的记录值是M，另一半是F，因此，对该列创建索引就没有意义。

可以对一张表创建多个索引。索引的优点是提高了查询效率，缺点是在插入、更新和删除记录时，需要同时修改索引，因此，索引越多，插入、更新和删除记录的速度就越慢。

### select
上述查询会直接计算出表达式的结果。虽然SELECT可以用作计算，但它并不是SQL的强项。但是，不带FROM子句的SELECT语句有一个有用的用途，就是用来判断当前到数据库的连接是否有效。许多检测工具会执行一条SELECT 1;来测试数据库连接。

###
要组合三个或者更多的条件，就需要用小括号()表示如何进行条件运算。

如果不加括号，条件运算按照NOT、AND、OR的优先级进行，即NOT优先级最高，其次是AND，最后是OR。加上括号可以改变优先级。

### order by
如果有WHERE子句，那么ORDER BY子句要放到WHERE子句后面。

## 分页
OFFSET是可选的，如果只写LIMIT 15，那么相当于LIMIT 15 OFFSET 0。

在MySQL中，LIMIT 15 OFFSET 30还可以简写成LIMIT 30, 15。

使用LIMIT <M> OFFSET <N>分页时，随着N越来越大，查询效率也会越来越低。

## 聚合查询
如果聚合查询的WHERE条件没有匹配到任何行，COUNT()会返回0，而SUM()、AVG()、MAX()和MIN()会返回NULL：

## GROUP BY 一般跟着  聚合查询 走
```sql
SHOW VARIABLES LIKE 'sql_mode';
```
只关心其中一个称之为ONLY_FULL_GROUP_BY的家伙。只要sql_mode的值里边有这个东东，MySQL服务器就“比较正常”（也就是不允许非分组列放到查询列表中），但是如果我们把这个东东从sql_mode系统变量中移除

## 要列出所有数据库
```sql
SHOW DATABASES;
```
其中，information_schema、mysql、performance_schema和sys是系统库，不要去改动它们。其他的是用户创建的数据库。

## 要创建一个新数据库，使用命令：
```sql
 CREATE DATABASE test;
```

## 对一个数据库进行操作时，要首先将其切换为当前数据库：
```sql
mysql> USE test;
```

## 列出当前数据库的所有表，使用命令：
```
SHOW TABLES;
```

## 要查看一个表的结构，使用命令：
```
DESC students;
```

## 可以使用以下命令查看创建表的SQL语句：
```
 SHOW CREATE TABLE students;
```

### 修改表就比较复杂。如果要给students表新增一列birth，使用：
```sql
ALTER TABLE students ADD COLUMN birth VARCHAR(10) NOT NULL;
```

## 要修改birth列，例如把列名改为birthday，类型改为VARCHAR(20)：
```sql
ALTER TABLE students CHANGE COLUMN birth birthday VARCHAR(20) NOT NULL;
```

## 插入或替换 
如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就先删除原记录，再插入新记录。此时，可以使用REPLACE语句，这样就不必先查询，再决定是否先删除再插入：
```sql
REPLACE INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99);
```
若id=1的记录不存在，REPLACE语句将插入新记录，否则，当前id=1的记录将被删除，然后再插入新记录。


## 插入或更新
如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就更新该记录，此时，可以使用INSERT INTO ... ON DUPLICATE KEY UPDATE ...语句：
```sql
INSERT INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99) ON DUPLICATE KEY UPDATE name='小明', gender='F', score=99;
```
若id=1的记录不存在，INSERT语句将插入新记录，否则，当前id=1的记录将被更新，更新的字段由UPDATE指定。

### 插入或忽略
如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就啥事也不干直接忽略，此时，可以使用INSERT IGNORE INTO ...语句：
```sql
INSERT IGNORE INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99);
```
若id=1的记录不存在，INSERT语句将插入新记录，否则，不执行任何操作。

## 快照
如果想要对一个表进行快照，即复制一份当前表的数据到一个新表，可以结合CREATE TABLE和SELECT：
```sql
-- 对class_id=1的记录进行快照，并存储为新表students_of_class1:
CREATE TABLE students_of_class1 SELECT * FROM students WHERE class_id=1;
```
新创建的表结构和SELECT使用的表结构完全一致。

## 写入查询结果集
如果查询结果集需要写入到表中，可以结合INSERT和SELECT，将SELECT语句的结果集直接插入到指定表中。

例如，创建一个统计成绩的表statistics，记录各班的平均成绩：
```sql
CREATE TABLE statistics (
    id BIGINT NOT NULL AUTO_INCREMENT,
    class_id BIGINT NOT NULL,
    average DOUBLE NOT NULL,
    PRIMARY KEY (id)
);
```
然后，我们就可以用一条语句写入各班的平均成绩：
```sql
INSERT INTO statistics (class_id, average) SELECT class_id, AVG(score) FROM students GROUP BY class_id;
```
确保INSERT语句的列和SELECT语句的列能一一对应，就可以在statistics表中直接保存查询的结果

### 强制使用指定索引
在查询的时候，数据库系统会自动分析查询语句，并选择一个最合适的索引。但是很多时候，数据库系统的查询优化器并不一定总是能使用最优索引。如果我们知道如何选择索引，可以使用FORCE INDEX强制查询使用指定的索引。例如：
```sql
 SELECT * FROM students FORCE INDEX (idx_class_id) WHERE class_id = 1 ORDER BY id DESC;
```
指定索引的前提是索引idx_class_id必须存在。

## 事务
对于单条SQL语句，数据库系统自动将其作为一个事务执行，这种事务被称为隐式事务。

要手动把多条SQL语句作为一个事务执行，使用BEGIN开启一个事务，使用COMMIT提交一个事务，这种事务被称为显式事务，例如，把上述的转账操作作为一个显式事务：
```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

## 隔离级别
对于两个并发执行的事务，如果涉及到操作同一条记录的时候，可能会发生问题。因为并发操作会带来数据的不一致性，包括脏读、不可重复读、幻读等。数据库系统提供了隔离级别来让我们有针对性地选择事务的隔离级别，避免数据不一致的问题。

SQL标准定义了4种隔离级别，分别对应可能出现的数据不一致的情况：
| Isolation Level  | 脏读（Dirty Read） | 不可重复读（Non Repeatable Read） | 幻读（Phantom Read） |
| :--------------: | :----------------: | :-------------------------------: | :------------------: |
| Read Uncommitted |        Yes         |                Yes                |         Yes          |
|  Read Committed  |         -          |                Yes                |         Yes          |
| Repeatable Read  |         -          |                 -                 |         Yes          |
|   Serializable   |         -          |                 -                 |          -           |



## [各种锁](https://www.modb.pro/db/55483)

## [主从](https://www.modb.pro/db/55483)
在master上给一个slave注册一个账号
```sql
GRANT REPLICATION SLAVE ON *.* TO 'slave1'@167.179.83.226 IDENTIFIED BY 'slave1Password';
```
CREATE USER 'replica'@'167.179.83.226' IDENTIFIED BY 'Qq_12233334444';

GRANT REPLICATION SLAVE ON *.* TO 'replica'@'167.179.83.226';

SHOW MASTER STATUS\G
```
File: mysql-bin.000004
Position: 1037
Binlog_Do_DB:
Binlog_Ignore_DB:
Executed_Gtid_Set:
```
```sql
CHANGE MASTER TO
MASTER_HOST='45.76.212.5' ,
MASTER_USER='replica' ,
MASTER_PASSWORD='Qq_12233334444' ,
MASTER_LOG_FILE='mysql-bin.000004' ,
MASTER_LOG_POS=1076978;
```

bind-address =45.76.212.5
server-id = 1
log_bin =mysql-bin


bind-address =167.179.83.226
server-id = 2
log_bin =mysql-bin


----

## 公网接入


## 重新同步
1. 锁主数据库
```sql
flush tables with read lock;
```
2. 解锁主数据库
```sql
unlock tables;
```


