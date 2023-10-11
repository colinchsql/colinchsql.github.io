---
layout: post
title: "JOIN using EXCEPT operator"
description: " "
date: 2023-10-11
tags: []
comments: true
share: true
---

When working with relational databases, JOIN operations are used to combine data from multiple tables based on a common column. The EXCEPT operator is one such operation which can be used to perform a JOIN with some additional functionality.

The EXCEPT operator is used to return the distinct rows from the left table that do not exist in the right table. In other words, it returns the difference between the two tables. This can be useful when you want to find records that are present in one table but not in another.

Let's take a look at an example to understand how to use the EXCEPT operator in a JOIN operation. Suppose we have two tables - `customers` and `orders`.

## Example Scenario

**Table: customers**

| customer_id | customer_name |
|-------------|---------------|
| 1           | John          |
| 2           | Jane          |
| 3           | Mike          |
| 4           | Sarah         |

**Table: orders**

| order_id | customer_id | amount |
|----------|-------------|--------|
| 1001     | 1           | 50     |
| 1002     | 2           | 75     |
| 1003     | 4           | 100    |

Now, let's say we want to retrieve all the customers who have not placed any orders yet. We can accomplish this using the EXCEPT operator in a JOIN operation.

## SQL Query

```sql
SELECT customers.customer_id, customers.customer_name
FROM customers
LEFT JOIN orders ON customers.customer_id = orders.customer_id
WHERE orders.customer_id IS NULL;
```

Explanation of the SQL query:
- We select the `customer_id` and `customer_name` columns from the `customers` table.
- We perform a LEFT JOIN between the `customers` and `orders` tables using the `customer_id` column as the join condition.
- We add a WHERE clause to filter out rows where `orders.customer_id` is NULL. This condition ensures that only customers who have not placed any orders are included in the result.

The result of the above query will be:

| customer_id | customer_name |
|-------------|---------------|
| 3           | Mike          |

As you can see, the customer with `customer_id` 3 (Mike) is the only customer who hasn't placed any orders.

The EXCEPT operator in combination with the JOIN operation provides a powerful way to find the difference between two tables. It can be used in various scenarios depending on your specific requirements.