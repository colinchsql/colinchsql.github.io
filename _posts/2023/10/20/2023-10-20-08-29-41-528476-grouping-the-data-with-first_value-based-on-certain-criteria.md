---
layout: post
title: "Grouping the data with FIRST_VALUE based on certain criteria"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

In some scenarios, we might need to group the data based on certain criteria and retrieve the first value for each group. The SQL function `FIRST_VALUE` can help us achieve this.

Here is an example of how to use the `FIRST_VALUE` function to group the data and retrieve the first value based on a specific criteria.

## Table structure

Consider a table called `employees` with the following structure:

| employee_id | employee_name | department | salary |
|-------------|---------------|------------|--------|
| 1           | John Doe      | Sales      | 50000  |
| 2           | Jane Smith    | HR         | 60000  |
| 3           | Mark Johnson  | Sales      | 55000  |
| 4           | Lisa Anderson | Finance    | 70000  |
| 5           | Mike Davis    | HR         | 65000  |
| 6           | Sarah Lee     | Finance    | 75000  |

## Query example

Suppose we want to group the employees by department and retrieve the employee with the highest salary for each department. We can achieve this using the `FIRST_VALUE` function and the `PARTITION BY` clause.

```sql
SELECT 
    department,
    FIRST_VALUE(employee_name) OVER (PARTITION BY department ORDER BY salary DESC) AS highest_paid_employee
FROM
    employees;
```

In this query, we partition the data by the `department` column and order it by the `salary` column in descending order. The `FIRST_VALUE` function then retrieves the first value (highest paid employee) for each partition.

## Result

The above query will give us the following result:

| department | highest_paid_employee |
|------------|----------------------|
| Sales      | Mark Johnson         |
| HR         | Jane Smith           |
| Finance    | Sarah Lee            |

Each row represents a department along with the employee who has the highest salary in that department.

By using the `FIRST_VALUE` function and properly partitioning the data, we can easily group the data and retrieve the first value based on certain criteria.

References:
- [SQL FIRST_VALUE Function](https://www.w3schools.com/sql/sql_first_value.asp)
- [SQL Server FIRST_VALUE Function](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql?view=sql-server-ver15)