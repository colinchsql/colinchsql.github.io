---
layout: post
title: "SQL LAST_VALUE with FETCH statement"
description: " "
date: 2023-09-29
tags: [SQLtips, FetchStatement]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to retrieve the last value from a specified column within a partition, based on the order specified in the `ORDER BY` clause. The `FETCH` statement can be used to limit the number of rows returned by a query. 

**Syntax:**
```sql
LAST_VALUE(expression) OVER (PARTITION BY column ORDER BY ordering_expression [ASC | DESC] 
                            [ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW])
```

Here's an example to demonstrate the usage of `LAST_VALUE` with the `FETCH` statement:

**Scenario:**
Suppose we have a table named `orders` that stores records of orders placed by customers. We want to retrieve the last order amount for each customer.

**SQL Query:**
```sql
SELECT customer_id, order_amount
FROM
    (SELECT customer_id, order_amount,
            ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date DESC) AS rn
     FROM orders) AS subquery
WHERE rn = 1
FETCH FIRST ROW ONLY;
```

**Explanation:**
- We use the inner query to assign a row number to each order for every customer, based on the order date in descending order.
- The outer query selects the `customer_id` and `order_amount` from the inner query, filtering only the rows with row number 1 (which corresponds to the last order for each customer).
- The `FETCH FIRST ROW ONLY` clause limits the result to only the first row.

By using the `LAST_VALUE` function in combination with the `FETCH` statement, we can efficiently retrieve the last value from a specific column within a partition. This can be very useful when working with large datasets or when analyzing time-series data.

#SQLtips #FetchStatement