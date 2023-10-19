---
layout: post
title: "Using FIRST_VALUE in stored procedures"
description: " "
date: 2023-10-20
tags: [GUID, function]
comments: true
share: true
---

In stored procedures, we often need to work with data and perform various operations on it. One such operation is finding the first value in a set of rows based on a specific order. This can be achieved using the `FIRST_VALUE` function in SQL.

## Understanding FIRST_VALUE

The `FIRST_VALUE` function is a window function in SQL that allows us to retrieve the first value from a set of rows within a partition. It is commonly used in scenarios where we need to find the earliest or first occurrence of a value based on a certain ordering.

## Syntax

The syntax for using `FIRST_VALUE` in a SQL stored procedure is as follows:

```sql
FIRST_VALUE (expression) OVER (PARTITION BY column_name ORDER BY order_column [ASC|DESC])
```

- `expression`: The column or expression from which to retrieve the first value.
- `PARTITION BY`: Optional clause used to divide the rows into partitions based on a specific column.
- `column_name`: The column used to create partitions if `PARTITION BY` is specified.
- `ORDER BY`: The column used to determine the order of the rows within each partition.
- `[ASC|DESC]`: Optional sorting order. By default, it is ascending (`ASC`).

## Example Usage

Let's consider a table named `Employees` with the following structure:

| EmployeeID | EmployeeName | Department | Salary |
|------------|--------------|------------|--------|
| 1          | John         | HR         | 5000   |
| 2          | Jane         | IT         | 6000   |
| 3          | Adam         | HR         | 5500   |
| 4          | Sarah        | IT         | 6500   |
| 5          | Michael      | Sales      | 4500   |

To find the first employee in each department based on their salary, we can use the `FIRST_VALUE` function:

```sql
SELECT DISTINCT
    FIRST_VALUE(EmployeeName) OVER (PARTITION BY Department ORDER BY Salary) AS FirstEmployee,
    Department
FROM
    Employees;
```

This will return the following result:

| FirstEmployee | Department |
|---------------|------------|
| John          | HR         |
| Sarah         | IT         |
| Michael       | Sales      |

In this example, we partitioned the rows by the `Department` column and ordered them by the `Salary` column. The `FIRST_VALUE` function then returned the first employee name within each department based on the ordering.

## Conclusion

The `FIRST_VALUE` function is a powerful tool in SQL that allows us to retrieve the first value in a set of rows based on a specific ordering. It can be used in stored procedures to perform various operations on data. By understanding its syntax and usage, you can utilize `FIRST_VALUE` effectively and efficiently in your SQL stored procedures.

References:
- [Microsoft SQL Server Documentation on FIRST_VALUE](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql?view=sql-server-ver15)
- [Oracle Database Documentation on FIRST_VALUE](https://docs.oracle.com/en/database/oracle/oracle-database/21/sqlrf/FIRST_VALUE.html#GUID-8A3AED9E-3F7D-4992-A795-9A82E2E2C3BC)
- [MySQL Documentation on FIRST_VALUE](https://dev.mysql.com/doc/refman/8.0/en/window-function-descriptions.html#function_first-value)