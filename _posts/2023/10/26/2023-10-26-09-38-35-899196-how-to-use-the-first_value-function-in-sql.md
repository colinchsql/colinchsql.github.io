---
layout: post
title: "How to use the FIRST_VALUE function in SQL"
description: " "
date: 2023-10-26
tags: [GUID, function]
comments: true
share: true
---

When working with SQL, there may be scenarios where you need to retrieve the first value from a specific column within a group of rows. This is where the `FIRST_VALUE` function comes in handy. In this blog post, we will explore how to use the `FIRST_VALUE` function in SQL and understand its syntax and use cases.

## Syntax of the `FIRST_VALUE` function
The syntax of the `FIRST_VALUE` function is as follows:

```sql
FIRST_VALUE(expression) OVER (PARTITION BY column ORDER BY sort_expression [ASC|DESC] ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
```

Let's break down the different components of this syntax:

- `expression`: This is the column or expression from which you want to retrieve the first value.
- `PARTITION BY column`: This is an optional clause that allows you to divide the result set into partitions based on the specified column. The calculation of the first value will be done within each partition.
- `ORDER BY sort_expression [ASC|DESC]`: This specifies the order in which the rows will be sorted before retrieving the first value. You can choose to sort the rows in ascending (`ASC`) or descending (`DESC`) order.
- `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: This defines the window frame within which the calculation will be done. In this case, it specifies that the first value will be calculated from the start of the partition (`UNBOUNDED PRECEDING`) up to and including the current row (`CURRENT ROW`).

## Example usage of the `FIRST_VALUE` function
Let's consider a scenario where you have a table named `sales` that contains information about sales transactions. You want to retrieve the first sale amount for each product within a specific date range. Here is an example query that demonstrates the use of the `FIRST_VALUE` function:

```sql
SELECT product_name, sale_date, sale_amount,
       FIRST_VALUE(sale_amount) OVER (PARTITION BY product_name
                                      ORDER BY sale_date ASC) AS first_sale_amount
FROM sales
WHERE sale_date BETWEEN '2021-01-01' AND '2021-12-31';
```

In this query, we select the `product_name`, `sale_date`, `sale_amount`, and also calculate the `first_sale_amount` using the `FIRST_VALUE` function. The result set will include the first sale amount for each product within the specified date range.

## Use cases of the `FIRST_VALUE` function
The `FIRST_VALUE` function is useful in various scenarios, such as:

- Identifying the first occurrence of an event within a group.
- Finding the earliest or oldest value in a time series.
- Calculating the first sale, transaction, or activity for each entity.

By using the `FIRST_VALUE` function, you can easily extract the desired information from your data sets and make informed decisions based on the first values within specific groups or time ranges.

## Conclusion
The `FIRST_VALUE` function in SQL provides a powerful way to retrieve the first value within a group or window. Understanding its syntax and use cases allows you to leverage this function effectively in your SQL queries. Whether you need to find the earliest value in a time series or retrieve the first sale amount within a group of products, the `FIRST_VALUE` function has got you covered.

Happy coding! 👩‍💻👨‍💻

_References:_
- [SQL Server FIRST_VALUE function](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql?view=sql-server-ver15)
- [Oracle Database FIRST_VALUE function](https://docs.oracle.com/en/database/oracle/oracle-database/21/sqlrf/FIRST_VALUE.html#GUID-63BEA83C-DAEF-48D5-82C5-FABAEDB330B9)
- [MySQL FIRST_VALUE function](https://dev.mysql.com/doc/refman/8.0/en/window-function-descriptions.html#function_first-value)