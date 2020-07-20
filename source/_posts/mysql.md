---
title: mysql数据库
date: 2019-08-25 20:49:59
tags:  [mysql,数据库的增删改查,子查询,左连接,右连接,内连接]
categories: mysql
toc: true
---

[TOC]



###MySQL数据库简介

```PYTHON
MySQL是服务端，提供操作数据的服务
navicat是客户端，提供界面，先连接服务端，操作mysql的数据

连接服务端:MySQL必须是已经启动状态,需要ip，端口，用户名，密码
    
想在关系型数据库存数据，先有仓库，再有表，再存数据

设计数据库时的数据类型与约束

**数据类型**

- 整数：int，默认有符号（可以存负数），无符号（不能存负数），长度没有意思
- 小数：decimal，（5，3），整数占2位，小数点后占3位
- 字符串：varchar，一个数字或一个字母或一个标点符号或一个中文占一个字符
- 日期时间：datetime，格式：`2019-04-02 00:00:00`

**约束**

- 主键(primary key)：唯一的标识一条数据，如果某个字段设置为主键，这列值==唯一且不能为空==，通常一个表会有一个id字段，设置为主键，通常设置为自动递增（从1开始自动增长），设置为无符号

  id字段：主键，无符号的int，自动递增

- 非空：字段不允许为空，==不填写值，显示(null)，是空==，空字符串不是空

- 惟一(unique)：此字段的值不允许重复，sql语法再讲
- 默认值(default)：当不填写此值时会使用默认值，如果填写时以填写为准，给varchar或datetime字段设置默认值时，必须用英文引号
- 外键(foreign key)：维护两个表之间的关联关系


####  查询编辑器

某个仓库--查询—右键点击—新建查询

- 每一条sql语句结尾需要一个英文分号

- 注释sql语句：ctrl+/(windows);command+/或者# (mac)

  取消注释：ctrl+shift+/(windows),command+中/英+/(mac)
```

###数据库表的操作

```PYTHON
**创建表**

语法：

​```sql
create table 表名(
字段名 类型 约束,
字段名 类型 约束,
...
)
​```
例：创建学生表，字段要求如下：

姓名(长度为10)， 年龄，身高(保留小数点2位)

要一个主键字段：id，无符号的整数，主键，自动递增

​```sql
create table students3(
id int unsigned primary key auto_increment,
name varchar(10),
age int,
height decimal(5,2)
);
​```
**删除表**

语法：

​```sql
语法一：drop table 表名

语法二：drop table if exists 表名
​```

例：删除学生表

​```sql
drop table students;
如果表不存在，会报错

drop table if exists students2;
如果表不存在，不会报错
​```
**数据操作-增删改**
###增

####添加一行数据

语法一：所有字段设置值，==值的顺序与表中字段的顺序对应==
insert into 表名 values(值1,值2,...)
主键列是自动增长，插入时需要占位，通常使用0或者 default 或者 null 来占位

语法二：部分字段设置值，值的顺序与给出的字段顺序对应
insert into 表名(字段1,字段2) values(值1,值2,...)


###添加多行数据

语法一：写多条insert语句，语句之间用英文分号隔开

​```sql
insert into students3 values(null,'亚瑟5',12,123.1);

insert into students3(name) values('鲁班5');

insert into students3(age,name) values(22,'鲁班5');
​```

语法二：写一条insert语句，设置多条数据，数据之间用英文逗号隔开

​```sql
insert into students3 values(null,'亚瑟51',12,123.1),
(null,'亚瑟52',12,123.1),(null,'亚瑟53',12,123.1);

**改**

语法：update 表名 set 字段=值,字段2=值2 where 条件

例：修改id为5的学生数据，姓名改为 狄仁杰，年龄改为 20
update students3 set name='狄仁杰',age=20 where id=5;
注意：如果不写where，会修改所有行的数据

**删**

语法一：delete from 表名 where 条件

