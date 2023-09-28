---
layout: post
title: "SQL LAST_VALUE with TRUNCATE statement"
description: " "
date: 2023-09-29
tags: [LAST_VALUE, TRUNCATE]
comments: true
share: true
---

In SQL, the **LAST_VALUE** function is used to return the last value within a specific window frame. It can be handy in scenarios where you need to retrieve the last value of a column based on a specific ordering. 

In this blog post, we will explore how to use the **LAST_VALUE** function in conjunction with the **TRUNCATE** statement to achieve our desired result.

## The TRUNCATE Statement

The **TRUNCATE** statement is a DDL (Data Definition Language) statement used to remove all the records from a table or a specified partition of a table. Unlike the **DELETE** statement, **TRUNCATE** does not log individual row deletions, making it faster and less resource-intensive. However, **TRUNCATE** is non-recoverable, meaning that once executed, there is no going back.

## Syntax of LAST_VALUE Function

The **LAST_VALUE** function can be used in a `SELECT` statement to retrieve the last value of a column based on a specific ordering. The syntax for the **LAST_VALUE** function is as follows:

```sql
LAST_VALUE ( expression ) OVER (
    [ PARTITION BY partition_expression ]
    ORDER BY sort_expression
    [ ROWS BETWEEN { UNBOUNDED PRECEDING | n PRECEDING } AND CURRENT ROW ]
)
```

- **expression**: The column or expression for which we want to retrieve the last value.
- **PARTITION BY**: Optional clause used to divide the result set into partitions.
- **ORDER BY**: The column or expression by which the result set is ordered, determining which value is considered the last.
- **ROWS BETWEEN**: Optional clause used to specify the window frame within which to evaluate the **LAST_VALUE**.

## Usage of LAST_VALUE with TRUNCATE Statement

Now, let's see an example of how we can use the **LAST_VALUE** function with the **TRUNCATE** statement.

Consider the following sample table named `employees`:

| Employee_ID | Name   | Salary  |
|-------------|--------|---------|
| 1           | John   | 5000    |
| 2           | Alice  | 6000    |
| 3           | Bob    | 4500    |
| 4           | Sarah  | 7000    |
| 5           | Michael| 5500    |

To remove all the records from the table except the row with the highest salary, we can use the following SQL query:

```sql
TRUNCATE TABLE employees 
EXCEPT 
SELECT * FROM (
  SELECT *, LAST_VALUE(salary) OVER (ORDER BY salary) AS last_salary
  FROM employees
) AS subquery 
WHERE salary < last_salary;
```

In this query, we first use the **LAST_VALUE** function to find the last (highest) salary from the `employees` table. Then, we use a **subquery** to compare each row's salary with the last_salary. Finally, we use the **TRUNCATE** statement to delete the rows that don't meet the condition.

**#SQL #LAST_VALUE #TRUNCATE**

By combining the power of the **LAST_VALUE** function and the **TRUNCATE** statement, you can efficiently delete specific rows from a table while retaining the one with the highest value based on a particular column.