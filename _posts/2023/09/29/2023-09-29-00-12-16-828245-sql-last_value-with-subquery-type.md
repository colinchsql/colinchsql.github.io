---
layout: post
title: "SQL LAST_VALUE with subquery type"
description: " "
date: 2023-09-29
tags: [WindowFunctions]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to fetch the last value within a specific window or partition. It is commonly used for time series analysis or when you need to access the last record in a dataset based on a specific ordering.

In this blog post, we will specifically explore how to use `LAST_VALUE` with a subquery type in SQL. This scenario arises when we want to retrieve the last value from a subquery result set.

Let's consider the following example of an imaginary table called `sales`:

```sql
CREATE TABLE sales (
    id INT,
    product_id INT,
    sale_date DATE,
    revenue DECIMAL(10,2)
);
```

Suppose we have data in the `sales` table as follows:

| id | product_id | sale_date  | revenue |
|----|------------|------------|---------|
| 1  | 100        | 2021-01-01 | 100.00  |
| 2  | 100        | 2021-01-02 | 150.00  |
| 3  | 200        | 2021-01-01 | 75.00   |
| 4  | 200        | 2021-01-02 | 110.50  |

Now let's say we want to retrieve the last sale revenue for each product. We can achieve this using the `LAST_VALUE` function with a subquery type. Here's an example query:

```sql
SELECT DISTINCT
    product_id,
    LAST_VALUE(revenue) OVER (PARTITION BY product_id ORDER BY sale_date 
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS last_revenue
FROM
    sales
```

In the above query, we first order the rows by `sale_date` within each partition of `product_id`. Then, we use the `LAST_VALUE` function with a window frame that includes all rows using `ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING`. The `DISTINCT` keyword is used to remove any duplicate results.

The result of the above query would be:

| product_id | last_revenue |
|------------|--------------|
| 100        | 150.00       |
| 200        | 110.50       |

By using `LAST_VALUE` with a subquery type, we were able to retrieve the last sale revenue for each product.

In conclusion, the `LAST_VALUE` function in SQL is a useful tool for accessing the last value within a specified window or partition. When combined with a subquery type, it allows us to fetch the last value from a subquery result set, as demonstrated in this blog post.

#SQL #WindowFunctions