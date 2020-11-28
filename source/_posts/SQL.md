---
title: MySQL语句
date: 2020-11-28 09:49
tags: 
- MySQL
- 数据库
---
# SQL
## DDL
*指定表的信息*
### 1. 建表  
例. create table instructor (
            ID         char(5),
            name       varchar(20) not null,
            dept_name  varchar(20),
            salary     numeric(8,2),
            primary key (ID),
            foreign key (dept_name) references department))
其中在创建表的时候可以加上以下3中约束：
    1. not null
    2. primary key 自动给指定键加上非空约束
    3. foreign key

### 2. 删表  
例. 删除整个表以及表中的内容  
drop table student  

### 3. 清空表
例. delete from student

### 4. 修改表的定义 
    1. 添加表的属性，例. alter table student add name varchar(20)  
    其中A是要添加的属性名，D是A的域。 新添加的属性值中的所有元组均为空
    2. 删除表的属性(没有得到所有的数据库系统的支持)，例. alter table student drop name

## DML
*提供增删改查功能*

### 1. 查询  
例. select distinct dept_name
	from instructor, teachers
    where dept_name = ‘Comp. Sci.'  and salary > 80000

#### select
+ 因为SQL允许元组值重复，所以可以使用distinct去重  
+ 可以使用关键字all指定不删去重复项  
+ 对于select后面的每个属性值，可以使用加减乘除运算，比如要取出每一个count的一半，可以写为count/2
+ 使用as可以重命名。
#### from
+ from中的,表示两个表的笛卡尔积
+ natural join 实现自然连接，自然连接会把两个表中具有相同属性且属性值相同元组连接为一项。自然连接在连接多个表的时候可能会把具有相同值但是不相关属性给连接起来的风险。
#### where
+ where中的条件可以使用and, or和not来连接
+ 可以通过类似如下语句：where section.course_id = course.course_id,来实现section表和course表关于course_id的连接
+ like关键字加上 %或者_,%匹配任意字符串，_匹配任意字符
+ order by 排序， 例. order by name desc(降序), order by name(默认升序，asc)
+ between and 选择区间
+ 解构 例. where (instructor.ID, dept_name) = (teaches.ID, ’Biology’);
+ null, 例. where name is null。任何关于null的比较都返回unknown。
+ 在where中，如果某个值是unknown会被当作false。 is unknown判断是不是known

#### 集合操作
1. (select course_id from section where sem = ‘Fall’ and year = 2009) union(select course_id from section where sem = ‘Spring’ and year = 2010)
2. (select course_id from section where sem = ‘Fall’ and year = 2009) intersect(select course_id from section where sem = ‘Spring’ and year = 2010)
3. (select course_id from section where sem = ‘Fall’ and year = 2009) except(select course_id from section where sem = ‘Spring’ and year = 2010)

以上三个操作都会自动去掉两者中重复的元组值，可以使用union all, intersect all 和 except all 来保留重复值

### 2.插入
注意不要插入和insert后面select的表是同个表，不然可能会造成歧义，出现bug
例. insert into teachers values(reton, 175)
例. insert into student
	select ID, name, dept_name, 0
    from   instructor

### 3. 修改
例. update instructor
        set salary = salary * 1.03
        where salary > 100000;
例. update instructor
            set salary = case
            when salary <= 100000 then salary * 1.05
            else salary * 1.03
            end

## 聚集函数
1. avg
例子. 
select avg (salary)
from instructor
where dept_name= ’Comp. Sci.’;
2. min
例子. 
select count (distinct ID)
from teaches
where semester = ’Spring’ and year = 2010
3. max
4. sum
5. count

### 3.删除
delete from instructor where dept_name= ’Finance’;

## 分组查询

### 1. group by
+ 分组查询中，select的属性必须是分组的属性
### 2. having
只能跟group by一起出现。
**where作用于分组之前，having作用于分组之后**

## 子查询
select distinct course_id
from section
where semester = ’Fall’ and year= 2009 and 
            course_id in (select course_id
            from section
            where semester = ’Spring’ and year= 2010);

### 1. some (at least one)
例. select name
from instructor
where salary > some (select salary
        from instructor
        where dept_name = ’Biology’);

### 2. all

### 3. exists
如果后面跟着的子查询不为空则返回true
select course_id
   from section as S
      where semester = ’Fall’ and year= 2009 and 
                    exists (select *
                from section as T
                where semester = ’Spring’ and year= 2010 
                and S.course_id= T.course_id);

### 4. not exists
### 5. unique
判断子查询得到的结果是不是无重复的
例. select T.course_id
from course as T
where unique (select R.course_id
                from section as R
                where T.course_id= R.course_id 
                and R.year = 2009);
### lateral(大部分数据库系统不支持)

select name, salary, avg_salary
from instructor I1, 
                lateral (select avg(salary) as avg_salary
                from instructor I2
                where I2.dept_name= I1.dept_name);

### with
生成一个临时的表
例.      
with max_budget (value) as
         (select max(budget)
                    from department)
                    select budget
                    from department, max_budget
                    where department.budget = max_budget.value;
**子查询也可以用在from语句后面**,例.
select dept_name, avg_salary
from (select dept_name, avg (salary) as avg_salary
           from instructor
           group by dept_name)
           as dept_avg (dept_name,  avg_salary)
           where avg_salary > 42000;










    