例：删除id为6的学生数据
delete from students3 where id=6;
注意：如果不写where，会删除所有行

语法二：删除表的所有数据，保留表结构

truncate table 表名
例：删除学生表的所有数据
truncate table students3_copy1;


**Truncate和Delete、Drop的区别**

1、Delete删除数据时，即使删除所有数据，其中的自增长字段不会从1开始

2、Truncate删除数据时，其中的自增长字段恢复从1开始

3、Drop是删除表，所有数据和表结构都删掉

**总结**

在速度上，drop > truncate > delete

如果想删除部分数据用delete，注意带上where子句

如果想删除表，用drop

如果想保留表而将所有数据删除，自增长字段恢复从1开始，用truncate

```

###查询相关的操作

#### 条件查询

```PYTHON

语法：select * from 表名 where 条件（条件是过滤行，格式：字段 符号 值）

**比较运算符**：字段=值，字段>值,字段<值,字段!=值,字段<>值;

**逻辑运算符**:
and：且，多个条件同时成立
 or：或，多个条件成立一个即可
 not：非，对某个条件取反


**模糊查询**
字段 like 值
% 代表任意个字符,_ 代表一个字符

例1：查询姓孙的学生
select * from students where name like '孙%';

例2：查询姓孙且名字是一个字的学生
select * from students where name like '孙_'; 

**范围查询**---in 

例1：查询家乡是北京或上海或广东的学生
select * from students where hometown in('北京','上海','广东');

 between 值1 and 值2 ，==值1<=值2==
例2：查询年龄为18至20的学生
select * from students where age between 18 and 20;


**空判断**

- (null)是空
- ''是空字符串
- 字段 is null

例1：查询没有填写身份证的学生

select * from students where card is null;

查询身份证为空字符串的学生
select * from students where card='';

例2：查询填写了身份证的学生
select * from students where not card  is  null;

```

####查询字段

```PYTHON
*查询所有字段**
语法：select * from 表名

*查询部分字段**
语法：select 字段名1,字段名2 from 表名
```

#### 起别名

```PYTHON
1.给表起别名，在多表查询中经常使用
语法：select 别名.字段名1,别名.字段名2 from 表名 as 别名

2.给字段起别名
语法：select name as 别名,sex as 别名,age from students;
```

####去重

```PYTHON
语法：select distinct 字段 from 表名
例：查询所有学生的性别，不显示重复的数据

select distinct sex from students;
注意：什么是重复数据，在显示的结果中，如果一行记录和另一行完全一致，才是重复数据
```

#### 排序

```PYTHON
语法：
select * from 表名 order by 字段 asc或desc 
- asc从小到大排列，即升序
- desc从大到小排序，即降序

例1：查询所有学生信息，按年龄从小到大排序
select * from students order by age asc;
select * from students order by age;
默认是升序

例2：查询所有学生信息，按年龄从大到小排序，年龄相同时，再按学号从小到大排序

select * from students order by age desc,studentno;
当按照多个字段排序时，先按第一个字段排序，当第一个字段的值相同时，再按第二个字段排序

默认排序只能排英文和数字，对中文字段排序需要用到convert函数

​```sql
select * from students order by convert(name using gbk);
​```
```

#### 聚合函数

```PYTHON
为了快速得到统计数据，有5个聚合函数:count，max，min，sum，avg


例1：查询学生总数
select count(*) from students;
count()，要么写*，要么写一个字段，如果count(字段)，不会统计为null的数据

例2：查询女生的最大年龄
select max(age) from students where sex='女';

例3：查询1班的最小年龄
select min(age) from students where class='1班';

例4：查询北京学生的年龄总和
select sum(age) from students where hometown='北京';

例5：查询女生的平均年龄
select avg(age) from students where sex='女';

查询所有学生的最大年龄、最小年龄、平均年龄
select max(age),min(age),avg(age) from students;

