---
layout: post
title: "Using aggregate functions in SQL CLI"
description: " "
date: 2023-10-16
tags: [AggregateFunctions]
comments: true
share: true
---

When working with SQL (Structured Query Language) in the command line interface (CLI), you often need to perform calculations on sets of data. This is where aggregate functions come in handy. Aggregate functions allow you to perform calculations on a group of rows and return a single value as the result.

In this blog post, we will explore the usage of aggregate functions in SQL CLI through examples and explanations.

### 1. COUNT Function

The `COUNT` function is used to count the number of rows in a specified column or table. It can be used with the `SELECT` statement to retrieve the count of records that match certain criteria.

Let's say we have a table called `employees` with columns `id`, `name`, and `department`. To count the number of employees in each department, we can use the following query:

```sql
SELECT department, COUNT(*) as employee_count
FROM employees
GROUP BY department;
```

In this example, `COUNT(*)` represents the count of all rows in each group, which is the number of employees in each department.

### 2. SUM Function

The `SUM` function is used to calculate the sum of values in a specified column. It is commonly used with numerical columns.

Let's say we have a table called `orders` with columns `order_id`, `customer_id`, and `total_amount`. To calculate the total sales amount for each customer, we can use the following query:

```sql
SELECT customer_id, SUM(total_amount) as total_sales
FROM orders
GROUP BY customer_id;
```

This query will sum up the `total_amount` for each `customer_id` and return the total sales amount for each customer.

### 3. AVG Function

The `AVG` function is used to calculate the average value of a specified column. It is often used with numerical columns.

Let's say we have a table called `products` with columns `product_id`, `category`, and `price`. To calculate the average price for each category, we can use the following query:

```sql
SELECT category, AVG(price) as average_price
FROM products
GROUP BY category;
```

This query will calculate the average price for each category and return the result.

### 4. MAX and MIN Functions

The `MAX` and `MIN` functions are used to find the maximum and minimum values respectively in a specified column.

Let's say we have a table called `students` with columns `student_id`, `name`, and `score`. To find the highest and lowest scores for each student, we can use the following query:

```sql
SELECT student_id, name, MAX(score) as highest_score, MIN(score) as lowest_score
FROM students
GROUP BY student_id, name;
```

This query will find the highest and lowest scores for each student and return the results.

These are just a few examples of the aggregate functions available in SQL CLI. You can use them to perform various calculations and analysis on your data.

Remember, when using aggregate functions, you need to use the `GROUP BY` clause to specify the grouping criteria. This allows the aggregate functions to operate on subsets of the data.

I hope this blog post has provided you with a good understanding of how to use aggregate functions in SQL CLI. Happy querying!

**#SQL #AggregateFunctions**