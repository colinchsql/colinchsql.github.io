---
layout: post
title: "SQLite Aggregate Functions"
description: " "
date: 2023-10-13
tags: [SQLite, AggregateFunctions]
comments: true
share: true
---

In a relational database management system (RDBMS), aggregate functions perform calculations on a set of values and return a single value. In SQLite, there are several aggregate functions that you can use to manipulate and analyze your data.

## 1. COUNT

The `COUNT` function is used to count the number of rows returned by a query. It can be used with the `*` wildcard to count all rows, or with a specific column name to count the number of non-null values in that column.

```sql
SELECT COUNT(*) FROM my_table;

SELECT COUNT(column_name) FROM my_table;
```

## 2. SUM

The `SUM` function is used to calculate the sum of all values in a column.

```sql
SELECT SUM(column_name) FROM my_table;
```

## 3. AVG

The `AVG` function is used to calculate the average of all values in a column.

```sql
SELECT AVG(column_name) FROM my_table;
```

## 4. MAX

The `MAX` function is used to find the maximum value in a column.

```sql
SELECT MAX(column_name) FROM my_table;
```

## 5. MIN

The `MIN` function is used to find the minimum value in a column.

```sql
SELECT MIN(column_name) FROM my_table;
```

## 6. GROUP BY

The `GROUP BY` clause is used in conjunction with aggregate functions to group rows based on one or more columns. This allows you to perform calculations and aggregations on a subset of data.

```sql
SELECT column1, SUM(column2)
FROM my_table
GROUP BY column1;
```

## 7. HAVING

The `HAVING` clause is used to filter the groups created by the `GROUP BY` clause. It works similarly to the `WHERE` clause but operates on groups instead of individual rows.

```sql
SELECT column1, SUM(column2)
FROM my_table
GROUP BY column1
HAVING SUM(column2) > 100;
```

Aggregate functions are powerful tools in SQL for performing calculations and deriving meaningful insights from your data. Understanding how to use them effectively can greatly enhance your data analysis capabilities.

For more information on aggregate functions in SQLite, you can refer to the [official SQLite documentation](https://www.sqlite.org/lang_aggfunc.html).

\#SQLite \#AggregateFunctions