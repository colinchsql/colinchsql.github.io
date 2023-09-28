---
layout: post
title: "SQL LAST_VALUE with ALL keyword"
description: " "
date: 2023-09-28
tags: []
comments: true
share: true
---

When working with SQL, you might come across scenarios where you need to retrieve the last value from a specific column in a table. SQL provides the `LAST_VALUE` function to facilitate this requirement. In addition to the `LAST_VALUE` function, you can also utilize the `ALL` keyword to further customize your query results. In this blog post, we'll explore how to use the `LAST_VALUE` function with the `ALL` keyword in SQL.

## Syntax of the LAST_VALUE Function

The `LAST_VALUE` function enables you to retrieve the last value from the specified column within a defined window frame. The basic syntax for using the `LAST_VALUE` function in SQL is:

```sql
LAST_VALUE(column) OVER (ORDER BY order_column [ROWS <window_frame>])
```

- `column`: Specifies the column from which the last value needs to be retrieved.
- `ORDER BY order_column`: Defines the column used to order the result set.
- `ROWS <window_frame>`: Optional parameter that specifies the range of rows within which the function is applied.

## Example Scenario

Let's consider a scenario where you have a table named `sales` with the following structure:

| sale_id | product  | quantity | sale_date  |
|---------|----------|----------|------------|
| 1       | Laptop   | 10       | 2021-01-01 |
| 2       | Smartphone | 20      | 2021-01-02 |
| 3       | Tablet   | 15       | 2021-01-03 |
| 4       | Laptop   | 5        | 2021-01-04 |
| 5       | Smartphone | 10      | 2021-01-05 |

You want to retrieve the last quantity sold for each product. The `LAST_VALUE` function with the `ALL` keyword can help you accomplish this task efficiently.

## Usage of LAST_VALUE with ALL

To use the `LAST_VALUE` function with the `ALL` keyword, you need to first partition your result set based on the column you want to retrieve the last value for. In our example scenario, we want to partition the data by the `product` column.

```sql
SELECT DISTINCT product,
  LAST_VALUE(quantity) OVER (PARTITION BY product ORDER BY sale_date
                             ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS last_quantity
FROM sales;
```

In this query, the `LAST_VALUE` function is partitioned by the `product` column and ordered by the `sale_date` column. Using the `ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING` clause, the function considers all rows within the partition.

The `DISTINCT` keyword is used to eliminate duplicate rows and only retrieve the distinct products with their last sold quantity.

## Conclusion

Utilizing the `LAST_VALUE` function with the `ALL` keyword in SQL is an effective way to retrieve the last value from a specific column within each partition. By properly partitioning and ordering the data, you can obtain the desired results efficiently. This technique can be particularly useful in scenarios where you need to analyze historical data or track the latest values.