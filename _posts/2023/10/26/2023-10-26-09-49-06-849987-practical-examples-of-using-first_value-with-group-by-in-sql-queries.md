---
layout: post
title: "Practical examples of using FIRST_VALUE with GROUP BY in SQL queries"
description: " "
date: 2023-10-26
tags: [Database]
comments: true
share: true
---

In SQL, the `FIRST_VALUE` function allows you to retrieve the first value from a group of rows when using the `GROUP BY` clause. This function is handy when you need to find the first occurrence of a specific value within each group. In this article, we will explore some practical examples of using `FIRST_VALUE` with `GROUP BY` to enhance your SQL queries.

## Example 1: Retrieve the earliest order date for each customer

Suppose you have a table called `orders` that contains information about customer orders, including the `customer_id` and `order_date`. You want to find the earliest order date for each customer. Here's how you can achieve that using `FIRST_VALUE` with `GROUP BY`:

```sql
SELECT customer_id, FIRST_VALUE(order_date) OVER (PARTITION BY customer_id ORDER BY order_date ASC) AS earliest_order_date
FROM orders
GROUP BY customer_id;
```

In this query, we are using `FIRST_VALUE` with the `OVER` clause to specify that we want to retrieve the first value (`order_date`) for each group (`customer_id`). The `PARTITION BY` clause ensures that the grouping is done based on the `customer_id`, and the `ORDER BY` clause within the `OVER` clause determines the order in which the rows are considered to find the first value.

## Example 2: Find the highest-paid employee in each department

Consider a table called `employees` that contains employee information, including the `employee_id`, `department_id`, and `salary`. You want to determine the highest-paid employee in each department. Here's how you can use `FIRST_VALUE` with `GROUP BY` to achieve that:

```sql
SELECT department_id, FIRST_VALUE(employee_id) OVER (PARTITION BY department_id ORDER BY salary DESC) AS highest_paid_employee_id
FROM employees
GROUP BY department_id;
```

In this query, we are using `FIRST_VALUE` with the `OVER` clause to retrieve the first value (`employee_id`) for each group (`department_id`). The `PARTITION BY` clause ensures that the grouping is done based on the `department_id`, and the `ORDER BY` clause within the `OVER` clause determines the order in which the rows are considered to find the first value.

By using `FIRST_VALUE` with `GROUP BY`, you can easily retrieve the first value within each group in your SQL queries. This can be particularly useful when you need to find the earliest or highest value for each group. Experiment with these examples in your own database to see the power of `FIRST_VALUE` with `GROUP BY` firsthand!

**References:**

- [Microsoft SQL Server Documentation: FIRST_VALUE function](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql)
- [Oracle Documentation: FIRST_VALUE function](https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/FIRST_VALUE.html)
- [PostgreSQL Documentation: Window Functions](https://www.postgresql.org/docs/current/functions-window.html) 

\#SQL \#Database