```

#### 分组

```PYTHON
按照字段分组，此字段相同的数据会被放到一个组中，==目的是对每一组的数据进行统计(聚合函数)==

语法：
select 字段,聚合 from 表名 group by 字段

例1：查询各种性别的人数
select sex,count(*) from students group by sex;

注意：按照哪个字段分组，select后面就只能写那个字段再加上聚合函数

```

#### 分组后的数据筛选

```PYTHON
语法：select 字段,聚合 from 表名 group by 字段 having 条件
例1：查询男生总人数

select count(*) from students where sex='男';

select sex,count(*) from students group by sex having sex='男';

having是对分组后得到的结果，再进行过滤

*对比where与having**

1.where是对from后面指定的表进行数据筛选，属于对原始数据的筛选
2.having是对group by的结果进行筛选
3.having后面的条件中可以用聚合函数，where后面不可以
```

#### 获取部分行

```PYTHON
语法：select * from 表名 limit 起始位置,个数
例1：查询前3行学生信息
select * from students limit 0,3;
select * from students limit 3;
省略起始位置，起始位置是0

```

#### SQL语句的书写顺序

```PYTHON
select *,字段名 as 别名,聚合  ⑥
from 表1  ①
inner|left|right join 表2 on 表1.字段=表2.字段  ②
where 条件  ③
group by 字段 having 条件(聚合)  ④
order by 字段 asc 或 desc  ⑤
limit  ⑥
```

#### 分页

```PYTHON
语法：select * from 表名 limit 起始位置,数量
​```

已知：每页显示3条数据，求：显示每一页的sql语句
查询表的数据的数量
select count(*) from students;
计算共显示多少页
12/3=4页
13/3=4+1页

-- 第一页
select * from students limit 0,3;
-- 第二页
select * from students limit 3,3;
-- 第三页
select * from students limit 6,3;
-- 第四页
select * from students limit 9,3;
​```
```

#### 连接查询

```PYTHON
概念：当查询结果的列来源于多张表时，需要将多张表连接成一个大的数据集，再选择合适的列返回

**内连接**：只把匹配成功的数据连接起来
语法1：select * from 表1 inner join 表2 on 表1.字段=表2.字段；
语法2：select * from 表1,表2 where 表1.字段=表2.字段；

多表的内连接查询：
select * from 表1 inner join 表2 on 表1.字段=表2.字段
前面连接后得到一个结果
inner join 表3 on 表3.字段=表1.字段
inner join ...
多表连接后的结果中，可能有重名的字段，如果用到了重名的字段，必须加表名


** 左连接**：查询的结果为两个表匹配到的数据加左表特有的数据
语法：select * from 表1 left join 表2 on 表1.列=表2.列
left join 前面的表是左表,左表在右表中找不到对应的数据用null填充


**右连接**：查询的结果为两个表匹配到的数据加右表特有的数据
语法：select * from 表1 right join 表2 on 表1.列=表2.列；
right join 后面的表是右表，右表在左表中找不到对应的数据用null填充

**自关联**：是连接查询的一种应用，对同一个表查询多次，把多次查询的结果连接起来
语法：select * from 表1 inner join 表1 on 表1.字段=表1.字段
例1：查询河南省的所有城市
select * from areas as a1
inner join areas as a2 on a1.aid=a2.pid
where a1.atitle='河南省';
注意：自关联必须对表起别名
应用场景：数据之间有上下级关系，用一个表存储
```

#### 子查询

```PYTHON
语法：select ...(select ...);

子查询是辅助主查询的,要么充当条件,要么充当数据源；
子查询是可以独立存在的语句,是一条完整的select语句；


##子查找充当条件
例1：查询大于平均年龄的学生

查平均年龄
select avg(age) from students;
21.5833
查询大于平均年龄的学生
select * from students where age>21.5833;

select * from students where age>(select avg(age) from students);

##子查询充当数据源：必须给子查询返回的结果且别名

