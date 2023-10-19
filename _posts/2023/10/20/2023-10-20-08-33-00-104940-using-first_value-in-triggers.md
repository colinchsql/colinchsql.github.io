---
layout: post
title: "Using FIRST_VALUE in triggers"
description: " "
date: 2023-10-20
tags: [References]
comments: true
share: true
---

Triggers in databases allow developers to automatically execute code when certain events occur, such as updates, inserts, or deletes on a table. One common use case for triggers is to perform calculations or update values based on changes in the database.

In this blog post, we will explore how to use the `FIRST_VALUE` function in triggers. `FIRST_VALUE` is a window function that retrieves the first value in an ordered set of values within a specific partition. It can be useful in triggers to capture the initial value of a column before it is modified.

## Creating a Trigger

To demonstrate the usage of `FIRST_VALUE` in triggers, let's consider a scenario where we have a "orders" table with columns `order_id`, `order_amount`, and `order_status`. We want to track the initial status of an order whenever it is modified.

To achieve this, we can create a trigger that captures the first value of `order_status` using `FIRST_VALUE` and inserts it into a separate "order_history" table.

Here's an example of how to create such a trigger in SQL:

```sql
CREATE TRIGGER capture_order_status
AFTER UPDATE ON orders
FOR EACH ROW
WHEN (OLD.order_status <> NEW.order_status)
BEGIN
    INSERT INTO order_history (order_id, initial_status)
    VALUES (NEW.order_id, FIRST_VALUE(OLD.order_status) OVER (PARTITION BY NEW.order_id ORDER BY order_id));
END;
```

In the above example, the trigger is fired after an update occurs on the "orders" table. It checks if the `order_status` has changed (`OLD.order_status <> NEW.order_status`). If there is a change, it inserts the `order_id` and the first value of `order_status` into the "order_history" table using the `FIRST_VALUE` function.

## Testing the Trigger

To test the trigger, you can execute update statements on the "orders" table and observe the changes in the "order_history" table. For example:

```sql
UPDATE orders
SET order_status = 'Cancelled'
WHERE order_id = 123;
```

This update statement will trigger the `capture_order_status` trigger, and the initial status of the order will be stored in the "order_history" table.

## Conclusion

Using the `FIRST_VALUE` function in triggers allows developers to capture the initial value of a column before it is modified. This can be helpful in scenarios where you need to keep a history of changes in your database. By using triggers and window functions like `FIRST_VALUE`, you can automate the process of capturing such changes and storing them in separate tables.

#References:

- [SQL Triggers](https://www.w3schools.com/sql/sql_triggers.php)
- [FIRST_VALUE function](https://docs.oracle.com/database/121/SQLRF/functions013.htm)