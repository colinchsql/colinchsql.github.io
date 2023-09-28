---
layout: post
title: "SQL LAST_VALUE with FOR statement"
description: " "
date: 2023-09-29
tags: [LAST_VALUE]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function allows you to retrieve the last value within a group of rows in a specific order. By combining it with the `FOR` statement, you can define the order in which the values are evaluated.

Let's take a look at the syntax of the `LAST_VALUE` function with the `FOR` statement:

```sql
LAST_VALUE(column_name) OVER (ORDER BY column_name [ASC|DESC] ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
```

- `column_name`: The column from which you want to retrieve the last value.

The `ORDER BY` clause specifies the order in which the rows are evaluated. You can choose to sort the rows in ascending (`ASC`) or descending (`DESC`) order based on the `column_name`.

The `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` clause sets the range within which the `LAST_VALUE` function operates. In this case, it includes all the rows from the start of the partition to the current row.

Now, let's see an example to understand how the `LAST_VALUE` function with the `FOR` statement works.

Suppose we have the following `employees` table:

| emp_id | emp_name | salary |
| ------ | -------- | ------ |
| 1      | John     | 2000   |
| 2      | Alice    | 2500   |
| 3      | Bob      | 1700   |
| 4      | Emma     | 3000   |
| 5      | Jack     | 2200   |

If we want to retrieve the last salary for each employee, ordered by their ID in ascending order, we can use the following SQL query:

```sql
SELECT emp_id, emp_name, 
    LAST_VALUE(salary) OVER (ORDER BY emp_id ASC ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS last_salary
FROM employees;
```

This will produce the following result:

| emp_id | emp_name | last_salary |
| ------ | -------- | ----------- |
| 1      | John     | 2000        |
| 2      | Alice    | 2500        |
| 3      | Bob      | 1700        |
| 4      | Emma     | 3000        |
| 5      | Jack     | 2200        |

In this example, the `LAST_VALUE` function with the `FOR` statement retrieves the last salary for each employee, ordered by their ID in ascending order.

#SQL #LAST_VALUE #FOR