例5：查询数据库和系统测试的课程成绩
先过滤，只要'数据库','系统测试'
select * from 
(select * from courses where  name in ('数据库','系统测试')) as temp
inner join scores on temp.courseno=scores.courseno

```

#### 数据库高级用法

```PYTHON
#### 1.1 数据库设计

**E-R模型**
 E表示entry，实体：一个数据对象，描述具有相同特征的事物，一个表
R表示relationship，联系：表示一个或多个实体之间的关联关系，关系的类型包括包括一对一、一对多、多对多

**关系也是一种数据，需要通过一个字段存储在表中**

一对一：常用的数据不常用数据的编号

一对多：多的一方记录编号

多对多：创建中间表记录编号

#### 1.2 命令行客户端

- 连接服务端

方式一：所有程序中--MySQL command line client

方式二：找到命令行客户端的路径，

C:\Program Files (x86)\MySQL\MySQL Server 5.1\bin\mysql.exe

`"C:\Program Files (x86)\MySQL\MySQL Server 5.1\bin\mysql.exe" -uroot -p`

- 操作数据库
1.查看所有数据库:show databases

2.使用数据库:use 仓库名

3.查看当前使用的数据库:select database()

4. 创建数据库:create database 仓库名 charset=utf8

5.删除数据库:drop database 仓库名

6.操作数据表

  查看当前数据库中所有表:show tables

  查看表结构:desc 表名

  查看表的创建语句:show create table 表名

   如果中文乱码，`set charset gbk;` ;是sql语句的分隔符，遇到;时才会执行前面的语句

- 备份与恢复

以管理员身份运行cmd程序

备份
mysql dump -uroot -p ceshidb12>ceshidb12.sql

恢复
mysql  -uroot -p  ceshibak<ceshidb12.sql

#### 1.3 内置函数

- 字符串函数

  1.拼接字符串concat

  select concat(123,'abc',89);
  
  select name,hometown,concat(name,'的家乡是',hometown) from students;


  - 包含字符个数length

  select length('我');中文长度是3
  
  select * from students where length(name)=9;

  - 截取字符串
    - left(str,len)返回字符串str的左端len个字符
    - right(str,len)返回字符串str的右端len个字符
    - substring(str,pos,len)返回字符串str的位置pos起len个字符

 	 select left('abc',1);
  	select right('abc',1);
  	select substring('abc',2,2);
  
  	select name,concat(left(name,1),'xx') from students;


  - 去除空格
    ltrim(str)返回删除了左空格的字符串str
    rtrim(str)返回删除了右空格的字符串str

  select ltrim('  abc  ');
  select rtrim('  abc  ');
  select rtrim(ltrim('  abc  '));
```

  - 大小写转换，函数如下
    lower(str)
    upper(str)

  select lower('aBa');
  select upper('aBa');
  ```

- 数学函数

  - 求四舍五入值round(n,d)，n表示原数，d表示小数位置，默认为0

  select round(1.56,1);
  
  select round(avg(age)) from students;

  - 求x的y次幂pow(x,y)

  select pow(2,4);


  - 获取圆周率PI()

  select PI();

  - 随机数
    rand()==，值为0-1.0的浮点数
  随机在一个表中取一条记录
  select * from students order by rand() limit 1;

- 日期时间函数

  - 当前日期current_date()
  - select current_time()
  - 当前日期时间now()
  - 日期格式化date_format(date,format)

  select date_format('2019-04-28 15:02:28','%Y年%m月%d日 %H时%i分%s秒')


#### 1.4 流程控制

case语法：
case 值 when 比较值1 then 结果1 when 比较值2 then 结果2 ... else 结果 end

select name,sex,case sex when '男' then concat(left(name,1),'帅哥') when '女' then concat(left(name,1),'美女') else concat(left(name,1),'xx') end as tmp from students;

#### 1.5 自定义函数

语法：create function 函数名称(参数列表) returns 返回类型 begin sql语句 end


