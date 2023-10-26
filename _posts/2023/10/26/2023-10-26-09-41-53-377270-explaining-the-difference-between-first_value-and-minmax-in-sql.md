---
layout: post
title: "Explaining the difference between FIRST_VALUE and MIN/MAX in SQL"
description: " "
date: 2023-10-26
tags: [SQLRF00668, SQLRF00625]
comments: true
share: true
---

When working with SQL queries, you may come across scenarios where you need to retrieve the first value or the minimum/maximum value from a set of rows based on certain criteria. In such cases, you may have the option to use either the FIRST_VALUE function or the MIN/MAX functions. Although they may seem similar, there are some key differences between them that are important to understand. 

## FIRST_VALUE Function

The FIRST_VALUE function is an analytical function in SQL that allows you to retrieve the first value from a set of rows based on the specified ordering. You can define the ordering using the ORDER BY clause within the OVER clause. 

Here's an example to illustrate the usage of the FIRST_VALUE function:

```sql
SELECT
    employee_id,
    department,
    salary,
    FIRST_VALUE(salary) OVER (PARTITION BY department ORDER BY salary) AS first_dept_salary
FROM
    employees;
```
In the above query, the FIRST_VALUE function is used to retrieve the first salary for each department by ordering the rows based on the salary in ascending order. The PARTITION BY clause is used to group rows by department.

## MIN/MAX Functions

On the other hand, the MIN and MAX functions are aggregate functions in SQL that allow you to retrieve the minimum and maximum values from a set of rows. These functions are commonly used in conjunction with the GROUP BY clause to calculate aggregate values for each group.

Here's an example to demonstrate the usage of the MIN and MAX functions:

```sql
SELECT
    department,
    MIN(salary) AS min_salary,
    MAX(salary) AS max_salary
FROM
    employees
GROUP BY
    department;
```

In the above query, both the MIN and MAX functions are used to retrieve the minimum and maximum salaries for each department group.

## Key Differences

Now that we understand the basic usage of both functions, let's highlight the key differences between FIRST_VALUE and MIN/MAX:

- **Function Type**: FIRST_VALUE is an analytical function, while MIN/MAX are aggregate functions.
- **Usage**: FIRST_VALUE is used to retrieve the first value based on the defined ordering within each group of rows. MIN/MAX are used to retrieve the overall minimum and maximum values for each group.
- **Ordering**: FIRST_VALUE allows you to define the ordering of rows using the ORDER BY clause within the OVER clause. MIN/MAX do not provide the option to specify custom ordering.
- **Return Type**: FIRST_VALUE returns the same data type as the column being evaluated, while MIN/MAX always return a numeric data type.

In summary, when you need to retrieve the first value within each group of rows based on specific ordering, you should use the FIRST_VALUE function. On the other hand, if you need to calculate the minimum or maximum values for each group without custom ordering, the MIN and MAX functions are the appropriate choices.

# References
- [Oracle Documentation: FIRST_VALUE Function](https://docs.oracle.com/database/121/SQLRF/functions004.htm#SQLRF00668)
- [Oracle Documentation: MIN Function](https://docs.oracle.com/database/121/SQLRF/functions063.htm#SQLRF00625)
- [Oracle Documentation: MAX Function](https://docs.oracle.com/database/121/SQLRF/functions055.htm#SQLRF00638)
- [SQL Server Documentation: FIRST_VALUE (Transact-SQL)](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql?view=sql-server-ver15)
- [SQL Server Documentation: MIN (Transact-SQL)](https://docs.microsoft.com/en-us/sql/t-sql/functions/min-transact-sql?view=sql-server-ver15)
- [SQL Server Documentation: MAX (Transact-SQL)](https://docs.microsoft.com/en-us/sql/t-sql/functions/max-transact-sql?view=sql-server-ver15)
- [MySQL Documentation: FIRST_VALUE Function](https://dev.mysql.com/doc/refman/8.0/en/window-function-descriptions.html#function_first-value)
- [MySQL Documentation: MIN Function](https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html#function_min)
- [MySQL Documentation: MAX Function](https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html#function_max)

#hashtags #SQL