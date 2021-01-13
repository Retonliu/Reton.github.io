---
title: 数据库----join
date: 2021-01-08 13:33
tags:
- 数据库
---
join的时候如果加上natural关键字，则会把相同的属性（连接起来的粘合剂）只留下一项
+ outer join: 
    1. left join(left outer join): 保留左边表的全部，如果左边表的元组不存在匹配的右边表的元组，则对应属性为空
    2. right join(right outer join): 与left outer join 相反
    3. full outer join: 不管左右两边是否匹配，都要保留下来。不匹配的属性置为null
+ inner join: 只取两个表的交集，即左右两边不存在匹配的则去掉

left join 用法: A left join B on A.x = B.x
full outer join 用法: A full outer join B using(x)