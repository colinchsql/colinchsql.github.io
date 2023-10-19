---
layout: post
title: "How to use the FIRST_VALUE function in SELECT statements"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

In SQL, the `FIRST_VALUE` function is used to retrieve the first value in an ordered set of values, based on a specific ordering criteria. This function can be useful when you want to extract the first occurrence of a value from a group or partition of rows.

To use the `FIRST_VALUE` function, you need to specify the column you want to retrieve the first value from as well as the ordering criteria. Here's the syntax:

```sql
SELECT FIRST_VALUE(column_name) OVER (ORDER BY ordering_criteria) AS first_value
FROM table_name;
```

Let's break down the syntax:

- `FIRST_VALUE(column_name)`: Specifies the column from which you want to retrieve the first value.
- `OVER (ORDER BY ordering_criteria)`: Defines the ordering criteria for the set of values. You can order by one or more columns.
- `AS first_value`: Assigns a name to the retrieved value.

For example, let's say you have a table called `employees` with columns `employee_id`, `employee_name`, and `salary`. You want to retrieve the first value of salary for each employee based on their employee_id. You can use the following query:

```sql
SELECT FIRST_VALUE(salary) OVER (PARTITION BY employee_id ORDER BY employee_id) AS first_salary
FROM employees;
```

In the above query, we are partitioning the rows by `employee_id`, so the `FIRST_VALUE` function will retrieve the first salary for each unique employee_id.

The result of the query will be a set of rows where each row contains the first salary for each employee.

Using the `FIRST_VALUE` function can be helpful in scenarios where you need to retrieve the first occurrence of a value within a group or partition.