# MySQL

## introduction & install

## base query

### select

    show databases;
    use [databases];
    select database();
    show tables;
    show full columns from [table];
    -- data_format "yyyy-mm-dd"
    select * from [table] where [row]={} order by [];

    select [arithmetic expressions] as [];
    select distinct [];

###  where

    MySQL 8.0 默认使用 utf8mb4字符集，其默认排序规则是 utf8mb4_0900_ai_ci（不区分大小写）

  AND OR NOT operators
  result: 0,1,NULL

### IN

    select * from [table] where [] in ();

### between

    select * from [table] where between {} and {};

### like

    select * from [table] where [] like "%a_";

### regexp

^ $ | [] [-]

    select * from [table] where [] regexp "";

### is null | is not null

    select * from where [] is null;

### order_by

default order by primary key

ase desc

ase null > !null

    select *,[] as [foo] from [] order by [row] ase, [row], [foo], [foo]*[bar] desc;
    --col order grammar , avoid using
    select [row],[row] from [table] order by 2,1;

    case [row]
        when then
        ...
    end

    field([row], val...)



### limit

    select * from [] limit {limit};
    select * from [] limit {offset},{limit};

### 执行顺序

1. FROM 和 JOIN
   ↓
2. WHERE
   ↓
3. GROUP BY
   ↓
4. HAVING
   ↓
5. SELECT
   ↓
6. DISTINCT
   ↓
7. ORDER BY
   ↓
8. LIMIT/OFFSET

## join

### join [inner join]

    select t1.[row] 
    from [table1] t1
    join [table2] t2
        on t1.[row]=t2.[row]

### joining across databases

    select * from [table1] join [database].[table2] t2 on [table1].[row] = t2.[row]

### self join

    select t1.[row1], t2.[row1] as r2
    from [table] t1
    join [table] t2
        on t1.[row1] = t2.[row2]

### join multiple tables

    select * 
    from [table1] t1
    join [table2] t2
        on t1.[row]=t2.[row]
    join [table3] t3
        on t2.[row]=t3.[row]

### compound join conditions

    select *
    from [table1] t1
    join [table2] t2
        on t1.[row]=t2.[row] and t1.[row2]=t2.[row2]

### implicit join syntax [be not rrcommended for use]

    select *
    from [table1] t1, [table2] t2
    where t1.[row]=t2.[row]

    等价于 

    select *
    from [table1] t1
    join [table2] t2
        on t1.[row]=t2.[row]

### outer joins [between multiple tables]

    left join [left outer join]

    right join [right outer join]

尽量只使用左连接，避免sql理解复杂度上升

### self outer joins

内连接语法换成外连接

### the using clause

    select t1.[row] 
    from [table1] t1
    join [table2] t2
        -- on t1.[row]=t2.[row] and t1.[row2]=t2.[row2]
        using ([row],[row2])
        -- 不同表列名完全一致时使用

### natural join  自然连接

    select * 
    from [table1] 
    narutal join [table2];

基于共同列由引擎决定连接，不建议使用

### cross joins  交叉连接

    select * 
    from [table1] t1 
    cross join [table2] t2;

    -- 隐式语法
    select *
    from [table1] t1,[table2] t2;

全连接

### Unions

        select * from [table1]
        union
        select * from [table2]

基于行合并select结果，被union的两个表的列数量要一样， 列名基于第一段查询

## CURD

### column attributes

### insert

    insert into [table]
    values (DEFAULT, 'str', '1999-01-01', NULL)

    insert into [table] ([col])
    values (dafault)

    insert into [table] ([col])
    values (dafault), ('')

### insert hierachical rows

先执行表1插入，以下函数可以获取最近执行sql的插入id，作为表2插入时的参数

    LAST_INSERT_ID()

### creating a copy of a table

建表时使用子查询， 不会复制表属性

    create table [table1] as
    select * from [table2] 

### update

    update [table] 
    set [row1]={},[row2]={}
    where [row3]={3}

mysql 客户端的安全更新模式，一次只能更新一条记录

    子查询

    update [table1]
    set [row1]={}
    where [row2] in   -- 只有一个结果用=，多个结果用in 
                    (select [row3] from [table2] where [row4]={})

### delete

    delete from [table]
    where [row]={} --不加限制全删

## 