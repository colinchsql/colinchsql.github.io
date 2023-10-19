---
layout: post
title: "Differences between FIRST_VALUE and LAG function in SQL"
description: " "
date: 2023-10-20
tags: [GUID, GUID]
comments: true
share: true
---

When working with SQL, there are often scenarios where we need to retrieve values from previous rows in a result set. Two commonly used functions for this purpose are `FIRST_VALUE` and `LAG`. While both functions allow us to access previous row values, they have some key differences. 

## FIRST_VALUE

The `FIRST_VALUE` function is used to retrieve the first value in an ordered partition of a result set. It allows us to easily access the first value without the need for complex joins or subqueries. Here's a basic example:

```sql
SELECT product_name, first_value(price) OVER (PARTITION BY category_id ORDER BY product_id)
FROM products;
```

In this example, we are retrieving the first price of each product within each category.

## LAG

On the other hand, the `LAG` function allows us to access the value from a preceding row in a result set. It is commonly used for calculating the difference or the change between current and previous values. Here's an example:

```sql
SELECT product_name, price, lag(price) OVER (ORDER BY product_id) as previous_price
FROM products;
```

In this example, we are retrieving the current price along with the previous price of each product.

## Key Differences

1. **Usage**: `FIRST_VALUE` retrieves the first value in an ordered partition, while `LAG` retrieves the value from a preceding row.
2. **Syntax**: `FIRST_VALUE` requires an `OVER` clause with a `PARTITION BY` clause to define the partition, whereas `LAG` requires an `OVER` clause with an `ORDER BY` clause to define the ordering.
3. **Result**: `FIRST_VALUE` returns the same result for all rows within a partition, while `LAG` returns a different value for each row.
4. **NULL Handling**: `FIRST_VALUE` returns NULL if no rows are present in the partition, while `LAG` returns NULL if there is no preceding row.

Keep in mind that the availability of these functions may vary depending on the SQL database you are using. So, it's always a good practice to consult the database documentation for the precise syntax and usage.

Understanding the differences between `FIRST_VALUE` and `LAG` functions in SQL can be crucial for efficiently retrieving the required data and performing calculations on sequential values. Choose the one that suits your use case best and leverage its power to enhance your SQL queries. 

# References
- [Oracle Documentation - FIRST_VALUE](https://docs.oracle.com/en/database/oracle/oracle-database/21/sqlrf/FIRST_VALUE.html#GUID-0A361F12-8633-4A75-AF2E-0AFE5F967B4D)
- [Oracle Documentation - LAG](https://docs.oracle.com/en/database/oracle/oracle-database/21/sqlrf/LAG.html#GUID-20BC8E45-8C1D-4FD9-9062-5F7A01D7461A)