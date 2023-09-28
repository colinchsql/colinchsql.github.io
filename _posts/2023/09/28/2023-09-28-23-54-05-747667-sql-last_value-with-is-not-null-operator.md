---
layout: post
title: "SQL LAST_VALUE with IS NOT NULL operator"
description: " "
date: 2023-09-28
tags: [LAST_VALUE, IS_NOT_NULL]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to fetch the last value in a specific window frame. It is commonly used in conjunction with the `IS NOT NULL` operator to filter out any NULL values.

Here's an example of how you can use the `LAST_VALUE` function with the `IS NOT NULL` operator:

```sql
SELECT 
    column1,
    LAST_VALUE(column2) OVER (ORDER BY column3 ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS last_value_column
FROM 
    table_name
WHERE 
    column2 IS NOT NULL;
```

In the above example:
- `column1` is the column you want to select in the result set.
- `column2` is the column from which you want to fetch the last value.
- `column3` is the column used for ordering the result set.
- `table_name` is the name of the table you are querying.

The `ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING` clause ensures that the window frame for the `LAST_VALUE` function encompasses all rows in the table.

The `WHERE` clause `column2 IS NOT NULL` filters out any rows where `column2` has a NULL value.

By combining the `LAST_VALUE` function with the `IS NOT NULL` operator and proper window framing, you can retrieve the last non-NULL value from a specific column in your SQL query. This can be useful when analyzing time series data or retrieving the most recent value in a dataset.

#SQL #LAST_VALUE #IS_NOT_NULL