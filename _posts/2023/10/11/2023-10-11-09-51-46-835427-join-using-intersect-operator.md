---
layout: post
title: "JOIN using INTERSECT operator"
description: " "
date: 2023-10-11
tags: [join]
comments: true
share: true
---

In SQL, the `INTERSECT` operator is used to combine the result of two or more queries and returns only the rows that are common to all queries. It can be used in conjunction with the `JOIN` operator to achieve more complex join operations. In this tutorial, we will explore how to perform a join using the `INTERSECT` operator.

## Syntax

The general syntax for performing a join using the `INTERSECT` operator is as follows:

```sql
SELECT column_list
FROM table1
JOIN table2
  ON join_condition
INTERSECT
SELECT column_list
FROM table3
JOIN table4
  ON join_condition;
```

## Example

Let's consider the following example to understand how to perform a join using the `INTERSECT` operator:

We have two tables, `customers` and `orders`, with the following structure:

**customers table:**

| customer_id | name     |
|-------------|----------|
| 1           | John     |
| 2           | Mary     |
| 3           | David    |
| 4           | Lisa     |

**orders table:**

| order_id | customer_id | product  |
|----------|-------------|----------|
| 1        | 1           | Laptop   |
| 2        | 2           | Phone    |
| 3        | 3           | Monitor  |
| 4        | 2           | Keyboard |
| 5        | 4           | Mouse    |

Now, suppose we want to find the customers who have placed orders for both 'Laptop' and 'Phone' products.

The SQL query to achieve this using the `INTERSECT` operator would be:

```sql
SELECT customers.name
FROM customers
JOIN orders ON customers.customer_id = orders.customer_id
WHERE orders.product = 'Laptop'

INTERSECT

SELECT customers.name
FROM customers
JOIN orders ON customers.customer_id = orders.customer_id
WHERE orders.product = 'Phone';
```

This query will return the name of customers who have placed orders for both 'Laptop' and 'Phone' products:

| name  |
|-------|
| Mary  |

In this example, the `JOIN` operator is used to join the `customers` table and the `orders` table on the `customer_id` column. Then, the `INTERSECT` operator is used to find the common customers who have placed orders for both 'Laptop' and 'Phone' products.

By using the `INTERSECT` operator, we can perform more complex joins and get the desired result set.

That's it! You have learned how to perform a join using the `INTERSECT` operator in SQL. Start applying this technique to your own projects and explore the power of combining queries to get the desired results.

#sql #join