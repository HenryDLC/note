MySql速查



数据库

```sql
-- 显示当前mysql中的数据库列表
show databases;
-- 显示指定名称的数据的创建的SQL指令
show create database <dbName>;

创建数据库
## 创建数据库 dbName表示创建的数据库名称，可以⾃定义
create database <dbName>;
## 创建数据库，当指定名称的数据库不存在时执⾏创建
create database if not exists <dbName>;
## 在创建数据库的同时指定数据库的字符集（字符集：数据存储在数据库中采⽤的编码格式
utf8 gbk）
create database <dbName> character set utf8;

修改数据库 修改数据库字符集
## 修改数据库的字符集
alter database <dbName> character set utf8; # utf8 gbk

删除数据库 删除数据库时会删除当前数据库中所有的数据表以及数据表中的数据
## 删除数据库
drop database <dbName>;
## 如果数据库存在则删除数据库
drop database is exists <dbName>;

使⽤/切换数据库
use <dbName>
```

数据表

```sql
查询数据表
show tables;

查询表结构
desc <tableName>;

删除数据表
## 删除数据表
drop table <tableName>;
## 当数据表存在时删除数据表
drop table if exists <tableName>;

修改数据表
## 修改表名
alter table <tableName> rename to <newTableName>;
## 数据表也是有字符集的，默认字符集和数据库⼀致
alter table <tableName> character set utf8;
## 添加列（字段）
alter table <tableName> add <columnName> varchar(200);
## 修改列（字段）的列表和类型
alter table <tableName> change <oldColumnName> <newCloumnName> <type>;
## 只修改列（字段）类型
alter table <tableName> modify <columnName> <newType>;
## 删除列（字段）
alter table stus drop <columnName>;

```

数值类型(常用)

| 类型        | 字节大小 | 有符号范围(Signed)                         | 无符号范围(Unsigned)     |
| ----------- | -------- | ------------------------------------------ | ------------------------ |
| TINYINT     | 1        | -128 ~ 127                                 | 0 ~ 255                  |
| SAMLLINT    | 2        | -32768 ~ 32767                             | 0 ~ 65535                |
| MEDIUMINT   | 3        | -8388608 ~ 8388607                         | 0 ~ 16777215             |
| INT/INTEGER | 4        | -2147483648 ~2147483647                    | 0 ~ 4294967295           |
| BIGINT      | 8        | -9223372036854775808 ~ 9223372036854775807 | 0 ~ 18446744073709551615 |

字符串

| 类型    | 字节大小 | 示例                                                         | 类型    |
| ------- | -------- | ------------------------------------------------------------ | ------- |
| CHAR    | 0-255    | 类型:char(3) 输入 'ab', 实际存储为'ab ', 输入'abcd' 会报长度过长的错误 | CHAR    |
| VARCHAR | 0-255    | 类型:varchar(3) 输 'ab',实际存储为'ab', 输入'abcd',会报长度过长的错误 | VARCHAR |
| TEXT    | 0-65535  | 大文本                                                       | TEXT    |
| 类型    | 字节大小 | 示例                                                         | 类型    |
| CHAR    | 0-255    | 类型:char(3) 输入 'ab', 实际存储为'ab ', 输入'abcd' 会报长度过长的错误 | CHAR    |

日期时间类型

| 类型      | 字节大小 | 示例                                                  | 类型      |
| --------- | -------- | ----------------------------------------------------- | --------- |
| DATE      | 4        | '2020-01-01'                                          | DATE      |
| TIME      | 3        | '12:29:59'                                            | TIME      |
| DATETIME  | 8        | '2020-01-01 12:29:59'                                 | DATETIME  |
| YEAR      | 1        | '2017'                                                | YEAR      |
| TIMESTAMP | 4        | '1970-01-01 00:00:01' UTC ~ '2038-01-01 00:00:01' UTC | TIMESTAMP |

约束

* 主键primary key：物理上存储的顺序
* 非空not null：此字段不允许填写空值
* 惟一unique：此字段的值不允许重复
* 默认default：当不填写此值时会使用默认值，如果填写时以填写为准
* 外键foreign key：对关系字段进行约束，当为关系字段填写值时，会到关联的表中查询此值是否存在，如果存在则填写成功，如果不存在则填写失败并抛出异常
* 说明：虽然外键约束可以保证数据的有效性，但是在进行数据的crud（增加、修改、删除、查询）时，都会降低数据库的性能，所以不推荐使用，那么数据的有效性怎么保证呢？答：可以在逻辑层进行控制

### 为什么要给表中的列添加约束呢？

* 保证数据的有效性

* 保证数据的完整性

* 保证数据的正确性

