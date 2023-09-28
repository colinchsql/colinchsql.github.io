---
layout: post
title: "SQL LAST_VALUE with stored procedure type"
description: " "
date: 2023-09-29
tags: [StoredProcedures]
comments: true
share: true
---

In SQL, the `LAST_VALUE()` function is used to return the last value in an ordered set of values. It is often used in conjunction with a combination of window functions for data analysis and reporting purposes.

## Syntax

The syntax for the `LAST_VALUE()` function is as follows:

```sql
LAST_VALUE(expression) OVER (
    [PARTITION BY partition_expression]
    ORDER BY sort_expression [ASC | DESC]
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
)
```

## Example

Let's consider a scenario where we have a table called `products` with columns `product_id`, `product_name`, and `price`. We want to fetch the last sold price for each product using the `LAST_VALUE()` function within a stored procedure.

```sql
CREATE PROCEDURE GetLastPriceByProduct
AS
BEGIN
    SELECT DISTINCT product_id, 
        LAST_VALUE(price) OVER (
            PARTITION BY product_id 
            ORDER BY last_sold_date DESC
            ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
        ) AS last_sold_price
    FROM products;
END
```

In the above example, we create a stored procedure named `GetLastPriceByProduct`. Inside the procedure, we use the `LAST_VALUE()` function to get the last sold price for each product based on the `last_sold_date` column, sorted in descending order. The `PARTITION BY` clause is used to group the records by `product_id`.

To execute the stored procedure and obtain the last sold prices for each product, you can simply call the procedure:

```sql
EXEC GetLastPriceByProduct;
```

This will return a result set containing the `product_id` and the corresponding `last_sold_price` for each product.

## Conclusion

The `LAST_VALUE()` function in SQL is a powerful tool for retrieving the last value in an ordered set of data. By utilizing this function within a stored procedure, you can efficiently obtain the last sold price or any other desired information based on specific criteria. It's an excellent way to analyze and report on your data effectively.

#SQL #StoredProcedures