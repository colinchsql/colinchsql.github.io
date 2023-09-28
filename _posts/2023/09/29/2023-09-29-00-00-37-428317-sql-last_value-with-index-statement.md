---
layout: post
title: "SQL LAST_VALUE with INDEX statement"
description: " "
date: 2023-09-29
tags: []
comments: true
share: true
---

In SQL, the `LAST_VALUE()` function is used to get the last value from an ordered set of values. It is often used in combination with the `OVER` clause to perform calculations on a specific range of rows.

### Syntax

The syntax for using the `LAST_VALUE()` function with the `OVER` clause is as follows:

```
LAST_VALUE(expression) OVER (
    [PARTITION BY column_name]
    ORDER BY column_name
    [ROWS BETWEEN {UNBOUNDED | CURRENT ROW} AND {UNBOUNDED | CURRENT ROW}]
)
```

The `expression` is the column or expression from which you want to get the last value. The `PARTITION BY` clause is optional and is used to divide the result set into partitions based on one or more columns. The `ORDER BY` clause is used to specify the order in which the rows are evaluated. The `ROWS BETWEEN` clause is optional and is used to define the window or frame within which the calculation is performed.

### Example

Consider the following table called `sales`:

```sql
CREATE TABLE sales (
    id INT,
    product_id INT,
    sale_date DATE,
    quantity INT
);

INSERT INTO sales (id, product_id, sale_date, quantity)
VALUES
    (1, 1, '2021-01-01', 10),
    (2, 1, '2021-01-02', 5),
    (3, 1, '2021-01-03', 8),
    (4, 2, '2021-01-01', 15),
    (5, 2, '2021-01-02', 7),
    (6, 2, '2021-01-03', 12);
```

To get the last quantity for each product, you can use the `LAST_VALUE()` function with the `OVER` clause:

```sql
SELECT DISTINCT
    product_id,
    LAST_VALUE(quantity) OVER (
        PARTITION BY product_id
        ORDER BY sale_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
    ) AS last_quantity
FROM sales;
```

This query will return the following result:

```
product_id | last_quantity
-----------+--------------
1          | 8
2          | 12
```

In this example, the `LAST_VALUE()` function is applied to the `quantity` column, and the rows are ordered by the `sale_date` column within each partition of `product_id`. The result set includes distinct `product_id` values with their corresponding last quantities.

Overall, the `LAST_VALUE()` function with the `OVER` clause and the `INDEX` statement can be a powerful combination in SQL to perform advanced calculations on ordered sets of data.