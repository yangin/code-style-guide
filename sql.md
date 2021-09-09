# SQL 编码规范

## 目录

  1. [命名](#命名)
  1. [语句](#语句)

## 命名

[1.1]()【强制】表的命名必须以`t_`为前缀,格式为t_`<table>`。
> `<table>` 为表名

```sql
-- bad
user_info

-- good
t_user_info
```

[1.2]()【强制】视图的命名必须以`v_`为前缀，格式为v_`<table>`。
> `<table>` 为表名

```sql
-- bad
user_info
t_user_info

-- good
v_user_info
```

[1.3]()【强制】存储过程的命名必须以`proc_`为前缀，格式为proc_`<procedure name>`。
> `<procedure name>` 为存储过程名

```sql
-- bad
get_work_info

-- good
proc_get_work_info
```

[1.4]()【强制】方法的命名必须以func_为前缀，格式为func_`<function name>`，且方法名的开头必须为动词或动词短语。
> `<function name>` 为方法名

```sql
-- bad
current_date
get_current_date

-- good
func_get_current_date
```

[1.5]()【强制】索引的命名必须以idx_为前缀，格式为：idx_`<table>`_`<column>`
> `<table>`为表名，`<column>`为添加索引的列名。

```sql
-- bad
name
user_info_name

-- good
idx_user_info_name
```

[1.6]()【强制】列名必须为非还保留字段的有意义的英文或英文简写，且全部为小写，单词之间使用_连接。

```sql
-- bad
date 
yhxm
USER_NAME
userName

-- good
id
user_name
```

[1.7]()【强制】列名与表名长度不得超过32个字符，若超过则采用缩写
> 为什么?

```sql
-- bad
personal_user_

-- good
address
```

[1.8]()【强制】列名与表名等相关命名均不得以`_`或`其他符号`开头或结尾。

```sql
-- bad
_name
_t_work
v_user$

-- good
user_name
t_work
v_user
```

[1.9]()【强制】当存在子母表关系时，子表中需存在与母表id关联的id，且id的命名为：母表名（或表名简写）+id。

```sql
-- 子表为child_table,母表为mother_table,则子表中表示与母表id对应关系的id叫做 mother_table_id。

-- bad
tid
mother_id

-- good
mother_table_id
```

## 语句

[2.1]()【强制】所有SQL的关键字都必须采用大写，字段，表名，视图名等为小写。

```sql
-- bad
select * from base_organize where id=1

-- good
SELECT * FROM base_organize WHERE id=1
```

[2.2]()【强制】当SQL语句过长时，按SELECT,FROM,WHERE,GROUP BY,ORDER BY等关键字进行折行，方便阅读。

```sql
-- bad
SELECT b.work_date,b.type FROM t_user_info a,t_work_info b WHERE a.id=b.user_id 
AND a.user_name='15055156363' AND a.state=1

-- good
SELECT b.work_date,b.type 
FROM t_user_info a,t_work_info b 
WHERE a.id=b.user_id 
AND a.user_name='15055156363' AND a.state=1
```

[2.3]()【强制】当多表关联查询时，出现的字段必须标明来源，避免在阅读复杂的SQL语句时混淆。

```sql
-- bad
SELECT work_date,type FROM t_user_info a,t_work_info b 
WHERE id=user_id 
AND user_name='15055156363' AND state=1

-- good
SELECT b.work_date,b.type 
FROM t_user_info a,t_work_info b 
WHERE a.id=b.user_id 
AND a.user_name='15055156363' AND a.state=1
```

[2.4]()【强制】当多表关联查询时，在WHERE部分，优先写出表的关联关系，然后写其他查询条件。

```sql
-- bad
SELECT b.work_date,b.type 
FROM t_user_info a,t_work_info b 
WHERE a.user_name='15055156363' AND a.state=1 AND a.id=b.user_id 

-- good
SELECT b.work_date,b.type 
FROM t_user_info a,t_work_info b 
WHERE a.id=b.user_id 
AND a.user_name='15055156363' AND a.state=1
```
