---
layout: post
title: "Comparing FIRST_VALUE vs. LAST_VALUE in SQL"
description: " "
date: 2023-10-26
tags: []
comments: true
share: true
---

When writing SQL queries, you may encounter situations where you need to retrieve the first or last value in a specific column within a group of records. In such cases, you have two functions at your disposal: `FIRST_VALUE` and `LAST_VALUE`.

Both `FIRST_VALUE` and `LAST_VALUE` are window functions that allow you to fetch the earliest or latest value within a group, based on a specific ordering. However, they differ in how they determine this value.

## FIRST_VALUE

The `FIRST_VALUE` function returns the value from the first row within a group, according to the specified order. It is commonly used to retrieve the initial state or starting point of a particular attribute.

Here's an example usage of `FIRST_VALUE`:

```sql
SELECT employee_id, salary, 
       FIRST_VALUE(salary) OVER (PARTITION BY department_id ORDER BY hire_date) AS starting_salary
FROM employees;
```

In this example, `FIRST_VALUE` is used to find the starting salary for each employee within their respective department, based on the hire date.

## LAST_VALUE

On the other hand, the `LAST_VALUE` function returns the value from the last row within a group, according to the specified order. It is often used to obtain the final state or the latest value of a certain attribute.

Let's take a look at an example of `LAST_VALUE`:

```sql
SELECT employee_id, salary, 
       LAST_VALUE(salary) OVER (PARTITION BY department_id ORDER BY hire_date) AS latest_salary
FROM employees;
```

In this query, `LAST_VALUE` is used to find the latest salary for each employee within their department, based on the hire date.

## Key Differences between FIRST_VALUE and LAST_VALUE

The primary difference between `FIRST_VALUE` and `LAST_VALUE` lies in the direction in which they fetch the value within a group. 

`FIRST_VALUE` retrieves the earliest value within a group, whereas `LAST_VALUE` fetches the latest value. 

Additionally, they also differ in their behavior when encountering multiple rows with the same value in the specified ordering. `FIRST_VALUE` will consistently return the same value for all rows with equal ordering values, whereas `LAST_VALUE` will change its value for each occurrence.

## Conclusion

In summary, both `FIRST_VALUE` and `LAST_VALUE` are useful window functions in SQL that allow you to fetch the earliest or latest value from a group of records based on a specific ordering. Understanding their differences is key to leveraging them effectively in your queries.

# References
- [Oracle Documentation - FIRST_VALUE](https://docs.oracle.com/cd/B19306_01/server.102/b14200/functions011.htm)
- [Oracle Documentation - LAST_VALUE](https://docs.oracle.com/cd/B12037_01/server.101/b10759/functions073.htm)

#hashtags: SQL, window functions