例：create function my_trim(str varchar(100)) returns varchar(100) begin return ltrim(rtrim(str));
end

使用：select my_trim('  abc  ')


delimiter的作用是把命令行中默认的分隔符;改成其他的符号

#### 1.6 存储过程

语法：create procedure 存储过程名称(参数列表) begin sql语句 end
例：create procedure proc_stu() begin select * from students;end

使用：call proc_stu;

- 存储过程和函数都是为了可重复的执行操作数据库的 sql 语句的集合.
- 存储过程和函数都是一次编译,就会被缓存起来,下次使用就直接命中缓存中已经编译好的 sql, 不需要重复编译
- 减少网络交互,减少网络访问流量

#### 1.7 ==视图==

语法：create view 视图名 as select...

例：create view v_sss as select stu.*,cs.courseNo,cs.name courseName,sc.score
from students stu
inner join scores sc on stu.studentNo = sc.studentnum
inner join courses cs on cs.courseNo = sc.courseNo;

注意：创建视图时，select语句返回的结果不能有重复的字段

使用：select * from v_sss;
作用：视图的用途就是查询，存在于服务端，可以重复使用，节省流量

- 查看视图：查看表会将所有的视图也列出来
show tables;

- 删除视图
drop view 名称

#### 1.8 事务

所谓事务,它是一个操作序列，这些操作要么都执行，要么都不执行

- 全部成功

1、开启事务：begin

2、多个操作都成功

大乔给小乔转5岁
update students set age=age-5 where name='大乔';

update students set age=age+5 where name='小乔';

3、提交事务：commit

- 全部失败

1、开启事务：begin

2、多个操作有一个失败

大乔给小乔转5岁
update students set age=age-5 where name='大乔';

update students set age=age+5 where nama='小乔';

3、回滚：rollback

#### 1.9 索引

提升查询的速度，降低更新表的速度