```sql
## 创建约束
create table books(
  book_isbn char(4) primary key,
);
-- or
create table books(
  book_isbn char(4),
  primary key(book_isbn) );
   
## 删除数据表主键约束
alter table books drop primary key;
## 创建表之后添加主键约束
alter table books modify book_isbn char(4) primary key;

## 联合主键
create table grades(
 stu_num char(8),
 course_id int,
primary key(stu_num,course_id) );
```

定义主键⾃动增⻓

```sql
## 定义int类型字段⾃动增⻓： auto_increment
create table types(
 type_id int primary key auto_increment,
);
```

### **DML** 数据操纵语⾔

> ⽤于完成对数据表中数据的插⼊、删除、修改操作

```sql
插⼊数据
insert into <tableName>(columnName,columnName....)
values(value1,value2....);

删除数据
delete from <tableName> [where conditions];

修改数据
update <tableName> set columnName=value [where conditions]
```

### **DQL** 数据查询语⾔

> 从数据表中提取满⾜特定条件的记录
>
> * 单表查询
>
> * 多表联合查询

```sql
查询基础语法
## select 关键字后指定要显示查询到的记录的哪些列
select colnumName1[,colnumName2,colnumName3...] from <tableName> [where
conditions];
## 如果要显示查询到的记录的所有列，则可以使⽤ * 替代字段名列表 （在项⽬开发中不建议
使⽤*）
select * from stus;

`where ⼦句
delete from tableName where conditions;
update tabeName set ... where conditions;
select .... from tableName where conditions;

条件关系运算符
## = 等于
select * from stus where stu_num = '20210101';
## != <> 不等于
select * from stus where stu_num != '20210101';
select * from stus where stu_num <> '20210101';
## > ⼤于
select * from stus where stu_age>18;
## < ⼩于
select * from stus where stu_age<20;
## >= ⼤于等于
select * from stus where stu_age>=20;
## <= ⼩于等于
select * from stus where stu_age<=20;
## between and 区间查询 between v1 and v2 [v1,v2]
select * from stus where stu_age between 18 and 20;

条件逻辑运算符
## and 并且 筛选多个条件同时满⾜的记录
select * from stus where stu_gender='⼥' and stu_age<21;
## or 或者 筛选多个条件中⾄少满⾜⼀个条件的记录
select * from stus where stu_gender='⼥' or stu_age<21;
## not 取反
select * from stus where stu_age not between 18 and 20; 1234567

LIKE ⼦句
select * from tableName where columnName like 'reg';
# 在like关键字后的reg表达式中
# % 表示任意多个字符 【 %o% 包含字⺟o】 
# _ 表示任意⼀个字符 【 _o% 第⼆个字⺟为o】

设置查询的列
select colnumName1,columnName2,... from stus where stu_age>20;

`as 字段取别名
select stu_name,2021-stu_age as stu_birth_year from stus;

`distinct 消除重复⾏
select distinct stu_age from stus;

排序 - order by
select * from tableName where conditions order by columnName asc|desc;

聚合函数
# count
select count(stu_num) from stus;
# max
select max(stu_age) from stus;
# min
select min(stu_age) from stus;
# sum
select sum(stu_age) from stus;
# avg
select avg(stu_age) from stus;

⽇期函数
# 通过字符串类型 给⽇期类型的列赋值
insert into
stus(stu_num,stu_name,stu_gender,stu_age,stu_tel,stu_qq,stu_enterence)
values('20200108','张⼩三','⼥',20,'13434343344','123111','2021-09-01
09:00:00');
# 通过now()获取当前时间
insert into
stus(stu_num,stu_name,stu_gender,stu_age,stu_tel,stu_qq,stu_enterence)
values('20210109','张⼩四','⼥',20,'13434343355','1233333',now());
# 通过sysdate()获取当前时间
insert into
stus(stu_num,stu_name,stu_gender,stu_age,stu_tel,stu_qq,stu_enterence)
values('20210110','李雷','男',16,'13434343366','123333344',sysdate());
# 通过now和sysdate获取当前系统时间
mysql> select now();
mysql> select sysdate();

分组查询 - group by
select 分组字段/聚合函数
from 表名
[where 条件]
group by 分组列名 [having 条件] [order by 排序字段]
## select 后使⽤ * 显示对查询的结果进⾏分组之后，显示每组的第⼀条记录（这种显示通常是⽆意义的）
## select 后通常显示分组字段和聚合函数(对分组后的数据进⾏统计、求和、平均值等)
## 语句执⾏属性:
-- 1)先根据where条件从数据库查询记录 
-- 2)group by对查询记录进⾏分组 
-- 3)执⾏having对分组后的数据进⾏筛选

分⻚查询 - limit
select ...
from ... 
where ...
limit param1,param2

