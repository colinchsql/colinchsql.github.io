---
layout: post
title: "Specifying the ORDER BY clause in FIRST_VALUE"
description: " "
date: 2023-10-20
tags: [GUID, SYNTAX]
comments: true
share: true
---

When using the FIRST_VALUE function in a SQL query, you can specify the ORDER BY clause to determine the order in which the values are evaluated. This can be useful when you want to retrieve the first value based on a particular sorting condition.

The syntax for using the FIRST_VALUE function with the ORDER BY clause is as follows:

```sql
FIRST_VALUE(expression) OVER (
    [PARTITION BY partition_expression]
    ORDER BY sort_expression [ASC|DESC]
)
```

Let's break down the different components of this syntax:

- `expression`: The column or expression from which you want to retrieve the first value.
- `PARTITION BY`: Optional clause that divides the rows into partitions before evaluating the first value.
- `partition_expression`: The column or expression by which you want to partition the data.
- `ORDER BY`: Specifies the sorting condition for evaluating the first value.
- `sort_expression`: The column or expression you want to use for sorting.
- `ASC|DESC`: Optional sorting direction, ascending (ASC) or descending (DESC).

Here's an example to illustrate how to use the ORDER BY clause with FIRST_VALUE:

```sql
SELECT DISTINCT department_name, 
    FIRST_VALUE(first_name) OVER (
        PARTITION BY department_id 
        ORDER BY hire_date DESC
    ) AS first_hired_employee
FROM employees;
```

In this example, we select the distinct department names and use the FIRST_VALUE function to retrieve the first name of the employee who was most recently hired in each department. The ORDER BY clause is used to sort the employees by their hire date in descending order within each department.

By specifying the ORDER BY clause in the FIRST_VALUE function, you can control the sorting order and obtain the first value based on specific criteria. This can be particularly helpful when you want to find the earliest or latest value in a dataset based on a specific condition.

Remember, the FIRST_VALUE function with the ORDER BY clause is available in various SQL databases such as Oracle, SQL Server, PostgreSQL, and MySQL.

# References
- [Oracle FIRST_VALUE documentation](https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/FIRST_VALUE.html#GUID-B88B6855-5DFF-4FF3-A847-4D6E46B27211)
- [SQL Server FIRST_VALUE documentation](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql)
- [PostgreSQL FIRST_VALUE documentation](https://www.postgresql.org/docs/current/sql-expressions.html#SYNTAX-WINDOW-FUNCTIONS)
- [MySQL FIRST_VALUE documentation](https://dev.mysql.com/doc/refman/8.0/en/window-function-descriptions.html#function_first-value)