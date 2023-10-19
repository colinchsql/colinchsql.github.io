---
layout: post
title: "Syntax of the FIRST_VALUE function in SQL"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

In SQL, the FIRST_VALUE function is used to retrieve the first value of an expression within a group. It is commonly used with the WINDOW clause to define the group of rows to consider.

The syntax of the FIRST_VALUE function can be expressed as follows:

```
FIRST_VALUE ( expression ) OVER (
    [PARTITION BY partition_expression]
    [ORDER BY order_expression [ASC | DESC]]
    [ROWS {UNBOUNDED PRECEDING | integer PRECEDING | CURRENT ROW | integer FOLLOWING | UNBOUNDED FOLLOWING}]
)
```

Let's break down the elements of the syntax:

- `expression`: This is the column or expression for which we want to retrieve the first value. It can be any valid SQL expression.

- `PARTITION BY`: This clause is optional and allows us to divide the rows into partitions. The FIRST_VALUE function will operate on each partition separately. If omitted, the function will consider all rows as a single partition.

- `ORDER BY`: This clause is optional and specifies the order in which the rows are evaluated. The FIRST_VALUE function will retrieve the first value based on this order. By default, the order is ascending (`ASC`), but we can also specify descending order (`DESC`).

- `ROWS`: This clause is optional and defines the range of rows to consider relative to the current row. We can use keywords like `UNBOUNDED PRECEDING`, `CURRENT ROW`, or specify a number of rows `integer PRECEDING` or `integer FOLLOWING`. This is useful when we want to include a subset of rows for calculation.

Here is an example usage of the FIRST_VALUE function:

```sql
SELECT
    employee_name,
    department,
    salary,
    FIRST_VALUE(salary) OVER (PARTITION BY department ORDER BY salary DESC) AS highest_salary
FROM
    employees
```

In this example, the `FIRST_VALUE` function is used to retrieve the highest salary within each department. The `PARTITION BY` clause divides the rows by department, and the `ORDER BY` clause sorts the salaries in descending order. The result will include the employee name, department, salary, and the highest salary within each department.

For further details and examples, refer to the documentation of your specific SQL database system or consult relevant SQL books and resources.

**References:**
- [Microsoft Docs - FIRST_VALUE function](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql?view=sql-server-ver15)
- [Oracle Docs - FIRST_VALUE function](https://docs.oracle.com/en/database/oracle/oracle-database/21/sqlrf/FIRST_VALUE.html)
- [PostgreSQL Docs - FIRST_VALUE function](https://www.postgresql.org/docs/current/functions-window.html)