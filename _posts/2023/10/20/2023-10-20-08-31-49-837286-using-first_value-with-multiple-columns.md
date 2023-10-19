---
layout: post
title: "Using FIRST_VALUE with multiple columns"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

In SQL, the `FIRST_VALUE` function is used to retrieve the first value within a group of rows based on a specified ordering. By default, `FIRST_VALUE` only returns the value from a single column. However, there are cases when you may need to include multiple columns in the result set. In this blog post, we'll explore how to use `FIRST_VALUE` with multiple columns in SQL.

## Table Setup

Let's start by creating a sample table to demonstrate the usage of `FIRST_VALUE` with multiple columns. Consider a table `sales` with the following structure:

```sql
CREATE TABLE sales (
  id INT,
  product_name VARCHAR(100),
  category VARCHAR(50),
  price DECIMAL(10, 2),
  sales_date DATE
);
```

We'll populate the table with some dummy data:

```sql
INSERT INTO sales (id, product_name, category, price, sales_date) VALUES
  (1, 'Product A', 'Electronics', 150.00, '2021-01-01'),
  (2, 'Product B', 'Clothing', 50.00, '2021-01-02'),
  (3, 'Product C', 'Electronics', 200.00, '2021-01-03'),
  (4, 'Product D', 'Clothing', 75.00, '2021-01-04'),
  (5, 'Product E', 'Electronics', 120.00, '2021-01-05'),
  (6, 'Product F', 'Clothing', 60.00, '2021-01-06');
```

## Using FIRST_VALUE with multiple columns

To include multiple columns along with `FIRST_VALUE`, we can make use of a subquery or a common table expression (CTE) in SQL. Here's an example that demonstrates how to retrieve the first sale of each product category along with the product name and price:

```sql
SELECT
  FIRST_VALUE(product_name) OVER (PARTITION BY category ORDER BY sales_date) AS first_product,
  FIRST_VALUE(price) OVER (PARTITION BY category ORDER BY sales_date) AS first_price
FROM sales;
```

In the above query, we use the `FIRST_VALUE` function with the `OVER` clause. The `PARTITION BY` clause is used to group the rows based on the `category` column, and the `ORDER BY` clause specifies the ordering based on the `sales_date` column.

## Result

The result of the query will be as follows:

```
| first_product | first_price |
|---------------|-------------|
| Product A     | 150.00      |
| Product B     | 50.00       |
| Product A     | 150.00      |
| Product B     | 50.00       |
| Product A     | 150.00      |
| Product B     | 50.00       |
```

As you can see, the query returns the first product and its corresponding price for each category.

## Conclusion

By using the `FIRST_VALUE` function in combination with the `OVER` clause and appropriate partitioning and ordering, we can retrieve the first value from multiple columns in SQL. This allows us to extract meaningful information from our data that can be used for analysis or reporting purposes.

Make sure to explore the capabilities of other window functions in SQL to further enhance your data querying capabilities.

# References
- [Microsoft SQL Docs - FIRST_VALUE function](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql?view=sql-server-ver15)
- [PostgreSQL Docs - Window Functions](https://www.postgresql.org/docs/current/tutorial-window.html)