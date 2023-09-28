---
layout: post
title: "SQL LAST_VALUE with UPDATE statement"
description: " "
date: 2023-09-28
tags: []
comments: true
share: true
---

In SQL, the `LAST_VALUE` function can be used to retrieve the last value of a specified column within a group. This function is commonly used with the `UPDATE` statement to update a table with the last value of a column.

To demonstrate this, let's consider a table called `employees` with the following structure:

```sql
CREATE TABLE employees (
  id INT,
  name VARCHAR(50),
  salary INT
);
```

Now, suppose we want to update the `salary` column of all employees in the table with their last recorded salary. We can use the `LAST_VALUE` function along with the `UPDATE` statement to achieve this.

The `LAST_VALUE` function requires the use of the `OVER` clause to define the ordering of the rows within a group. In this case, we can order the rows by the `id` column to ensure that the last value is selected.

Here's an example SQL query that demonstrates how to update the `salary` column with the last recorded salary for each employee:

```sql
UPDATE employees
SET salary = LAST_VALUE(salary) OVER (ORDER BY id
                                      ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING);
```

In the above example, we specify the `id` column in the `ORDER BY` clause to ensure that the rows are ordered by the `id` column. The `ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING` clause ensures that the `LAST_VALUE` is calculated over all rows in the table.

By executing this SQL query, each employee's `salary` column in the `employees` table will be updated with their last recorded salary.

In conclusion, the `LAST_VALUE` function in SQL can be used with the `UPDATE` statement to update a table column with the last value of a specified column. This is achieved by utilizing the `OVER` clause to define the ordering of rows within a group.