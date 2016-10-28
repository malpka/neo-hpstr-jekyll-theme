---
layout: post
title: "Howto hide SQL Server databases for specific login in Management Studio"
date: 2014-05-05 12:09:55 +0200
comments: true
categories: sql
facebook:
    image: http://blog.codemonkey.pl/images/mydb.png
---
{% img left /images/mydb.png 373 265 mydb %}

Default Microsoft SQL Server configuration allows all useres marked as `public` to see all the databases on the server. 

After creating a database we can grant a `db_owner` role for a server login without allowing it to view another db's.

Assuming that login `myuser` is created in a server security part.

``` sql
USE mydb
ALTER AUTHORIZATION ON DATABASE::mydb to myuser

USE MASTER
DENY VIEW ANY DATABASE TO myuser
```

From now on user can see only the newly created `mydb` database (and of course `master` and `tempdb`)

[Source](http://social.msdn.microsoft.com/Forums/sqlserver/en-US/a989ca87-660d-41c4-9dac-70b29a83ddfb/hide-database-names-from-unauthroized-users-in-ssms?forum=sqlsecurity),
[moar source](http://www.mssqltips.com/sqlservertip/2995/how-to-hide-sql-server-user-databases-in-sql-server-management-studio/)
