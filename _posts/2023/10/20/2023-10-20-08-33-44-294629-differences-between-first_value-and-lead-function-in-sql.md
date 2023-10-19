---
layout: post
title: "Differences between FIRST_VALUE and LEAD function in SQL"
description: " "
date: 2023-10-20
tags: [GUID]
comments: true
share: true
---

In SQL, the `FIRST_VALUE` and `LEAD` functions are commonly used to analyze and manipulate data in a table. While they may seem similar at first glance, these two functions serve different purposes. Let's explore the differences between `FIRST_VALUE` and `LEAD` functions in SQL.

## FIRST_VALUE function

The `FIRST_VALUE` function returns the first value in an ordered set of values for each row within a specified window. It allows you to retrieve the first value based on a certain ordering condition within a specific group.

The syntax for the `FIRST_VALUE` function is as follows:
```sql
FIRST_VALUE(expression) OVER (PARTITION BY column_name ORDER BY ordering_condition) AS alias_name
```
Here, `expression` is the column or expression you want to retrieve the first value of, `column_name` is the column used for partitioning the result set, `ordering_condition` is the column or expression used for ordering, and `alias_name` is the optional alias for the result.

For example, if we have a table named `employees` with columns `employee_id`, `employee_name`, and `salary`, and we want to retrieve the first salary for each employee based on the ordering of employee names, we can use the `FIRST_VALUE` function as follows:

```sql
SELECT employee_id, employee_name, salary,
       FIRST_VALUE(salary) OVER (PARTITION BY employee_id ORDER BY employee_name) AS first_salary
FROM employees;
```

## LEAD function

On the other hand, the `LEAD` function allows you to access the value of a specified expression from a subsequent row within the same result set. It is useful when you want to retrieve values from a row that follows the current row.

The syntax for the `LEAD` function is as follows:
```sql
LEAD(expression, offset, default_value) OVER (PARTITION BY column_name ORDER BY ordering_condition) AS alias_name
```
Here, `expression` is the value you want to retrieve, `offset` is the number of rows forwards from the current row where the value should be retrieved, `default_value` is the optional value to be returned if the offset row does not exist, `column_name` is the column used for partitioning the result set, `ordering_condition` is the column or expression used for ordering, and `alias_name` is the optional alias for the result.

For example, if we have a table named `sales` with columns `transaction_id`, `sale_date`, and `amount`, and we want to retrieve the amount of the next transaction for each sale date based on the ordering of transaction IDs, we can use the `LEAD` function as follows:

```sql
SELECT transaction_id, sale_date, amount,
       LEAD(amount, 1, 0) OVER (PARTITION BY sale_date ORDER BY transaction_id) AS next_transaction_amount
FROM sales;
```

The above query will return the transaction ID, sale date, amount, and the amount of the next transaction for each sale date.

In summary, the `FIRST_VALUE` function retrieves the first value in a window based on an ordering condition, while the `LEAD` function retrieves the value from a subsequent row within the same result set. Understanding the differences between these two functions is essential for accurately analyzing and manipulating data in SQL.

### Relevant References
- [Oracle Documentation on FIRST_VALUE function](https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/FIRST_VALUE.html#GUID-4A1A1CDF-4687-4C20-9D76-4A29F0C10E05)
- [Microsoft SQL Server Documentation on LEAD function](https://docs.microsoft.com/en-us/sql/t-sql/functions/lead-transact-sql?view=sql-server-ver15)