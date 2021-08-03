# Mysql数据库入门


# Mysql数据库入门

## 概念

数据库(Database，DB)是按照数据结构来组织，存储和管理数据的仓库；底层以二维表形式保存数据的库就是关系型数据库关系型数据库；常见关系型数据库有Oracle(Oracle)、DB2(IBM)、SQL Server(MS)、MySQL(Oracle)

## 常见数据结构

MySQL支持多种类型，大致可以分为四类：数值型、浮点型、日期/时间和字符串(字符)类型

### 数值型

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210720113014.png " ")

### 浮点型

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210720113028.png " ")

### 日期型

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210720113042.png " ")

### 字符型

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210720113057.png " ")

## 字段约束

### 主键约束

主键约束：如果为一个列添加了主键约束，那么这个列就是主键，主键的特点是唯一且不能为空。通常情况下，每张表都会有主键。

主键自增策略**当主键为数值类型时，为了方便维护，可以设置主键自增策略（auto_increment），设置了主键自增策略后，数据库会在表中保存一个AUTO_INCREMENT变量值，初始值为1，当需要id值，不需要我们指定值，由数据库负责从AUTO_INCREMENT获取一个id值，作为主键值插入到表中。而且每次用完AUTO_INCREMENT值，都会自增1. AUTO_INCREMENT=1

```sql
create table abc(
id int primary key auto_increment
);
insert into abc values(null);
insert into abc values(null);
insert into abc values(null);
select * from abc;
```

### 非空约束

非空约束：如果为一个列添加了非空约束，那么这个列的值就不能为空，但可以重复。

```sql
create table user(
id int primary key auto_increment,
password varchar(50) not null
);
show tables;
insert into user values(null,null);//不符合非空约束
insert into user values(null,123;);//OK
```

### 唯一约束

唯一约束：如果为一个列添加了唯一约束，那么这个列的值就必须是唯一的（即不能重复），但可以为空。

```sql
create table test(
id int primary key auto_increment,
username varchar(50) unique--唯一约束
	);
show tables;
insert into test values(null,'lisi');
insert into test values(null,'lisi');--username的值要唯一,重复会报错的
select * from test;
```

### 外键约束

外键其实就是用于通知数据库两张表数据之间对应关系的这样一个列。这样数据库就会帮我们维护两张表中数据之间的关系。注意，创建表的同时添加外键

- 如何保存两张表（dept、emp）之间的关系，通常我们会在多的一方(emp)添加一个列(dept_id)来保存另一方(dept)的主键(id)，以此来保存两张表数据之间的对应关系

```sql
create table emp(
 id int,
 name varchar(50),
 dept_id int,
 foreign key(dept_id) references dept(id)
);
```

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210720113415.png " ")

## SQL语句

- SQL ： Structured Query Language 结构化查询语言
- SQL是在关系数据库上执行数据操作、检索及维护所使用的标准语言
- 可以用来查询数据，操纵数据，定义数据，控制数据



### Sql语句分类

- 数据定义语言(DDL)：Data Definition Language
- 数据操纵语言(DML)：Data Manipulation Language
- 数据查询语言(DQL)：Data Query Language
- 数据控制语言(DCL)：Data Control Language
- 事务控制语言(TCL)：Transaction Control Language

#### 数据定义语言—DDL

- create （database/tavble） 创建库 创建表
- alter (table) 添加、删除、修改数据表字段（列）
- drop (database/table) 删除库 删除表



- 库相关

```sql
CREATE DATABASE mybase;
CREATE DATABASE mybase CHARACTER SET UTF8;
```

```sql
SHOW DATABASES;
```

```sql
SELECT DATABASE();
#查看当前使用的数据库
```

```sql
ALTER DATABASE mybase CHARACTER SET UTF8;
修改数据库编码
```

```sql
DROP DATABASE mybase;
#删除数据库
```

```sql
USE mybase;
#切换数据库
```

- 表相关

