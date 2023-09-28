---
layout: post
title: "SQL LAST_VALUE with DELETE statement"
description: " "
date: 2023-09-28
tags: [LAST_VALUE, DELETE]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function is used to retrieve the last value within a partition. By combining it with the `DELETE` statement, you can delete specific rows based on the last value of a column within a partition.

Let's consider a scenario where we have a table called `orders` with the following structure:

```sql
CREATE TABLE orders (
    id INT,
    order_number INT,
    order_date DATE
);
```

We want to delete all the orders that have the highest order number within each month. To achieve this, we can use the `LAST_VALUE` function along with a `DELETE` statement.

Here's an example of how you can accomplish this:

```sql
DELETE FROM orders 
WHERE id IN (
    SELECT id
    FROM (
        SELECT id, 
            LAST_VALUE(order_number) OVER (PARTITION BY EXTRACT(MONTH FROM order_date) ORDER BY order_number) AS last_order_number
        FROM orders
    ) subquery
    WHERE order_number = last_order_number
);
```

In the inner subquery, we use the `LAST_VALUE` function with the `PARTITION BY` clause to determine the last order number for each month. Then, in the outer query, we delete the rows where the order number matches the last order number for each month.

By using the `LAST_VALUE` function along with the `DELETE` statement, we can easily delete the records that have the highest order number within each month in our `orders` table.

#SQL #LAST_VALUE #DELETE