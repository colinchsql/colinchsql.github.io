---
layout: post
title: "SQL LAST_VALUE with LEAD function"
description: " "
date: 2023-09-28
tags: []
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to get the last value in a group or window. When combined with the `LEAD` function, it allows you to retrieve the next value in a sequence, making it a powerful tool for analyzing data in a specific order.

## Syntax of LAST_VALUE with LEAD

The syntax for using `LAST_VALUE` with `LEAD` is as follows:

```sql
LAST_VALUE(expression) OVER (PARTITION BY partition_expression ORDER BY order_expression ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
```

Here:

- `expression` is the column or expression to get the last value of
- `PARTITION BY` defines the grouping of the data
- `ORDER BY` specifies the order of the data within each group
- `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` ensures that the window includes all rows from the start of the partition up to and including the current row

## Example usage

Suppose we have a table called `employees` with the following data:

| id | name  | salary |
|----|-------|--------|
| 1  | John  | 5000   |
| 2  | Alice | 6000   |
| 3  | Bob   | 5500   |
| 4  | Emma  | 7000   |

We can use `LAST_VALUE` with `LEAD` to find the next highest salary for each employee in order:

```sql
SELECT name, salary, LAST_VALUE(salary) OVER (ORDER BY salary) AS next_highest_salary
FROM employees
```

The result would be:

| name  | salary | next_highest_salary |
|-------|--------|---------------------|
| John  | 5000   | 5500                |
| Bob   | 5500   | 6000                |
| Alice | 6000   | 7000                |
| Emma  | 7000   | 7000                |

In the above example, the `LAST_VALUE` function is applied on the `salary` column, and the `LEAD` function orders the result set by the `salary`. It retrieves the next highest salary for each employee.

## Conclusion

Using the `LAST_VALUE` function with the `LEAD` function allows you to access the last value in a group or window while also retrieving the next value in a sequence. This can be useful in various scenarios, such as identifying trends or comparing values.