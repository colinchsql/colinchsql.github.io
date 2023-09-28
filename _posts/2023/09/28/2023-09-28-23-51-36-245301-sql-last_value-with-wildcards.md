---
layout: post
title: "SQL LAST_VALUE with wildcards"
description: " "
date: 2023-09-28
tags: [LAST_VALUE, wildcards]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to retrieve the last value in a specified column within a specific partition or result set. By default, the `LAST_VALUE` function retrieves the last non-null value in the column. However, sometimes we may want to perform a search using wildcards and retrieve the last value that matches the pattern.

To achieve this, we can utilize the `%` wildcard operator in conjunction with the `LAST_VALUE` function. The `%` wildcard represents zero or more characters in the pattern. Let's take a look at an example:

```sql
SELECT
  product_name,
  LAST_VALUE(product_name) OVER (
    ORDER BY product_id
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
  ) AS last_product_name
FROM
  products
WHERE
  product_name LIKE '%Widget%'
ORDER BY
  product_id;
```

In the above example, we have a table named `products` with columns `product_id` and `product_name`, where we want to retrieve the last value of `product_name` that contains the word "Widget". 

Here, we use the `LAST_VALUE` function with the `OVER` clause to specify the window frame as `ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING`, which includes all rows in the partition. The `ORDER BY` clause orders the result set by `product_id`.

Finally, we apply a `WHERE` clause to filter the rows based on the `product_name` containing the word "Widget". The last value with the pattern "Widget" will be returned as `last_product_name`.

By combining the `LAST_VALUE` function with wildcards, we can easily retrieve the last matching value in SQL based on a specific pattern. This can be particularly useful when working with tables containing historical data or when tracking changes over time.

Remember to adjust the table and column names in the example code to match your actual database schema.

#SQL #LAST_VALUE #wildcards