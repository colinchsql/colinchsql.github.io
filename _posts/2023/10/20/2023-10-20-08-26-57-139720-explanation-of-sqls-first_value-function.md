---
layout: post
title: "Explanation of SQL's FIRST_VALUE function"
description: " "
date: 2023-10-20
tags: [GUID]
comments: true
share: true
---

SQL's FIRST_VALUE function is a powerful tool that allows you to retrieve the first value in a specified order within a group of rows. This function is particularly useful when you want to get the first value in a set of data, based on a specific ordering criteria.

## Syntax

The syntax for using the FIRST_VALUE function in SQL is as follows:

```sql
FIRST_VALUE(expression) OVER (
  [PARTITION BY partition_expression]
  ORDER BY sort_expression [ASC | DESC]
  [ROWS {N | UNBOUNDED PRECEDING} ...]
)
```

Let's break down the different components of this syntax:

- `expression`: This represents the column or expression from which you want to retrieve the first value.
- `PARTITION BY`: This clause is optional and allows you to divide the result set into partitions or groups based on the specified expression. The FIRST_VALUE function is then applied separately to each partition.
- `ORDER BY`: This clause is mandatory and specifies the order in which the rows should be evaluated. You can specify one or more columns or expressions to define the sorting criteria.
- `ROWS {N | UNBOUNDED PRECEDING} ...`: This clause is optional and determines the window frame of the FIRST_VALUE function. It allows you to specify a range of rows within which the function is applied.

## Example Usage

Let's consider a simple example to understand how the FIRST_VALUE function works. Imagine we have a table called `employees` with the following data:

| employee_id | employee_name | salary |
|-------------|---------------|--------|
| 1           | Alice         | 5000   |
| 2           | Bob           | 6000   |
| 3           | Charlie       | 4500   |
| 4           | David         | 5500   |
| 5           | Emily         | 4000   |

To retrieve the first employee's name and salary based on the highest salary, we can use the FIRST_VALUE function in the following way:

```sql
SELECT
  FIRST_VALUE(employee_name) OVER (ORDER BY salary DESC) AS first_employee_name,
  FIRST_VALUE(salary) OVER (ORDER BY salary DESC) AS first_employee_salary
FROM
  employees;
```

The above query will return the following result:

| first_employee_name | first_employee_salary |
|---------------------|----------------------|
| Bob                 | 6000                 |
| Bob                 | 6000                 |
| Bob                 | 6000                 |
| Bob                 | 6000                 |
| Bob                 | 6000                 |

As you can see, the FIRST_VALUE function retrieves the first employee's name and salary, which is Bob with a salary of 6000, based on the highest salary.

## Conclusion

In conclusion, SQL's FIRST_VALUE function is a useful tool for retrieving the first value within a group of rows based on a specified order. It allows you to easily extract relevant information from your data, making it a valuable function in SQL queries.

# References
- [SQL FIRST_VALUE Function - Oracle](https://docs.oracle.com/en/database/oracle/oracle-database/21/sqlrf/FIRST_VALUE.html#GUID-1C714E76-385A-4F44-9993-1B097898E282)
- [SQL FIRST_VALUE Function - PostgreSQL](https://www.postgresql.org/docs/12/functions-window.html)