---
layout: post
title: "SQL LAST_VALUE with ROWS BETWEEN clause"
description: " "
date: 2023-09-28
tags: [WindowFunctions]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to retrieve the last value in a specified column within a window frame. This function can be further enhanced by using the `ROWS BETWEEN` clause, which allows you to define the range of rows to consider when applying the `LAST_VALUE` function.

Here's an example to demonstrate how to use `LAST_VALUE` with the `ROWS BETWEEN` clause:

```sql
SELECT product_name, sale_date, quantity,
       LAST_VALUE(quantity) OVER (PARTITION BY product_name
                                  ORDER BY sale_date
                                  ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS last_quantity
FROM sales_table;
```

In the above code snippet, we are selecting the `product_name`, `sale_date`, `quantity` columns, and using the `LAST_VALUE` function on the `quantity` column. The `OVER` clause is followed by the `PARTITION BY` clause, which divides the data into partitions based on the `product_name` column. The `ORDER BY` clause sorts the partitions by the `sale_date` column.

The `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` specifies the range of rows to consider for the `LAST_VALUE` function. In this case, it includes all the rows from the start of the partition up to the current row.

The result of this query will include an additional column called `last_quantity`, which contains the last value of the `quantity` column within each partition.

By using the `ROWS BETWEEN` clause, you have the flexibility to modify the range of rows according to your specific requirements. For instance, you could change it to `ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING` to consider the previous and next row along with the current row.

**#SQL #WindowFunctions**

Using `LAST_VALUE` with the `ROWS BETWEEN` clause provides a powerful way to obtain the last value of a column within a specified range of rows. Whether you need to track the last transaction, inventory levels, or any other data point, this SQL feature can be quite handy.