# param1 int , 表示获取查询语句的结果中的第⼀条数据的索引（索引从0开始）
# param2 int, 表示获取的查询记录的条数（如果剩下的数据条数<param2，则返回剩下的所有记录）
```

### 外键约束

```sql
#【⽅式⼀】在创建表的时候，定义cid字段，并添加外键约束
# 由于cid 列 要与classes表的class_id进⾏关联，因此cid字段类型和⻓度要与class_id⼀致
create table students(
stu_num char(8) primary key,
 stu_name varchar(20) not null,
 stu_gender char(2) not null,
 stu_age int not null,
 cid int,
constraint FK_STUDENTS_CLASSES foreign key(cid) references
classes(class_id) );
#【⽅式⼆】先创建表，再添加外键约束
create table students(
stu_num char(8) primary key,
 stu_name varchar(20) not null,
 stu_gender char(2) not null,
 stu_age int not null,
 cid int
);
# 在创建表之后，为cid添加外键约束
alter table students add constraint FK_STUDENTS_CLASSES foreign
key(cid) references classes(class_id);

# 删除外键约束
alter table students drop foreign key FK_STUDENTS_CLASSES;

级联修改 和 级联删除
（修改一个外键数据，与之对应的外键表数据也随之修改）
在添加外键时，设置级联修改 和 级联删除
# 删除原有的外键
alter table students drop foreign key FK_STUDENTS_CLASSES;
# 重新添加外键，并设置级联修改和级联删除
alter table students add constraint FK_STUDENTS_CLASSES foreign
key(cid) references classes(class_id) ON UPDATE CASCADE ON DELETE
CASCADE;


```

### 连接查询

> 在MySQL中可以使⽤join实现多表的联合查询——连接查询，join按照其功能不同分为
>
> 三个操作：
>
> * inner join 内连接
>
> * left join 左连接
>
> * right join 右连接

### 内连接 INNER JOIN

> 笛卡尔积
>
> * 笛卡尔积（A集合&B集合）：使⽤A中的每个记录⼀次关联B中每个记录，笛卡尔积的总数=A总数*B总数
>
> * 如果直接执⾏ select ... from tableName1 inner join tableName2; 会获取两种数据表中的数据集合的笛卡尔积（依次使⽤tableName1 表中的每⼀条记录 去 匹配tableName2的每条数据）

```sql
select ... from tableName1 inner join tableName2 ON 匹配条件 [where 条件];

使⽤ on 设置两张表连接查询的匹配条件
-- 使⽤where设置过滤条件：先⽣成笛卡尔积再从笛卡尔积中过滤数据（效率很低）
select * from students INNER JOIN classes where students.cid = classes.class_id;
-- 使⽤ON设置连接查询条件：先判断连接条件是否成⽴，如果成⽴两张表的数据进⾏组合⽣成⼀条结果记录
select * from students INNER JOIN classes ON students.cid =
classes.class_id;
```

### 左连接 **LEFT JOIN**

> 左连接：显示左表中的所有数据，如果在有右表中存在与左表记录满⾜匹配条件的数据，则进⾏匹配；如果右表中不存在匹配数据，则显示为Null

```sql
# 语法
select * from leftTabel LEFT JOIN rightTable ON 匹配条件 [where 条件];
-- 左连接 : 显示左表中的所有记录
select * from students LEFT JOIN classes ON students.cid =
classes.class_id;
```

###  右连接 **RIGHT JOIN**

```sql
-- 右连接 ：显示右表中的所有记录
select * from students RIGHT JOIN classes ON students.cid =
classes.class_id;
```

### 数据表别名

> 如果在连接查询的多张表中存在相同名字的字段，我们可以使⽤ 表名.字段名 来进⾏区分，如果表名太⻓则不便于SQL语句的编写，我们可以使⽤数据表别名

```sql
select s.*,c.class_name
from students s
INNER JOIN classes c
ON s.cid = c.class_id;
```

### ⼦查询**/**嵌套查询

> ⼦查询 — 先进⾏⼀次查询，第⼀次查询的结果作为第⼆次查询的源/条件（第⼆次查询是基于第⼀次的查询结果来进⾏的）

```sql
⼦查询返回单个值-单⾏单列
-- 如果⼦查询返回的结果是⼀个值（单列单⾏），条件可以直接使⽤关系运算符（= !=....）
select * from students where cid = (select class_id from classes where
class_name='Java2105');

⼦查询返回多个值-多⾏单列
-- 如果⼦查询返回的结果是多个值（单列多⾏），条件使⽤IN / NOT IN
select * from students where cid IN (select class_id from classes where
class_name LIKE 'Java%');

