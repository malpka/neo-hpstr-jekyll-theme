---
layout: post
title: "SQL - Calculate sum of preceding values"
date: 2015-02-27 10:02:46 +0200
comments: true
categories: sql
---

From SQL Server 2012 it's simple as

``` sql
SELECT val, sum = SUM(val) OVER (ORDER BY val ROWS UNBOUNDED PRECEDING) FROM #tab;
```

Result

```
val     sum
-----------
1		1
2		3
3		6
4		10
5		15
6		21
7		28
8		36
9		45
10		55
```