```sql
#创建表
create table exam(
id INT(11) PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(20),
English INT,
Chinese INT,
Math int
);

```

```sql
desc exam;
#查看表结构
```

```sql
drop table exam;
#删除表
```

```sql
ALTER TABLE exam ADD History INT NOT NULL;
#添加列
```

```
ALTER TABLE exam MODIFY History DOUBLE(7,2);
#修改列的类型、长度、约束
```

```sql
ALTER TABLE exam CHANGE History Physics INT NOT NULL;
#修改表的列名
```

```sql
RENAME TABLE exam TO score;
#修改表名
```

```
ALTER TABLE score CHARACTER SET GBK;
#修改表的字符集
```

```
ALTER TABLE score DROP Physics;
#删除列
```

#### 数据操作语言—DML

**update,insert,delete**

- 插入部分列

```sql
INSERT 
INTO score(id,NAME,English,Chinese,Math) 
VALUE(1,‘Hudie’,90,90,90);
```

- 插入所有列

```sql
INSERT INTO score VALUES(3,‘Shu’,80,80,80);
```

- 修改记录

```sql
UPDATE score set Chinese=99; –全表修改
UPDATE score SET Math=100 WHERE id=‘1’;
```

- 删除记录

```sql
DELETE FROM score WHERE id=‘2’;
DELETE FROM score;
```



#### 数据控制语言—DCL

数据控制语言DCL(grant,revoke)主要为用户授予和撤销权限

- 创建用户：CREATE USER 用户名@ip IDENTIFIED BY 密码;

```sql
create user Fox@localhost identified by ‘123456’;
```

- 给用户授权:GRANT 权限1,权限2,…,权限n   ON   数据库名.* TO 用户名@IP;

```sql
grant select,drop on mysql.* to Fox@localhost;
```

- 撤销权限:REVOKE 权限1，权限2，·····权限n     ON   数据库名.* TO 用户名@IP;

```
revoke select on mysql.* from Fox@localhost;
```

- 查看用户的权限:SHOW GRANTS FOR 用户名@IP

```
show grants for Fox@localhost;
```

- 删除用户

```
drop user Fox@localhost;
```

#### 数据查询语言—DQL

**SELECT**

关键字：

distinct

as

+-*/

like，

and，or

in /，not in  

between

order by

聚合函数

group by

limit

```sql
SELECT * FROM exam;
	--全表查询
	
SELECT DISTINCT Math FROM exam;
SELECT DISTINCT name,Math FROM exam;
	--过滤重复字段
	
SELECT NAME,English AS English_score 
FROM exam;
	--字段起别名（as可省略）
	
SELECT NAME,English,Chinese 
FROM exam 
WHERE NAME=‘张三’;
	--查询指定字段

SELECT id,NAME,English-20 AS _English FROM exam;
SELECT NAME,English+Math+Chinese FROM exam;
	--使用加减乘除
	
SELECT FROM exam WHERE NAME LIKE ‘张_’;
SELECT FROM exam WHERE NAME LIKE ‘%%’;
	--模糊查询

SELECT 
FROM exam 
WHERE English > 90 AND Chinese >90;

SELECT 
FROM exam 
WHERE English < 90 or Math >99;
	--and，or

SELECT FROM exam WHERE id=2 OR id=3 OR id=4;
SELECT FROM exam where id IN(2,3,4);
SELECT FROM exam where id not IN(2,3,4);
	--in，not in

SELECT 
FROM exam 
WHERE English BETWEEN 90 AND 100;
	--between···and
	
SELECT FROM exam ORDER BY Chinese ASC;
SELECT FROM exam ORDER BY Chinese DESC;
	--order by

<-- 如果英语成绩相同,按照汉语成绩降序排列 -->
SELECT 
FROM exam 
ORDER BY English DESC,Chinese DESC; 

SELECT SUM(English+Math+Chinese) FROM exam;
SELECT COUNT(id) FROM exam WHERE NAME IS NOT NULL;
SELECT MAX(English) FROM exam;
SELECT MIN(English) FROM exam;
SELECT AVG(English) FROM exam;
	--聚合函数	
```

