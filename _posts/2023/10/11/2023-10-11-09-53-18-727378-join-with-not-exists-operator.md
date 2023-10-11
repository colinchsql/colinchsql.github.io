---
layout: post
title: "JOIN with NOT EXISTS operator"
description: " "
date: 2023-10-11
tags: [notexists]
comments: true
share: true
---

In SQL, the JOIN operation is used to combine rows from multiple tables based on a related column between them. The NOT EXISTS operator, on the other hand, is used to check if a subquery returns no rows.

In certain scenarios, we may want to retrieve records from one table that do not have a corresponding entry in another table. This is where the NOT EXISTS operator can be handy when used with the JOIN operation.

Here's an example to illustrate how to use the JOIN with a NOT EXISTS operator in SQL:

Let's consider two tables: `customers` and `orders`.

**Table: customers**

| customer_id | customer_name |
|-------------|---------------|
| 1           | John          |
| 2           | Jane          |
| 3           | Mark          |
| 4           | Emily         |

**Table: orders**

| order_id | customer_id | order_date |
|----------|-------------|------------|
| 1        | 2           | 2021-01-01 |
| 2        | 3           | 2021-02-14 |
| 3        | 4           | 2021-03-27 |

Suppose we want to find customers who have not placed any orders. We can achieve this using a combination of the JOIN and NOT EXISTS operators.

Here's the SQL query to achieve our goal:

```sql
SELECT c.customer_id, c.customer_name
FROM customers AS c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders AS o
    WHERE o.customer_id = c.customer_id
);
```

In the above query, we select customer_id and customer_name from the customers table. Then, using the NOT EXISTS operator, we check if there are no rows returned from the subquery, which selects orders based on the customer_id match.

The result of the above query will be:

| customer_id | customer_name |
|-------------|---------------|
| 1           | John          |

In this case, John is the only customer who has not placed any orders.

Using the JOIN with the NOT EXISTS operator allows us to filter the rows based on the absence of related records in another table efficiently.

This technique can be useful in various scenarios when we need to find rows that have no matching entries in a related table.

#sql #notexists