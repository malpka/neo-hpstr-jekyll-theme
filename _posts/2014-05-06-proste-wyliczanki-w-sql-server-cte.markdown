---
layout: post
title: "Proste wyliczanki w SQL Server - CTE"
date: 2014-05-06 10:02:46 +0200
comments: true
categories: sql
---

Tylko pamiętajcie o średniku przed `with`! ;)

Odliczanie od 1 do 10.

``` sql
;with cte as 
(
  select 1 as x
  union all
  select x+1 from cte where x < 10
)
select * from cte
```

Wynik

```
x
-----------
1
2
3
4
5
6
7
8
9
10
```

Równie dobrze możemy przechodzić po datach:

<!-- more -->

``` sql
declare @start_date datetime = '2014-05-06 00:00:00'
declare @dest_date datetime = '2014-05-12 00:00:00'
;with date_cte as
(
  select @start_date as mydate
  union all 
  select DATEADD(dd, 1, mydate)
  from date_cte c
  where DATEADD(dd, 1, mydate) <= @dest_date
)
select mydate from date_cte
```

Wynik:

```
mydate
-----------------------
2014-05-06 00:00:00.000
2014-05-07 00:00:00.000
2014-05-08 00:00:00.000
2014-05-09 00:00:00.000
2014-05-10 00:00:00.000
2014-05-11 00:00:00.000
2014-05-12 00:00:00.000
```

## Standardowe przechodzenie po drzewie

### Drzewo

``` sql
declare @t table
(
  id int not null,
  parent_id int null
)

insert into @t values (0, null),(1, 0),(2, 1),(3, 1),(4, 3),(5, 0),(6, 0),(7, 6)
-- 0
-- +-1
-- | +-2
-- | +-3
-- |   +-4
-- +-5
-- +-6
--   +7
```

``` sql
select * from @t
```

```
id          parent_id
----------- -----------
0           NULL
1           0
2           1
3           1
4           3
5           0
6           0
7           6
```

### Od liścia do korzenia

``` sql
;with cte as 
(
  select id, parent_id from @t where id = 4
  union all
  select t.id, t.parent_id
  from cte c
  join @t t on c.parent_id = t.id
)
select * from cte
```

wynik

``` 
id          parent_id
----------- -----------
4           3
3           1
1           0
0           NULL

(4 row(s) affected)

```


### Od gałęzi do liści

``` sql
;with cte as 
(
  select id, parent_id from @t where parent_id = 1
  union all
  select t.id, t.parent_id
  from cte c
  join @t t on t.parent_id = c.id
)
select * from cte
```

wynik

```
id          parent_id
----------- -----------
2           1
3           1
4           3

(3 row(s) affected)
```