- 关键字：group by，limit

```sql
	--查询每个部门的最高薪水,只有最高薪水大于15000的记录被显示
SELECT deptno,MAX(sal)AS max_sal 
FROM emp 
GROUP BY deptno 
HAVING max_sal>=15000;

	--查询每个部门的平均工资
SELECT deptno,AVG(sal) 
FROM emp 
GROUP BY deptno 
HAVING AVG(sal)>9000;

	--查看工资最高的前十个职员信息 （页数-1，）
SELECT *
FROM emp 
ORDER BY sal DESC LIMIT 0,10;
```

##### 单表查询

###### 1.DISTINCT用于剔除重复记录

```sql
select name, sal, bonus from emp;

select distinct bonus from emp; -- distinct用于剔除重复记录
```

###### 2.WHERE条件限定

WHERE子句后面跟的是条件，条件可以有多个，多个条件之间用连接词（or | and）进行连接。

WHERE子句查询语法：SELECT    列名称  | *    FROM 表名称 WHERE 列 运算符 值

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210720113308.png " ")

- 查询emp表中【总薪资(薪资+奖金)大于3500】的所有员工，显示员工姓名、总薪资
- ifnull(列名, 值)函数: 判断指定的列是否包含null值，如果有null值，用第二个值替换null值

```sql
select name, sal+bonus from emp
where sal+bonus > 3500;

select name, sal+ifnull(bonus,0) from emp
where sal+ifnull(bonus,0) > 3500;
```

- 注意查看上面查询结果中的表头，如何将表头中的 sal+bonus 修改为 "总薪资"使用as可以为表头指定别名（格式：**列名 as 别名**），另外as可省略

```sql
select name as 姓名, sal+ifnull(bonus,0) as 总薪资 from emp
where sal+ifnull(bonus,0) > 3500;

select name 姓名, sal+ifnull(bonus,0) 总薪资 from emp
where sal+ifnull(bonus,0) > 3500;
```

- 查询emp表中【薪资在3000和4500之间】的员工，显示员工姓名和薪资
- between···and 在...和...之间

```sql
select name,sal from emp
where sal>=3000 and sal<=4500;

select name,sal from emp
where sal between 3000 and 4500;
```

## Mysql 常见函数

### MYSQL Date 函数

#### CURDATE() 函数

`CURDATE() `函数返回当前的日期

例子1：

```sql
SELECT NOW(),CURDATE(),CURTIME()
```

结果类似：

|        NOW()        | CURDATE()  | CURTIME() |
| :-----------------: | :--------: | :-------: |
| 2021-08-02 08:00:00 | 2021-08-02 | 08:00:00  |

例子2：

```sql
CREATE TABLE Orders 
(
OrderId int NOT NULL,
ProductName varchar(50) NOT NULL,
OrderDate datetime NOT NULL DEFAULT CURDATE(),
PRIMARY KEY (OrderId)
)
```

{{< admonition  "注意">}}

OrderDate 列规定 CURDATE() 作为默认值

作为结果，当向表中插入行时，当前日期和时间自动插入列中，如：

```sql
INSERT INTO Orders (ProductName) VALUES ('Computer')
```

| OrderId | ProductName | OrderDate  |
| :-----: | :---------: | :--------: |
|    1    |  Computer   | 2021-08-02 |

{{< /admonition  >}}

#### DATE_FORMAT() 函数

DATE_FORMAT()  函数用于以不同的格式显示日期/时间数据。

语法：`DATE_FORMAT(date,format)`

- `date` 参数是合法的日期

- `format`：规定日期/时间的输出格式。

```sql
DATE_FORMAT(PERFOR_TIME,'%Y-%m-%d')=CURDATE()
```

#### DATE_SUB() 函数

DATE_SUB() 函数用于从日期减去指定的时间间隔

