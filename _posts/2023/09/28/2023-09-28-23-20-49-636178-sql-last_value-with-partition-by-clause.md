---
layout: post
title: "SQL LAST_VALUE with PARTITION BY clause"
description: " "
date: 2023-09-28
tags: []
comments: true
share: true
---

In SQL, the LAST_VALUE function is used to obtain the last value in a specified window frame. The PARTITION BY clause is used to divide the result set into partitions based on a specified column or expression. In this blog post, we will explore how to use the LAST_VALUE function with the PARTITION BY clause in SQL.

## Syntax

The syntax for using LAST_VALUE with the PARTITION BY clause is as follows:

```sql
LAST_VALUE(column_name) OVER (
    [PARTITION BY partition_column]
    ORDER BY order_column 
    [ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW]
)
```

- `column_name`: Specifies the column for which you want to get the last value.
- `partition_column`: Divides the result set into partitions based on the values in this column. It is optional to use this clause.
- `order_column`: Specifies the column based on which the last value is determined.
- `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: Defines the window frame within which the function is applied. This clause is optional and if omitted, the function considers all rows in the partition.

## Example

Let's assume we have a table called `orders` with the following data:

| order_id | customer_id | order_date  | order_amount |
|----------|-------------|-------------|--------------|
| 1        | 1           | 2022-01-01  | 100          |
| 2        | 1           | 2022-02-01  | 200          |
| 3        | 2           | 2022-01-15  | 150          |
| 4        | 2           | 2022-02-28  | 300          |
| 5        | 2           | 2022-03-10  | 250          |

To find the last order amount for each customer, we can use the LAST_VALUE function with the PARTITION BY clause as shown below:

```sql
SELECT DISTINCT
    customer_id,
    LAST_VALUE(order_amount) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS last_order_amount
FROM
    orders
```

In the above example, we are partitioning the result set by the `customer_id` column and ordering it by the `order_date` column. The LAST_VALUE function then returns the last `order_amount` for each customer.

The output of the above query will be:

| customer_id | last_order_amount |
|-------------|------------------|
| 1           | 200              |
| 2           | 250              |

In conclusion, the LAST_VALUE function with the PARTITION BY clause allows you to retrieve the last value within each partition in SQL. It is a powerful tool for analyzing data and performing calculations on a specific subset of the result set.