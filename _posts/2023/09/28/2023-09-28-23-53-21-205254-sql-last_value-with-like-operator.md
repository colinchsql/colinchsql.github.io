---
layout: post
title: "SQL LAST_VALUE with LIKE operator"
description: " "
date: 2023-09-28
tags: []
comments: true
share: true
---

In SQL, the `LAST_VALUE` function allows you to access the last value of an expression in a set of rows. By default, it returns the last value based on the ordering specified in the `ORDER BY` clause. However, when combined with the `LIKE` operator, you can perform pattern matching on the last value returned.

Let's see how you can use the `LAST_VALUE` function with the `LIKE` operator in SQL.

## Syntax

The basic syntax of the `LAST_VALUE` function with the `LIKE` operator is as follows:

```sql
LAST_VALUE ( expression ) 
  OVER ( 
    [ PARTITION BY partition_expression ] 
    ORDER BY sort_expression 
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
  )
  LIKE pattern;
```

The `expression` represents the column or expression you want to retrieve the last value from. The `PARTITION BY` clause allows you to partition the result set into groups based on specific columns. The `ORDER BY` clause specifies the ordering of the result set. The `ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING` clause ensures that the entire result set is considered.

## Example

Let's consider an example to demonstrate the usage of `LAST_VALUE` with the `LIKE` operator.

Suppose we have a table called `products` with the following structure:

```sql
CREATE TABLE products (
  id INT,
  name VARCHAR(100),
  category VARCHAR(100)
);
```

And it contains the following data:

```sql
| id |   name   | category |
|----|----------|----------|
| 1  | Laptop   | Electronics |
| 2  | Smartphone | Electronics |
| 3  | Headphones | Electronics |
| 4  | T-Shirt  | Clothing |
| 5  | Jeans    | Clothing |
```

If we want to find the last product name that ends with the letter "s" in each category, we can use the following query:

```sql
SELECT DISTINCT
  LAST_VALUE(name) 
    OVER (PARTITION BY category ORDER BY id
          ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
    LIKE '%s' AS last_product_ends_with_s,
  category
FROM
  products;
```

This query will return the following result:

```sql
| last_product_ends_with_s |   category   |
|--------------------------|--------------|
|        true              | Electronics  |
|        true              | Clothing     |
```

In the result, `true` indicates that the last product in the category ends with the letter "s".

## Conclusion

By combining the `LAST_VALUE` function with the `LIKE` operator in SQL, you can perform pattern matching on the last value returned from a result set. This can be useful in various scenarios where you need to identify specific patterns in your data.