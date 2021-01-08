---
title: 中高级SQL
date: 2021-01-08 15:21
tag:
- 数据库
---

# view
目的：视图，以在特定用户的视图中隐藏特定数据。任何不属于概念模型但作为“虚拟关系”对用户可见的关系称为视图，即仅仅是虚拟存在的。视图的表达式中可以引用其他的视图以及自身（递归）。

使用方法：
1. 创建
```
create view v as 
    select name
    from student;
```
2. 插入
```
insert into v values(reton);
```
插入只允许以下的简单视图：
+ 创建的时候，sql语句中from中只跟一个数据库
+ 创建的时候，select子句中不能包含表达式和聚集函数
+ 创建的时候，sql语句中没有group by和havaing子句
+ 没有被select子句列出的属性都没有not null约束
3. 删除
```
drop view v;
```
Materialized Views： 将虚拟存在的视图实际存储起来。但是不会随着虚拟视图更新而更新，需要手动更新。
**由于视图是虚拟存在的，视图定义保存表达式。在涉及到视图的查询的时候表达式被替换到使用视图的查询中。**
# transction
1. unit of work
2. atomic 
3. Isolation from concurrent transactions
4. begin implicitly，ended by commit work or rollback work

# 模式
1. 创建
    例. create table studnet 
2. 删除  

# Integrity Constraints
定义：确保数据库的操作不会导致数据一致性的丢失，防止对数据库的意外损害
1. not null，在创建数据库的时候使用
2. primary key( A1, A2, …, Am)
3. unique( A1, A2, …, Am),确保写在括号中的属性不会重复
4. check， 例子 check (semester in (’Fall’, ’Winter’, ’Spring’, ’Summer’))。*不支持子查询*
5. foreign key，例子dept_name varchar(20) references department或者foreign key (dept_name) references department。更新的时候需要先更新被参考的表。
6. default,默认值
7. index加速查询,有加index的属性,在查询的时候就不用把整个表的该属性遍历一遍
    1. 创建方法:
    + 针对单个属性的索引create index index_name on table(attr)
    + 组合查询: create index index_name on table(attr1, attr2)
    2. 删除方法:
    drop index index_name on table 
    > 添加约束
        例. alter table tableNmae add constraint primary key(id)  

    > 删除约束
        alter table tableNmae drop constraint constraintNmae


# 用户自定义类型
例子. create type Dollars as numeric (12,2) final 

# 用户自定义域
例子. create domain person_name char(20) not null
用户自定义域和用户自定义类型很像,但是自定义的域添加约束.

# 授权

1. 数据库的部分授权形式
    1. read - allows reading, but not modification of data
    2. insert - allows insertion of new data, but not modification of existing data.
    3. update - allows modification, but not deletion of data.
    4. delete - allows deletion of data  
2. 修改数据库模式的授权形式
    1. Index - allows creation and deletion of indices(index的复数).
    2. Resources - allows creation of new relations.
    3. Alteration - allows addition or deletion of attributes in a relation
    4. Drop - allows deletion of relations
3. 用户权限管理
    1. grant 授予  

        可以授予的权限有:
        + select
        + insert
        + update
        + delete
        + all privileges
        + references privilege //为某个属性设置外键的权利
        + with grant option //授予grant的权利,放在语句的最后
        例. grant user 'userName'@'hostName' indentified by 'passport'; //注册用户
        ```
        grant  //授权
            select, update
        on *.*
        to userName@'hostName';
        ```
        授权视图
        ```
        create view v as
        (sql);
        grant select on v to userName
        ```
    2. revoke 删除权限
    例子
    ```
    revoke
        update
    on *.* //哪些表
    from userName@'hostName';
    ```
    删除账户信息
    ```
    drop user 'userName'@'hostName'
    ```

# producer
producer允许业务逻辑作为存储过程记录在数据库中，一组为了完成特定功能的SQL 语句集
1. 创建
第一个参数是输入变量,第二个参数是输出变量
例. 
```
create procedure proName(in company varchar(20), out employee int)
begin
    select ..
    from ...
end;
```

2. 调用
```
call proName(param1, @param2);
```
3. 删除
```
drop procedure proName;
```

# function 
function允许业务逻辑作为存储过程记录在数据库中，一组为了完成特定功能的SQL 语句集 ;存储函数将向调用者返回一个且仅返回一个结果值;函数重载名称相同,参数个数不同
1. 创建
```
create function funName(company_name varchar(20))
returns varchar(20) //函数输出的是什么
begin
    declare res varchar(20);
    select city
    from employee
    where employee_name = ''
    into res;
    return res;
end;
```
2. 调用
```
select funName('xxxxx');
```

# 触发器
触发器是作为数据库修改的副作用由系统自动执行的语句
创建触发器
例
```
create trigger triggerName
after update on works for each row
begin
....
end;
```
引用更新前的值:referencing old row as   :  for deletes and updates
引用更新后的值:referencing new row as  : for inserts and updates
例.
```
create trigger setnull_trigger before update of takes
referencing new row as nrow
for each row
when (nrow.grade = ‘ ‘)
begin atomic
    set nrow.grade = null;
end;

```
