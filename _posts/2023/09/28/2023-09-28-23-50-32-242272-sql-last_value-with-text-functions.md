---
layout: post
title: "SQL LAST_VALUE with text functions"
description: " "
date: 2023-09-28
tags: []
comments: true
share: true
---

In SQL, the LAST_VALUE function is used to return the last value in an ordered set of data based on a specified column. This function can be especially useful when working with text values, as it allows us to apply text functions to the last value.

## Example Scenario

Let's say we have a table named `products` with the following schema:

| product_id | product_name |
|------------|--------------|
| 1          | Apple        |
| 2          | Banana       |
| 3          | Cherry       |
| 4          | Durian       |
| 5          | Elderberry   |

We want to find the last product name that starts with the letter 'B' and convert it to uppercase.

## SQL Code Example

```sql
SELECT LAST_VALUE(UPPER(product_name)) OVER (
    ORDER BY product_id
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
) AS last_product_starting_with_b
FROM products
WHERE product_name LIKE 'B%';
```

Explanation of the code:
- The `LAST_VALUE` function is applied to the `product_name` column to get the last value.
- `UPPER` is a text function used to convert the last value to uppercase.
- The `OVER` clause specifies the window in which the `LAST_VALUE` function is evaluated.
- `ORDER BY product_id` ensures the data is ordered based on the product_id column.
- `ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING` includes all rows within the window.

The resulting output will be:

| last_product_starting_with_b |
|------------------------------|
| BANANA                       |

## Conclusion

Using the `LAST_VALUE` function in combination with text functions allows us to perform data transformations on the last value in an ordered set of data. This can be beneficial when working with text values and needing to extract specific information from the last value.