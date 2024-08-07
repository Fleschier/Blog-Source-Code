---
layout:     post
title:      "数据库SQL语句"
date:       2018-04-7 20:55:00
categories: Computer Programs
tags: ๑SQL
description: "学习记录"
---

> 不适合人类阅读的学习笔记

- **数据库的命令语句均不区分大小写**

## 创建语句
---

### 基本创建

- 创建数据库 ：`create database XXX`

- 带详细参数的数据库创建：
```
create database School on(
	name = 'School_data',
	filename = 'c:\data\School_data.mdf',
	size = 5mb,
	filegrowth = 1mb --每次增长的大小
)
```

- 创建表： `create table XXX`

- 带属性的创建：
```
create table student(
	Sno char(6) primary key,
	Sname varchar(8),
	Ssex char(2),
	Sage smallint,
	Sdept varchar(15)
)
```

- 更加复杂的创建：
```
create table student(
	Sno char(6) primary key,  --主键
	Sname varchar(8) not null constraint ck_1 unique, --创建时加入约束条件
	Ssex char(2) not null constraint ck_2 check(Ssex in('男','女')),
	Sage smallint constraint ck_3 check(sage>16),
	Sdept varchar(15) default 'JSJ'  --默认值
)
create table course(
	Cno char(6) primary key,
	Cname varchar(20),
	Cpno char(4),
	Ccredit tinyint
)
create table SC(
	Sno char(6) not null, --要在表外添加主键的约束，则这个属性不能为空
	Cno char(6) not null,
	Grade decimal(12,1) constraint ck_6 check(Grade <= 100 and Grade >=0)
	constraint fk_1 foreign key (Sno) references student(sno)
)
alter table SC add constraint PK_SC primary key(Sno,Cno)
```
check语句是一种约束条件写法，与constraint功能类似

- 在创建时设置foreign key：
```
create table sc(
	Sno char(6),
	Cno char(4),
	Grade decimal(12,2),
	primary key(Sno,Cno),
	foreign key(Sno) references student(Sno),
	foreign key(Cno) references course(Cno)
)
```

### 创建索引

```
create index Ix_student_sname on student(Sname)
create index Ix_student_sdept on student(Sdept)
create index Ix_sc_cno on SC(Cno)
create index Ix_course_cname on Course(Cname)
sp_help student  --查看索引等信息
drop index student.ix_student_sname    --删除索引
```

### 插入数据：
>数据顺序和类型要与创建时的定义一致

```
insert into student values('5001','赵强','男','20','SX')
insert into student values('5002','李丽华','女','21','JSJ')
insert into student values('5001','李静','女','20','SX')
```
### 将数据从一个表插入另一个表

```
--批量插入数据(从student 到 sc_name)
insert into sc_name (Sno,Sname,Ssex)
select Sno,Sname,Ssex from student where Sdept = 'SX'
```


## 在表外的更改操作
---

### 在表外更改表结构

```
create table student(
	Sno char(6),
	Sname varchar(8),
	Ssex char(2),
	Sage smallint,
	Sdept varchar(15)
)
alter table student add address varchar(60) --添加列
alter table student add inDate datetime --添加列，数据类型为datetime
alter table student alter column adress varchar(50)
alter table student drop column inDate
```

### 用户自定义完整性约束

```
alter table student add constraint cs_1 check(Ssex in ('男','女'))
alter table student add constraint cs_2 check(Sage >16)
alter table Course add constraint cs_3 check(Ccredit in (0,1,2,3,4,5))
alter table Course add constraint cs_4 check(Cno != Cpno)
```

- 删除约束： `alter table student drop constraint cs_1`

### 更新表数据

- 使用update和查找条件： `update student set Sno = 4018 where Sno = 4003`

## 获取详细信息
---

- `sp_help 表名`

- `sp_helpdb 数据库名`

## 查询语句
---
### 基本查询操作

- `select [列名（逗号间隔）或者*] from 表名`

### 进阶(单表)

```
select Sno,Sname,Sage from student
where Sage >= 19 and Sage <= 21 and Ssex = '女' order by Sage desc
-- desc表示降序，asc表示升序
```

```
select Sno,Ssex from student where Sname like '_明%'  
--'_'表示一个字符，%表示任意多个字符,这里筛选出名字第二个字为‘明’的人
```

```
select Sno,Cno from SC where Grade is null
-- 如果用'= null'则查询结果为空
```

```
select Sno,Cno,cast((Grade/10) as int)from SC
-- cast(a as int)转换数据类型
```

```
select distinct Sdept from student
-- distinct写在最前面
```

### 进阶（统计）

```
select count(*) as number from student
where Sname like '%明%'
-- 统计名字有‘明’的人数
```

```
select Cno,sum(Grade) as total_grade,avg(Grade) as avg_grade,max(Grade) as max_grade,min(Grade) as min_grade from SC  
group by Cno
order by avg_grade desc
-- sum()求和
```

```
select Cno from SC
where Grade >= 85
group by Cno
having count(Sno)>10
-- where 筛选必须在group 之前，group之后可以用having筛选，两者可以并用
```

