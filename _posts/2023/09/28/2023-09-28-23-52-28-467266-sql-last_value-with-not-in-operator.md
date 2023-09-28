---
layout: post
title: "SQL LAST_VALUE with NOT IN operator"
description: " "
date: 2023-09-28
tags: [WindowFunctions]
comments: true
share: true
---

In this blog post, we will explore how to use the `LAST_VALUE` function in SQL along with the `NOT IN` operator. This combination can be useful in scenarios where you need to filter out the last value of a specific column that is not present in another set of values.

## Introduction to `LAST_VALUE`

The `LAST_VALUE` function is a window function in SQL that allows you to access the last value in a specified column within a specific sequence of rows. It is commonly used in conjunction with a window frame clause, such as `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`, to define the window over which the function operates.

## Using `LAST_VALUE` with `NOT IN` Operator

To use the `LAST_VALUE` function with the `NOT IN` operator, we need to follow a two-step process:

1. Use the `LAST_VALUE` function to retrieve the last value of the column we are interested in.
2. Use the `NOT IN` operator to filter out any rows where the last value is present in a specified set of values.

Here's an example that demonstrates the usage:

```sql
SELECT column_name
FROM (
  SELECT column_name, LAST_VALUE(column_name) OVER (ORDER BY order_column) AS last_value
  FROM table_name
) AS subquery
WHERE last_value NOT IN ('value1', 'value2', 'value3');
```

In this example, we are retrieving the `column_name` from the `table_name` table. The `LAST_VALUE` function is used to retrieve the last value of `column_name` based on the ordering specified by the `order_column`. The result is then filtered using the `NOT IN` operator to exclude any rows where the last value is 'value1', 'value2', or 'value3'.

## Conclusion

The combination of the `LAST_VALUE` function and the `NOT IN` operator can be a powerful tool in SQL when you need to filter out the last value of a column that is not found in a specific set of values. This approach can help you efficiently achieve your desired results.

#SQL #WindowFunctions