---
layout: post
title: "SQL LAST_VALUE with IGNORE NULLS option"
description: " "
date: 2023-09-28
tags: [LastValue, IgnoreNulls]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to retrieve the last value in a group of rows. However, by default, it includes `NULL` values in the calculation. If you want to ignore `NULL` values and retrieve the last non-null value, you can make use of the `IGNORE NULLS` option in SQL.

Here's an example to illustrate how to use the `LAST_VALUE` function with `IGNORE NULLS`:

```sql
SELECT 
    product_id,
    quantity,
    LAST_VALUE(quantity IGNORE NULLS) OVER (PARTITION BY product_id ORDER BY order_date) AS last_quantity
FROM
    orders;
```

In the above example, we have a table called `orders` with columns `product_id`, `quantity`, and `order_date`. We want to retrieve the last non-null `quantity` value for each `product_id`.

The `LAST_VALUE` function is used with the `IGNORE NULLS` option inside the `OVER` clause. The `PARTITION BY` clause is used to define the groups based on the `product_id` column. The `ORDER BY` clause is used to specify the order of the rows within each group.

By using the `LAST_VALUE(quantity IGNORE NULLS)`, the function will return the last non-null `quantity` value for each group of `product_id`.

### Conclusion

The `LAST_VALUE` function in SQL is a powerful tool for retrieving the last value in a group of rows. By using the `IGNORE NULLS` option, you can exclude `NULL` values and retrieve the last non-null value instead. This can be particularly useful when working with datasets that contain missing or null values.

#SQL #LastValue #IgnoreNulls