---
layout: post
title: "SQL LAST_VALUE with IN operator"
description: " "
date: 2023-09-28
tags: [LAST_VALUE]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to return the last value in a group of rows based on an ordering. This can be useful when you want to retrieve the latest or most recent value from a set of data.

The `IN` operator, on the other hand, is used to specify multiple values in a WHERE clause. It allows you to retrieve data where the value of a specific column matches any of the values specified.

Combining the `LAST_VALUE` function with the `IN` operator can be beneficial when you want to retrieve the last value of a column from a subset of rows meeting specific criteria.

## Syntax

The basic syntax for using the `LAST_VALUE` function with the `IN` operator is as follows:

```sql
SELECT LAST_VALUE(column_name) OVER (PARTITION BY partition_col ORDER BY order_col) AS last_value
FROM table_name
WHERE column_name IN (value1, value2, ...)
```

- `column_name`: The name of the column from which you want to retrieve the last value.
- `partition_col`: The column used for dividing the result set into partitions. The `LAST_VALUE` function will operate within each of these partitions separately.
- `order_col`: The column used for ordering the rows within each partition.
- `table_name`: The name of the table containing the data.
- `value1`, `value2`, etc.: The values to match against the `column_name` using the `IN` operator.

## Example

Let's suppose we have a table named `sales` with the following structure:

| product_id | sale_date  | sale_amount |
|------------|------------|-------------|
| 1          | 2021-05-01 | 100         |
| 1          | 2021-05-05 | 150         |
| 2          | 2021-04-30 | 200         |
| 2          | 2021-05-07 | 300         |

To retrieve the last sale amount for products with `product_id` 1 and 2, we can use the following SQL query:

```sql
SELECT LAST_VALUE(sale_amount) OVER (PARTITION BY product_id ORDER BY sale_date) AS last_sale_amount
FROM sales
WHERE product_id IN (1, 2)
```

The result of this query will be:

| last_sale_amount |
|------------------|
| 150              |
| 300              |

Here, the `LAST_VALUE` function is applied to the `sale_amount` column, partitioned by `product_id`, and ordered by `sale_date`. The `WHERE` clause filters the rows for `product_id` 1 and 2 only.

In this way, we are able to retrieve the last sale amount for each product based on the specified criteria.

#SQL #LAST_VALUE #IN