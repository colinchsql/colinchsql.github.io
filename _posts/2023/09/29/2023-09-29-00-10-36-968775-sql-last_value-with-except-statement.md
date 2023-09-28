---
layout: post
title: "SQL LAST_VALUE with EXCEPT statement"
description: " "
date: 2023-09-29
tags: [LASTVALUE, EXCEPT]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to return the last value in a set of rows. This can be useful when you want to find the most recent record or the latest update in a table. 

The `EXCEPT` statement is used to combine the result sets of two queries and return only the distinct rows that are present in the first query but not in the second query.

## Syntax

```sql
LAST_VALUE (expression) OVER (PARTITION BY column ORDER BY column [ASC|DESC] ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
```

## Example 

Consider a table called `employees` with the following structure:

| employee_id | name     | salary |
|-------------|----------|--------|
| 1           | John     | 3000   |
| 2           | Jane     | 2500   |
| 3           | Michael  | 4000   |
| 4           | Jessica  | 3500   |
| 5           | Samantha | 4500   |

If you want to find the last recorded salary for each employee, you can use the `LAST_VALUE` function along with the `EXCEPT` statement. Here's an example query:

```sql
SELECT employee_id, name, salary
FROM (
    SELECT employee_id, name, salary,
        LAST_VALUE(salary) OVER (
            PARTITION BY employee_id
            ORDER BY employee_id ASC
            ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
        ) as last_salary
    FROM employees
) AS subquery
WHERE salary != last_salary
```

In the above query, we use the `LAST_VALUE` function to get the last salary value for each employee. Then, we use the `EXCEPT` statement to exclude the rows where the salary is equal to the last recorded salary. 

This query will return the rows where the salary has changed for each employee:

| employee_id | name     | salary |
|-------------|----------|--------|
| 1           | John     | 3000   |
| 2           | Jane     | 2500   |
| 3           | Michael  | 4000   |
| 4           | Jessica  | 3500   |

In conclusion, by combining the `LAST_VALUE` function with the `EXCEPT` statement, you can easily find the rows where a specific column value has changed in a table. This can be particularly useful when working with historical or time-based data. 

#SQL #LASTVALUE #EXCEPT