```
select Sno from SC
where Grade <60  
group by Sno
having count(Cno) > 2
```
### 进阶（连接）

```
select distinct Cno from student,SC
where student.Sno = SC.Sno and Sdept = 'JSJ'
-- 连接要写出连接条件
```

```
-- 三种写法
select Sname from student,SC
where student.Sno = SC.Sno and Cno = 1002
XXXXXX
select Sname from student
join SC on student.Sno = Sc.Sno
where Cno = 1002             -- JOIN..ON..语句
XXXXXX
select Sname from student
where Sno in(                --嵌套执行
	select Sno from SC where Cno = 1002
)
```

```
select student.Sno, Grade from student,course,SC
where student.Sno = SC.Sno and course.Cno = SC.Cno and Cname = '数据库原理' and Grade <60
--用表名.列名来获取具有相同列名的几个表中某个表的某一列
```

```
-- 两种写法
select student.Sname from student,SC
where student.Sno = SC.Sno and Grade >= 80 and Cno = 1004
XXXXXX
select Sname from student
where Sno in(                --嵌套写法
	select Sno from SC where Grade > 80 and Cno in(
		select Cno from course where Cname = '数据库原理'
	)
)
```
###

### 进阶（嵌套）

```
-- 找出平均成绩最大的一个（两种写法）
select  top 1 Sno,avg(Grade) as avg_grade from SC
group by Sno
order by avg(Grade) desc
XXXXXX
select Sno,avg(Grade) as avg_grade from SC
group by Sno
having avg(Grade) >= all(select avg(Grade) from SC group by Sno)
```

## 删除
---

- 删除表： `drop table XXX`

- 删除表中的内容： `delete from XXX`

- 删除数据库： `drop database XXX`

- 删除依赖： `drop constraint XXX`

## 补充
---

### 循环生成数据
```
--生成大量数据
create procedure usp_makedata as
declare @nCnt int, @sNo char(6), @sname varchar(8)
set @nCnt = 12000 --counter
while @nCnt <999999
begin
	set @nCnt = @nCnt +1
	set @sNo = convert(varchar(6),@nCnt)
	set @sName = '张' +@sno
	insert into student (sno,sname,ssex,sage) values (@sno,@sname,'男',20)
end
return
exec usp_makedata	--执行生成过程
```
### 测试生成的数据
```
--生成测试
create procedure usp_test as
declare @nCount int ,@data int
set @nCount=0
while @nCount <100
begin
	select @data = count(*) from student
	where sname <'张3800' or sname >'张8800'
	set @nCount =@nCount + 1
end
exec usp_test --执行测试
```
### 善后
```
drop procedure usp_makedata
drop procedure usp_test
```
## E-R图的画法
---

- 实体型(Entity)：用矩形表示，矩形框内写明实体名

- 属性(Attribute)：用椭圆形表示，并用无向边将其与相应的实体连接起来

- 联系(Relationship)：用菱形表示，菱形框内写明联系名，并用无向边分别与有关实体连接起来，同时在无向边旁标上联系的类型(1 : 1，1 : n或m : n)。 (一对一，一对多还是多对多)

- 图例：
![](/images/SQL/E-R graphe.png)

- 示例：
![](/images/SQL/TIM图片20180503210911.jpg)
画图时先画实体型和联系，最后添加属性即可。对于那些有公共属性的两个实体型，属性应当连到联系上(菱形上的属性)

### 从 E-R图转为关系模式：

- 首先是看有几个实体，每个实体单独存放为一个关系，即表。**每个表的字段包含了这个实体所有的属性，即括号内的内容**

- 然后分析实体间的联系。实体间联系有的要单独存一个表，有的不要。

- **如果实体和实体间是多对一或者一对一的关系则不需要单独创建一个表，而是通过在参与联系的多方实体中，增加一个参与联系的1方的实体的主键作为一列来表示联系**。例如，车队和车辆是一对多的关系，这里 **多** 是车辆这个实体，1是车队这个实体。车队的实体的主键是车队号，所以，我们在多方(车辆)这个表中，增加1方(车队)的主键(车队号)作为一列来表示联系，即将  车队号  加到 车辆 这个实体的属性列表中。这里的 车队号 显然是 **外键**。

- **如果两个实体之间的联系是多对多的，联系要单独存放为一个表**。这个表的主键，是参与联系的两个实体的主键的组合，而联系的属性作为其他列。例如：车辆和司机之间是多对多的关系，使用 `联系名(车牌号，司机编码，使用日期，公里数)` 这里的车牌号是 车辆 这一实体的主键，司机编码是 司机 这一实体的主键，而后面两个是联系的属性。外键是： 车牌号，司机编码。

- 每个关系的主键都要标出来，外键写在关系的最后，属性括号的外面。




- [简明教学](https://blog.csdn.net/sunzhenhua0608/article/details/8822871)

- [详细教学](https://blog.csdn.net/zxq1138634642/article/details/9121363)

<br>

> 最后更新于2018.5.3
