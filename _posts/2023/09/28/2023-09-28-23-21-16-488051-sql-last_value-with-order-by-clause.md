---
layout: post
title: "SQL LAST_VALUE with ORDER BY clause"
description: " "
date: 2023-09-28
tags: [LastValue, OrderBy]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to retrieve the last value in a set of values, based on a specified order. The `ORDER BY` clause is used to determine the order in which the rows are evaluated.

## Syntax

The basic syntax of the `LAST_VALUE` function with `ORDER BY` clause is as follows:

```
LAST_VALUE(column_expression) OVER (ORDER BY sort_expression [ASC|DESC])
```

- `column_expression`: The column or expression for which the last value is to be retrieved.
- `sort_expression`: The column or expression used to determine the order of the rows.
- `ASC` or `DESC`: Optional. Specifies the sort order. Defaults to ascending (ASC).

## Example

Let's consider a simple table called `orders` with the following data:

```
+----+------------+-------+
| ID |  OrderDate | Total |
+----+------------+-------+
|  1 | 2021-01-01 |   100 |
|  2 | 2021-02-01 |    85 |
|  3 | 2021-03-01 |   150 |
+----+------------+-------+
```

Suppose we want to retrieve the last total value from the `orders` table, ordered by the order date in descending order. We can use the `LAST_VALUE` function along with the `ORDER BY` clause as follows:

```sql
SELECT 
    LAST_VALUE(Total) OVER (ORDER BY OrderDate DESC) AS LastTotal
FROM 
    orders;
```

The result of the above query will be:

```
+----------+
| LastTotal |
+----------+
|       150 |
|       150 |
|       150 |
+----------+
```

As you can see, the `LAST_VALUE` function returns the last total value (150) for each row, as specified by the `ORDER BY` clause.

## Conclusion

The `LAST_VALUE` function with the `ORDER BY` clause in SQL allows you to retrieve the last value from a set of values, based on a specified order. This can be useful in scenarios where you need to fetch the latest or most recent value from a table.

#SQL #LastValue #OrderBy