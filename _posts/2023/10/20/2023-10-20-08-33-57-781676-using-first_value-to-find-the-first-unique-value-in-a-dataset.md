---
layout: post
title: "Using FIRST_VALUE to find the first unique value in a dataset"
description: " "
date: 2023-10-20
tags: [function, FUNCTIONS]
comments: true
share: true
---

When working with datasets, it is often necessary to find the first unique value based on specific criteria. SQL provides various functions to accomplish this, one of which is FIRST_VALUE. In this blog post, we will explore how to use the FIRST_VALUE function to identify the first unique value in a dataset.

## Table of Contents
- [Introduction to FIRST_VALUE function](#introduction-to-first_value-function)
- [Example Scenario](#example-scenario)
- [Using FIRST_VALUE to find the first unique value](#using-first_value-to-find-the-first-unique-value)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction to FIRST_VALUE function

The FIRST_VALUE function is a window function in SQL that allows you to retrieve the first value in an ordered partition of a dataset. It is often used in conjunction with other analytical functions to perform complex analyses.

## Example Scenario

Let's consider a scenario where we have a table named `employees` with the following structure:

| employee_id | name   | department_id |
|-------------|--------|---------------|
| 1           | John   | 1             |
| 2           | Mary   | 1             |
| 3           | Alice  | 2             |
| 4           | Bob    | 3             |
| 5           | Mike   | 2             |
| 6           | Susan  | 3             |

Our aim is to find the first employee in each department based on their `employee_id`.

## Using FIRST_VALUE to find the first unique value

To solve this problem, we can use the FIRST_VALUE function along with the PARTITION BY clause to create partitions based on the `department_id` column. Then, we can order the employees within each partition by `employee_id` and retrieve the first value using the FIRST_VALUE function.

```sql
SELECT employee_id, name, department_id,
  FIRST_VALUE(employee_id) OVER (PARTITION BY department_id ORDER BY employee_id) AS first_employee_id
FROM employees;
```

This query will return the following result:

| employee_id | name   | department_id | first_employee_id |
|-------------|--------|---------------|------------------|
| 1           | John   | 1             | 1                |
| 2           | Mary   | 1             | 1                |
| 3           | Alice  | 2             | 3                |
| 4           | Bob    | 3             | 4                |
| 5           | Mike   | 2             | 3                |
| 6           | Susan  | 3             | 4                |

In the result, the `first_employee_id` column represents the first employee's `employee_id` within each department.

## Conclusion

Using the FIRST_VALUE function in SQL, we can easily find the first unique value in a dataset based on specific criteria. By combining it with the PARTITION BY clause, we can partition the dataset and retrieve the first value within each partition. This function provides a powerful tool for data analysis and decision-making.

## References

- [SQL Server FIRST_VALUE Function](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql?view=sql-server-ver15)
- [MySQL FIRST_VALUE Function](https://dev.mysql.com/doc/refman/8.0/en/window-function-descriptions.html#function_first-value)
- [PostgreSQL FIRST_VALUE Function](https://www.postgresql.org/docs/current/functions-window.html#FUNCTIONS-WINDOW-TABLE)
- [Oracle FIRST_VALUE Function](https://docs.oracle.com/en/database/oracle/oracle-database/21/sqlrf/FIRST_VALUE.html#GUID-55E3C674-F9C0-42D2-85B8-663CE03D7F52)