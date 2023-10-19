---
layout: post
title: "Using FIRST_VALUE to find the first occurrence of an employee name in a dataset"
description: " "
date: 2023-10-20
tags: [GUID, function]
comments: true
share: true
---

Often, when working with datasets, we need to find the first occurrence of a particular value within a group or a specific order. In SQL, the FIRST_VALUE function allows us to retrieve the first value of a specified column within a group or ordered set of rows.

Let's say we have a table called `employees` with the following structure:

| emp_id  | emp_name | department |
|---------|----------|------------|
| 1       | John     | Sales      |
| 2       | Amanda   | HR         |
| 3       | Sarah    | Marketing  |
| 4       | John     | Sales      |
| 5       | John     | HR         |

To find the first occurrence of an employee name in the dataset, we can use the FIRST_VALUE function in combination with the PARTITION BY clause. Here's an example query:

```sql
SELECT DISTINCT 
  emp_name,
  FIRST_VALUE(emp_id) OVER (
    PARTITION BY emp_name ORDER BY emp_id
  ) AS first_occurrence_id
FROM employees;
```

In the above query, we are selecting the distinct employee names along with their first occurrence employee ID. The PARTITION BY clause is used to group the rows by employee name, and the ORDER BY clause is used to specify the order of the rows within each group.

The FIRST_VALUE function will extract the first value of `emp_id` within each partition (group) based on the specified order. The result will include only the unique employee names and their corresponding first occurrence ID.

The result of the query for our example dataset will be:

| emp_name | first_occurrence_id |
|----------|---------------------|
| John     | 1                   |
| Amanda   | 2                   |
| Sarah    | 3                   |

By using the FIRST_VALUE function, we can easily retrieve the first occurrence of an employee name within a dataset. This can be helpful in various scenarios, such as identifying the earliest record, finding the first employee in terms of seniority, or determining the first customer in a sales dataset.

Remember to adapt the query according to your own table structure and field names.

# Conclusion

In this blog post, we explored how to use the FIRST_VALUE function in SQL to find the first occurrence of an employee name within a dataset. By leveraging the PARTITION BY and ORDER BY clauses in combination with the FIRST_VALUE function, we can efficiently extract the desired information. This technique can be handy in various analytical and reporting tasks. Next time you need to find the first occurrence of a value in a dataset, consider using the FIRST_VALUE function in SQL.

# References
- [SQL Server FIRST_VALUE Function](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql?view=sql-server-ver15)
- [Oracle FIRST_VALUE Function](https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/FIRST_VALUE.html#GUID-37241B06-2841-4A8D-9BAD-BB2319D0A2BB)
- [MySQL FIRST_VALUE Function](https://dev.mysql.com/doc/refman/8.0/en/window-function-descriptions.html#function_first-value)