1.查看索引：show index from 表名
2.创建索引
 方式一：建表时创建索引
	create table create_index2(id int primary key,-- 如果字段是主键或唯一，会自动创建索引
	name varchar(10) unique,-- 唯一约束
	age int,
	key (age) -- 创建索引）；

索引作用在某一列数据，如果name字段有索引，下面的语言效果高

select * from student where name=''

  方式二：对于已经存在的表，添加索引
create index 索引名称 on 表名(字段名称(长度))
create index name_i on create_index(name(10));
create index age_i on create_index(age);


3.删除索引：

drop index 索引名称 on 表名

#### 1.10 外键

一个表a的字段aa，被另一个b的bb字段约束

语法

方式一：创建数据表的时候设置外键约束
foreign key(自己的字段) references 主表(主表字段)

例：create table class(id int unsigned primary key auto_increment,name varchar(10));

create table stu(name varchar(10),class_id int unsigned,foreign key(class_id) references class(id));

方式二：对于已经存在的数据表设置外键约束

alter table 从表名 add foreign key (从表字段) references 主表名(主表字段);

例：alter table stu add foreign key(class_id) references class(id);

查看外键：show create table 表名


例：
CREATE TABLE `stu` (
  `name` varchar(10) DEFAULT NULL,
  `class_id` int(10) unsigned DEFAULT NULL,
  KEY `class_id` (`class_id`),
  CONSTRAINT `stu_ibfk_1` FOREIGN KEY (`class_id`) REFERENCES `class` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8
​```

删除外键：alter table 表名 drop 
foreign key 外键名称;

外键的缺点：降低表更新的效率
  ```

#### 重置MYSQL密码

```PYTHON
**修改密码**
1、连接上mysql，操作mysql仓库

2、修改密码，密码存在user表中
update user set password=password('321');

加密是不可逆

3、刷新权限，让密码生效
flush privileges;

8.0版本直接运行下面命令
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你的新密码'

**忘记 root 账户密码怎么办**

重置密码
1、找到配置文件
C:\Program Files (x86)\MySQL\MySQL Server 5.1\my.ini

[mysqld]
skip-grant-tables

重启mysql服务

2、按照前面的内容设置一个新密码

3、还原配置文件，重启mysql服务

8.0配置文件路径
C:\ProgramData\MySQL Server 8.0

**操作日志**
1、查询日志功能是否启用
show variables like 'general%';

2、启用日志
set global general_log=1;

3、操作数据库，日志文件会发生变化

4、关闭日志
set global general_log=0;

#### 1.1 NoSQL

非关系型数据库的统称

- 不用sql语言
- 不用表存储数据
- 性能高

#### 1.2 Redis

- key-value存数据
- 性能高
>启动redis时，加载硬盘的数据到内存，
>定时把内存中的新数据保存到硬盘

## 2. 服务端与客户端

- 服务端操作

  - 启动:redis-server

  - 停止:ctrl+c

  - 如果把启动redis的窗口关闭:ps -aux | grep 'redis';kill 3892

- 客户端操作

  - 连接服务端
	redis-cli
	redis-cli --raw(如果中文乱码用)

  - 停止:ctrl+c

  - 切换数据库

  不能创建仓库，默认有16个仓库，通过0-15来标识

  select 数字 刚连接上服务端时，进入的是0仓库

## 3. key-value

键值对

键的名称唯一，不能重复，用字母数字和下划线

值的类型有5种，string，hash，list，set，zset

## 4. string

字符串

- string是redis最基本的类型
- 最大能存储512MB数据
- string类型是二进制安全的，可以存储任何数据，比如数字、图片等

**增加、修改**

- 设置键值
- 如果设置的键不存在则为添加，如果设置的键已经存在则修改

语法：`set key value`

例1：设置键为'user1'值为'wzj'的数据

`set user1 wzj`

- 设置键值及过期时间，以秒为单位

语法：`setex key 秒 value`

例2：设置键为'user2'值为'lb'过期时间为8秒的数据

`setex user2 8 lb`

- 设置多个键值

语法 ：`mset key1 value1 key2 value2 ...`

例3：设置键为'user4'值为'xq'、键为'user5'值为'dq'、键为'user6'值为'zgl'、键为'user7'值为'bq'的数据

`mset user4 xq user5 dq user6 zgl user7 bq`

- 追加值，如果键不存在，新建一个键值对

语法：`append key value`

例4：向键为user1中追加值' haha'

`append user1 haha`



**获取**

- 获取：根据键获取值，如果不存在此键则返回nil

语法：`get key`

例5：获取键'user1'的值

` get user1000`

- 根据多个键获取多个值

语法：`mget key1 key2 ...`

例6：获取键'user3'、'user4'、'user5'、'user6'的值

`mget user3 user4 user5 user6`



string没有删除命令

## 5. 键命令

- ==查找键==，参数支持正则表达式

语法：`keys 表达式`

例1：查看所有键

`keys *`

例2：查看名称中包含a的键

`keys *a*`

*任意个字符，?一个字符

- 判断键是否存在，如果存在返回1，不存在返回0

语法：`exists key1 key2 ...`

例3：判断键'user1'、'user2'是否存在

`exists user1 user2`

- 查看键对应的value的类型

语法：`type key`

例4：查看键'user1'的值类型，为redis支持的五种类型中的一种

`type user1`

- ==删除键==及对应的值

语法：`del key1 key2...`

例5：删除键'user3'、'user4'、'user5'、'user6'

`del user3 user4 user5 user6`

- 设置过期时间，以秒为单位

语法：`expire key 秒`

例6：设置键'user1'的过期时间为10秒

`expire user1 10`

- 查看有效时间，以秒为单位

语法：`ttl key`

例7：查看键'user7'的有效时间

`tll user7`

-1代表永不过期 ，-2代表过期或不存在

## 6. hash

哈希

- hash用于存储键值对集合
- 值的类型为string
- 键可以理解为属性，一个属性对应一个值

**增加、修改**

- 设置单个属性

语法：`hset key 属性 值 `

例1：设置键'huser1'的属性'name'为'lb'

`hset huser1 name lb`

- 设置多个属性

语法：`hmset key 属性 值 属性2 值2`

例2：设置键'huser2'的属性'name'为'wzj'、属性'gender'为'nv'、属性'birthday'为'2017-1-1'

`hmset huser2 name wzj gender nv birthday 2017-1-1`



**获取**

- 获取指定键所有的属性

语法：`hkeys key`

例3：获取键'huser2'的所有属性

`hkeys huser2`

- 获取一个属性的值

语法：`hget key 属性 `

例4：获取键'huser2'属性'name'的值

`hget huser2 name`

- 获取多个属性的值

语法：`hmget key属性 属性2 `

例5：获取键'huser2'属性'name'、'gender'、'birthday'的值

`hmget huser2 name gender birthday`

- 获取所有属性的值

语法：`hvals key`

例6：获取键'huser2'所有属性的值

`hvals huser2`

例7：获取键'huser2'所有属性和所有值

`hgetall huser2`



**删除**

- 删除属性，属性对应的值会被一起删除

语法：`hdel key 属性1 属性2`

- 例8：删除键'huser2'的属性'gender',name

`hdel huser2 gender name`

如果所有属性都被删除，整个键值对被删除

## 7. list

链表

- 链表中存的数据类型为string
- 按照添加的顺序排序，从左往右的顺序
- list是双向链表

**增加**

- 在左侧插入数据

语法：`lpush key 值1 值2`

例1：从键为'luser1'的列表左侧加入数据'dq'、'xq'

`lpush luser1  dq xq`

- 在右侧插入数据

语法：`rpush key 值1 值2`

例2：从键为'luser1'的列表右侧加入数据'lb'、'zf'

`rpush  luser1  lb zf`

- 在指定元素的前或后插入新元素

语法：`linsert key before或after 现有值 新值`

例3：在键为'luser1'的列表中元素'lb'前加入'wzj'

`linsert luser1 before lb wzj`

**获取**

- 返回列表里指定范围内的元素
  - start、stop为元素的下标索引
  - 索引从左侧开始，第一个元素为0
  - 索引可以是负数，表示从尾部开始计数，如-1表示最后一个元素

语法：`lrange key start stop`

例4：获取键为'luser1'的列表所有元素

`lrange luser1 0 -1`

**修改**

- 设置指定索引位置的元素值
  - 索引从左侧开始，第一个元素为0
  - 索引可以是负数，表示尾部开始计数，如-1表示最后一个元素

语法：`lset key 位置 新值`

例5：修改键为'luser1'的列表中下标为1的元素值为'kai'

`lset luser1 1 kai`

**删除**

- 删除指定元素
  - 将列表中前count次出现的值为value的元素移除
  - count >0: 从头往尾移除
  - count <0: 从尾往头移除
  - count = 0: 移除所有

语法：`lrem key count value`

例6.2：从'luser2'列表右侧开始删除2个'h0'

`lrem luser2 0 h0`

## 8. set

==无序==集合

- 元素为string类型
- 元素具有==唯一==性，不重复
- 说明：对于集合没有修改操作

**增加**

- 添加元素

语法：`sadd key 值1 值2`

例1：向键'suser1'的集合中添加元素'dq'、'xq'、'lb'

`sadd suser1 dq xq lb`

**获取**

- 返回所有的元素

语法：`smembers key`

例2：获取键'suser1'的集合中所有元素

`smembers 'suser1'`

**删除**

- 删除指定元素

语法：`srem key 值`

例3：删除键'suser1'的集合中元素'xq'

`srem suser1 xq`

## 9. zset

==有序==集合

- 元素为string类型
- 元素具有==唯一==性，不重复
- 每个元素都会关联一个分数，分数可以为负数，通过分数将元素从小到大排序
- 说明：没有修改操作

**增加**

- 添加

语法：`zadd key 分1 值1 分2 值2`

例1：向键'zuser1'的集合中添加元素'dq'、'xq'、'lb'、'bq'，分数分别为1、5、8、3

`add zuser1 1 dq 5 xq 8 lb 3 bq`

如果值存在，可以修改那个值的分数

**获取**

- 返回指定范围内的元素
  - start、stop为元素的下标索引
  - 索引从左侧开始，第一个元素为0
  - 索引可以是负数，表示从尾部开始计数，如-1表示最后一个元素

语法：`zrange key start stop`

例2：获取键'zuser1'的集合中所有元素

`zrange 'zuser1' 0 -1`

- 返回score值在min和max之间的元素

语法：`zrangebyscore key 低分 高分`

例3：获取键'zuser1'的集合中分数在4和9之间的元素

`zrangebyscore zuser1 4 9`

- 返回成员member的score值

语法：`zscore key 值`

例4：获取键'zuser1'的集合中元素'lb'的分数

`zscore zuser1 lb`

**删除**

- 删除指定元素

语法：`zrem key 值1 值2`

例5：删除集合'zuser1'中元素'dq'

`zrem zuser1 dq`

- 删除分数在指定范围的元素

语法：`zremrangebyscore key 低分 高分`

例6：删除集合'zuser1'中分数在4、9之间的元素

`remrangebyscore zuser1 4 9`
```

# [mysql忘记密码解决方法](https://junconec.github.io/2019/07/23/mysql/)

mysql 解决忘记密码问题

mac下mysql 1045 (28000): Access denied for user ‘root’@’localhost’ (using password:

新入了mac pro，安装好mysql后，用终端进入mysql遇到个问题： 1045 (28000): Access denied for user ‘root’@’localhost’ (using password: N

讲道理，我还设密码呢，但是第一次进来就报错，goo了一下大概原因可能是mysql创建的时候给自动分配了密码。

不管分配没分配密码，反正一般的解决方法就是：先跳过验证，再重设密码。

具体步骤：

1. 先关闭MySQL服务；
   执行

   sudo /usr/local/mysql/support-files/mysql.server stop

或者在系统偏好设置中关闭MySQL服务(如果电脑有设置密码的，此处会要求输入计算机密码)

2.去mysql文件夹里设置跳过验证（3步）

```
先进入mysql文件夹：
cd /usr/local/mysql/bin/



设置权限，如果电脑有设置密码（开机和解锁计算机时要求输入的那个密码），在输入此句后会要求输入密码。输入密码后按回车确认
sudo su

跳过验证
./mysqld_safe --skip-grant-tables &
```

3.开始设置我们自己的新密码

打开一个新的终端，输入

```
/usr/local/mysql/bin/mysql -u root -p
```

然后会要求输入密码，因为此时根本没有密码，所以直接点确认，显示以下信息表示成功进入mysql(与windows系统一样)

```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 20
Server version: 5.7.11

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```

现在设置新密码，注意要打引号：

```
UPDATE mysql.user SET authentication_string=PASSWORD('cc77') where User='root';
```

回车确认，显示以下信息表示修改密码成功

```
Query OK, 1 row affected, 1 warning (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 1
```

然后刷新一下，让上述修改生效：

```
flush privileges;
```

刷新成功会显示以下信息：

```
Query OK, 0 rows affected (0.01 sec)
```

4.重启mysql,用新密码登录，可以登录成功了。但是进行其他mysql操作，会显示：

ERROR 1820 (HY000) :You must reset your password using AlTER USER statement before executing this statement.

意思是还要再重设一遍密码，直接输入：

```
SET PASSWORD = PASSWORD('cc77');
```

修改成功后，终端会显示：

```
Query OK, 0 rows affected, 1 warning (0.01 sec)
```

至此，修改密码彻底完成，可以做任何相关sql操作了





