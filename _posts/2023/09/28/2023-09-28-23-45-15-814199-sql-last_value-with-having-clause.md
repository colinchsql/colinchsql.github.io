---
layout: post
title: "SQL LAST_VALUE with HAVING clause"
description: " "
date: 2023-09-28
tags: [LAST_VALUE, HAVING]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function allows us to access the last value in a set of rows according to a specified order. We can further filter the results using the `HAVING` clause, which is used to filter group rows created by the `GROUP BY` clause.

## Syntax

The syntax for using `LAST_VALUE` with `HAVING` clause is as follows:
```
SELECT column1, ..., LAST_VALUE(column2) OVER (PARTITION BY column3 ORDER BY column4) AS last_value
FROM table_name
GROUP BY column1, ...
HAVING condition;
```

## Example

Let's say we have a table called "orders" with the following columns: "order_id", "customer_id", "product_name", and "order_date".

To find the last order date for each customer who has more than 3 orders, we can use the `LAST_VALUE` function with the `HAVING` clause. The SQL query would be as follows:

```sql
SELECT customer_id, 
       LAST_VALUE(order_date) OVER (PARTITION BY customer_id ORDER BY order_date) AS last_order_date
FROM orders
GROUP BY customer_id
HAVING COUNT(*) > 3;
```

In this example, we partition the result set by the "customer_id" column and order it by the "order_date". We then use the `LAST_VALUE` function to retrieve the last order date for each customer. The `HAVING` clause filters the result set to only include customers who have more than 3 orders.

This query will give us a result set containing the "customer_id" and the corresponding "last_order_date" for all customers who have made more than 3 orders.

## Conclusion

Using the `LAST_VALUE` function with the `HAVING` clause in SQL allows us to find the last value in a set of rows and further filter the results based on specific conditions. It is a powerful tool for analyzing data and extracting meaningful insights.

#SQL #LAST_VALUE #HAVING