语法：`DATE_SUB(date,INTERVAL expr type)`

- *date* 参数是合法的日期表达式
- *expr* 参数是您希望添加的时间间隔
- type 参数可以是下列值：

![image-20210802165004339](https://gitee.com/cao-lianjie/pic-go/raw/master/img/image-20210802165004339.png " ")

示例：

假设有如下表

| OrderId | ProductName | OrderDate               |
| :-----: | :---------: | ----------------------- |
|    1    | 'Computer'  | 2021-08-29 16:25:46.635 |

现在，我们希望从 "OrderDate" 减去 2 天，我们使用下面的 SELECT 语句：

```sql
SELECT OrderId,DATE_SUB(OrderDate,INTERVAL 2 DAY) AS OrderPayDate
FROM Orders
```

结果：

| OrderId |      OrderPayDate       |
| :-----: | :---------------------: |
|    1    | 2021-08-27 16:25:46.635 |

### MYSQL CAST()函数

`CAST`函数:==将某种数据类型的表达式显式转换为另一种数据类型==

语法：CAST (expression AS data_type)

- expression：任何有效的SQLServer表达式
- AS：分隔两个参数，在AS之前的是要处理的数据，在AS之后是要转换的数据类型
- data_type：目标系统所提供的数据类型，包括bigint和sql_variant，不能使用用户定义的数据类型

|            数据类型            | data_type |
| :----------------------------: | :-------: |
| 二进制（同带binary前缀的效果） |  BINARY   |
|       字符型（可带参数）       |  CHAR()   |
|              日期              |   DATE    |
|              时间              |   TIME    |
|           日期时间型           | DATETIME  |
|              整数              |  SIGNED   |
|           无符号整数           | UNSIGNED  |







# 事务传播



- 事务的传播类型

MANDATORY

NEVER

NOT_SUPPORTED

SUPPORTS

REQUIRED（默认）

REQUIRES_NEW

NESTED

- 在某个业务类中有2个更新数据的方法，且都是事务性的，如果第2个方法调用第1个方法，会有几个事务？

Spring管理事务是基于接口进行代理，一个业务类产生一个代理对象，当调用的两个更新数据的方法来源于Spring管理的同一对象，则只会产生一个代理对象，只有一个事务，不存在事务的传播；

当两个方法来源于Spring管理的不同代理对象，则存在两个事务

情形一：

Spring管理事务是基于接口进行代理的，一个业务类产生一个代理对象，在调用`@Transactional`注解的方法之前就会开启事务，并在过程中决定是否回滚或最终提交！

```
开启事务

		执行update2()方法
			调用update1()方法
				
    因update1()方法抛出异常且符合回滚规则，执行回滚事务
    
若未出现回滚，则提交事务（本例会回滚，不会执行这一步）
```

由于update1()是在update2()内部调用的，不是由代理对象来调用,内部调用update1（）不存在事务性，只会在调用update2()方法时开启1个事务，内部调用的update1()根本不是事务性的（不管有没有@Transactional注解），既然只有1个事务，也就不存在事务的传播了！

情形二：

这一次也是在update2()中调用另一个事务性的方法，为什么就是有效的呢？是因为这次调用的是另一个对象的方法，而这个对象也是Spring的事务管理机制产生的代理对象，其执行过程大致是：

```
开启事务
		执行update2()方法（UserServiceImpl类的）
				更新id=2的数据，且成功
				
				开启新事务
						调用updateSuccessfully()方法（OrderServiceImpl类的）
				未出现回滚，则提交事务
				
				更新id=2000000的数据，且失败，执行回滚事务
若未出现回滚，则提交事务（本例会回滚，不会执行这一步）

```

总结：

- Spring管理事务是基于接口代理的；
- 当前类的方法之间的调用，并不存在事务的传播，被调用的方法之前是否添加@Transactional注解对结果没有影响；
- 不同类的方法之间的调用，对于被调用的方法，可以通过@Transactional注解的propagation属性来配置事务传播类型。
