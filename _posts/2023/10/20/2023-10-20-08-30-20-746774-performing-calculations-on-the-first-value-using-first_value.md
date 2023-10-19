---
layout: post
title: "Performing calculations on the first value using FIRST_VALUE"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

In SQL, `FIRST_VALUE` is a window function that allows you to perform calculations on the first value in a group of rows. It can be particularly useful when you want to calculate running totals, cumulative sums, or compare each row with the first row in a group.

The basic syntax of using `FIRST_VALUE` is as follows:

```
FIRST_VALUE(expression) OVER (PARTITION BY column ORDER BY column ASC/DESC)
```

Let's take a look at an example to demonstrate how `FIRST_VALUE` works:

```sql
SELECT category, product, price,
  FIRST_VALUE(price) OVER (PARTITION BY category ORDER BY price ASC) AS lowest_price
FROM products
```

In this example, we have a table called `products` that contains information about various products, including the category, product name, and price. We want to find the lowest price for each category.

By using `FIRST_VALUE(price) OVER (PARTITION BY category ORDER BY price ASC)`, we calculate the lowest price for each group of products within the same category. The `PARTITION BY` clause divides the rows into groups based on the category column, and the `ORDER BY` clause sorts the rows within each group by price in ascending order.

The result will include the original columns (category, product, price) and an additional column called `lowest_price`, which displays the first value (lowest price) for each category.

Using `FIRST_VALUE`, you can also perform other calculations based on the first value, such as finding the highest value, calculating the difference between each row and the first row, or determining if a row is equal to the first row.

Keep in mind that `FIRST_VALUE` is just one of many window functions available in SQL. You can explore other functions like `LAST_VALUE`, `LAG`, and `LEAD` to perform various calculations and comparisons on different rows within a group.

Now that you understand how to use `FIRST_VALUE` in SQL, you can leverage this powerful function to perform calculations and analysis on the first value in your data sets.

---

References:
- [SQL FIRST_VALUE() function](https://www.w3schools.com/sql/sql_top.asp)
- [Analytic Functions in Oracle SQL](https://www.oracletutorial.com/oracle-analytic-functions/oracle-first_value-function/)