⼦查询返回多个值-多⾏多列
-- ⼦查询:先查询cid=1班级中的所有学⽣信息，将这些信息作为⼀个整体虚拟表(多⾏多列)
-- 再基于这个虚拟表查询性别为男的学⽣信息（‘虚拟表’需要别名）
select * from (select * from students where cid=1) t where
t.stu_gender='男';
```

## 索引

```sql
唯⼀索引
-- 创建唯⼀索引: 创建唯⼀索引的列的值不能重复
-- create unique index <index_name> on 表名(列名);
create unique index index_test1 on tb_testindex(tid); 

普通索引
-- 创建普通索引: 不要求创建索引的列的值的唯⼀性
-- create index <index_name> on 表名(列名);
create index index_test2 on tb_testindex(name);

组合索引
-- 创建组合索引
-- create index <index_name> on 表名(列名1,列名2...);
create index index_test3 on tb_testindex(tid,name); 

全⽂索引（不支持中文，弃用）
create fulltext index <index_name> on 表名(字段名);

删除索引
drop index index_test3 on tb_testindex;
```

索引的使⽤总结

 优点

* 索引⼤⼤降低了数据库服务器在执⾏查询操作时扫描的数据，提⾼查询效率

* 索引可以避免服务器排序、将随机IO编程顺序IO

缺点

* 索引是根据数据表列的创建的，当数据表中数据发⽣DML操作时，索引⻚需要更新；

* 索引⽂件也会占⽤磁盘空间；

注意事项

* 数据表中数据不多时，全表扫⾯可能更快吗，不要使⽤索引；

* 数据量⼤但是DML操作很频繁时，不建议使⽤索引；

* 不要在数据重复读⾼的列上创建索引（性别）；

* 创建索引之后，要注意查询SQL语句的编写，避免索引失效。

## 数据库事务

> 我们把完成特定的业务的多个数据库DML操作步骤称之为⼀个事务
>
> 事务，就是完成同⼀个业务的多个DML操作

```sql
-- 借书业务
-- 操作1：在借书记录表中添加记录
insert into records(snum,bid,borrow_num,is_return,borrow_date)
values('1001',1,1,0,sysdate());
-- 操作2：修改图书库存
update books set book_stock=book_stock-1 where book_id=1;
-- 转账业务：张三给李四转账1000
-- 操作1：李四的帐号+1000
-- 操作2：张三的账户-1000
```

### 数据库事务特性

原⼦性（Atomicity）：⼀个事务中的多个DML操作，要么同时执⾏成功，要么同时执⾏失败

⼀致性（Consistency）：事务执⾏之前和事务执⾏之后，数据库中的数据是⼀致的，完整性和⼀致性不能被破坏

隔离性（Isolation）：数据库允许多个事务同时执⾏（张三借Java书的同时允许李四借Java书），多个必⾏的事务之间不能相互影响

持久性（Durability）：事务完整之后，对数据库的操作是永久的

#### 事务隔离级别

> 数据库允许多个事务并⾏，多个事务之间是隔离的、相互独⽴的；如果事务之间不相互隔离并且操作同⼀数据时，可能会导致数据的⼀致性被破坏。

read uncommitted（读未提交）：在一个事物中读取到的另一个还没有提交的数据，会出现——`脏读`

read committed（读已提交）：已经解决了脏读问题，在一个事物中只能读取另一个事物已提交的数据，这种情况会出现`不可重复读`的问题：在事物中重复读数据，数据的内容是不一样的

repeatable read（可重复读）（默认级别）：在一个事物中每次读取到的数据都是一致的，不会出现脏读和不可重复读的问题。但是会出现——虚读（幻读）：两个事物中同时查询了表中数据，一个事物提交了数据更改，另一个事物提交了相同的数据更改会提示`主键重复`，但是这个事物查询到的数据并没有相同主键的id。因为MVCC的版本控制问题，事物A提交了数据，事物B查询的数据不是最新的数据，但是每次做写操作时MVCC都会先去查最新的版本，而再最新的版本中已经有了相同的主键，所以事物B无法二次插入。但是因为查询的数据并没有相同的主键所以仿佛是幻觉一样。

解决虚读：通过上行锁解决虚读问题。

上行锁成功：其他事物需要等待该条数据成功执行后再执行，哪怕插入相同数据其余事物也会等待后失败。

上行锁失败：其他事物正在对该条数据做写入操作（InnoDB在事物中对数据做写操作自动上行锁），所以该事物无法直接上行锁直到其他事物提交数据后该事物才能上行锁程功。如果其他事物和该事物插入的数据一样，该事物上行锁的select会有数据，再对比该数据和该事物要插入的数据对比选择是否继续插入数据。

Serializable（串行化）：串行化的隔离级别不允许任何并发发生，不存在任何并发问题。相当于锁表，性能非常差，一般都不考虑。





5400  5%  