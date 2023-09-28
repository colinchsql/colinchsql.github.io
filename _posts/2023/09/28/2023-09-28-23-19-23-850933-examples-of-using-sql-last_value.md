---
layout: post
title: "Examples of using SQL LAST_VALUE"
description: " "
date: 2023-09-28
tags: [WindowFunctions]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to retrieve the last value in an ordered set of values. It is commonly used in scenarios where you want to access the most recent value in a specific order. The `LAST_VALUE` function can be used with other window functions, such as `PARTITION BY` and `ORDER BY`, to further refine the results.

Here are a few examples of how to use the `LAST_VALUE` function in SQL:

## Example 1: Retrieve the last value in a column

Suppose you have a table named `employees` with columns `employee_id`, `name`, and `salary`. You want to find the last (most recent) salary of each employee based on their employee_id. You can use the `LAST_VALUE` function to achieve this:

```sql
SELECT DISTINCT employee_id, 
  LAST_VALUE(salary) OVER (PARTITION BY employee_id ORDER BY employee_id) AS last_salary
FROM employees;
```

In this example, we use the `LAST_VALUE` function with the `PARTITION BY` clause to group the results by `employee_id`. The `ORDER BY` clause is used to specify the order in which the values should be considered. The result is a distinct list of employee IDs with their corresponding last salary.

## Example 2: Retrieve the last non-null value in a column

Sometimes, you may have a column with null values, and you want to retrieve the last non-null value for each row. The `LAST_VALUE` function can help you achieve this as well. 

```sql
SELECT employee_id, name,
  LAST_VALUE(salary IGNORE NULLS) OVER (ORDER BY employee_id) AS last_non_null_salary
FROM employees;
```

In this example, we use the `IGNORE NULLS` option with the `LAST_VALUE` function to skip the null values while determining the last non-null salary. The `ORDER BY` clause is used to specify the order in which the values should be considered.

## Conclusion

The `LAST_VALUE` function is a powerful tool in SQL to retrieve the last value in a set of ordered values. It is useful in various scenarios, such as finding the most recent value or the last non-null value in a column. By leveraging its capabilities with window functions like `PARTITION BY` and `ORDER BY`, you can further fine-tune the results to meet your specific requirements.

#SQL #WindowFunctions