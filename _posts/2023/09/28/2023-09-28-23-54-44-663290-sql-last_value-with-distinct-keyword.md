---
layout: post
title: "SQL LAST_VALUE with DISTINCT keyword"
description: " "
date: 2023-09-28
tags: [LAST_VALUE, DISTINCT]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to return the last value in an ordered set of values. By default, it considers all duplicate values in the set and returns the last occurrence. However, there might be cases where you want to get the last distinct value from a set. In such situations, you can use the `DISTINCT` keyword along with `LAST_VALUE`. 

Here's an example to demonstrate how to use `LAST_VALUE` with the `DISTINCT` keyword:

```sql
SELECT DISTINCT LastName, 
       LAST_VALUE(FirstName) OVER (PARTITION BY LastName ORDER BY CreateDate) AS LastDistinctFirstName
FROM Employees;
```

In the above example, we have a table named `Employees` with columns `LastName`, `FirstName`, and `CreateDate`. We want to retrieve the last distinct `FirstName` for each `LastName`.

The `DISTINCT` keyword ensures that only distinct `LastName` values are considered. The `LAST_VALUE` function then returns the last `FirstName` within each distinct group of `LastName` values, based on the ordering specified in the `ORDER BY` clause (in this case, `CreateDate`).

By using `LAST_VALUE` with the `DISTINCT` keyword, you can obtain the desired results and get the last distinct value from a set of values in SQL.

#SQL #LAST_VALUE #DISTINCT