---
layout: post
title: "SQL LAST_VALUE with END statement"
description: " "
date: 2023-09-29
tags: [LASTVALUE]
comments: true
share: true
---

When working with SQL, you might come across situations where you need to fetch the last value from a column within a specific set of rows. The `LAST_VALUE` function in SQL is a powerful tool to achieve this.

The `LAST_VALUE` function retrieves the last value of an expression within a window frame in a specified order. With the addition of the `END` statement, you can further customize the behavior of the `LAST_VALUE` function.

Let's dive into an example to understand how to use `LAST_VALUE` with the `END` statement.

## Example Scenario

Consider a scenario where you have a table named `employees` that contains employee information such as `employee_id`, `employee_name`, and `salary`. You want to retrieve the last salary of each employee in ascending order by employee ID.

## SQL Query

To accomplish this, you can use the `LAST_VALUE` function with the `END` statement. Here's an example SQL query:

```sql
SELECT DISTINCT employee_id, 
    LAST_VALUE(salary) OVER (
        PARTITION BY employee_id 
        ORDER BY employee_id ASC
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
        ) AS last_salary
FROM employees;
```

Let's break down the query:

- `DISTINCT`: This keyword is used to retrieve unique combinations of `employee_id` and `last_salary`.
- `LAST_VALUE(salary)`: The `LAST_VALUE` function fetches the last salary value within the specified window frame.
- `PARTITION BY employee_id`: This clause partitions the data based on the unique employee IDs.
- `ORDER BY employee_id ASC`: The `ORDER BY` clause specifies the ascending order of employee IDs.
- `ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING`: This clause defines the range of rows included in the window frame.

## Output

Running the above query will yield a result similar to the following:

```
| employee_id | last_salary |
|-------------|-------------|
| 1001        | 5000        |
| 1002        | 8000        |
| 1003        | 6000        |
| 1004        | 7000        |
```

In the result set, you can see the last salary associated with each employee ID.

## Conclusion

The `LAST_VALUE` function with the `END` statement in SQL allows you to conveniently retrieve the last value of an expression within a specified window frame. By understanding and utilizing this function, you can efficiently analyze data and derive meaningful insights.

#SQL #LASTVALUE #END