---
layout: post
title: "Using FIRST_VALUE to find the first occurrence of a temperature in a dataset"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

When working with datasets, it's often necessary to find the first occurrence of a specific value. In this blog post, we'll explore how to use the `FIRST_VALUE` function in SQL to find the first occurrence of a temperature in a dataset.

### What is the FIRST_VALUE Function?

The `FIRST_VALUE` function is an analytic function in SQL that allows you to find the first value in a given set of data based on a specified order. It returns the value from the first row in the partition of the result set.

### Example Dataset

Let's consider a dataset containing temperature measurements of a city over multiple days. The dataset has two columns: `date` and `temperature`. We want to find the first occurrence of a temperature above 30 degrees Celsius.

|    date    | temperature |
|------------|-------------|
| 2021-01-01 |     25      |
| 2021-01-02 |     28      |
| 2021-01-03 |     30      |
| 2021-01-04 |     32      |
| 2021-01-05 |     35      |
| 2021-01-06 |     27      |

### Using FIRST_VALUE to Find the First Occurrence

To find the first occurrence of a temperature above 30 degrees Celsius in our dataset, we can use the `FIRST_VALUE` function along with the `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` clause. This ensures that only the first row with a temperature above 30 is returned.

```sql
SELECT DISTINCT 
    FIRST_VALUE(temperature) OVER (ORDER BY date) AS first_hot_day
FROM 
    temperatures
WHERE 
    temperature > 30
```

In the above SQL query, we use the `FIRST_VALUE` function with the `ORDER BY` clause to order the dataset by the `date` column. The `WHERE` clause filters the rows to only include temperatures above 30. The `DISTINCT` keyword is used to eliminate duplicate values.

### Result

The query will return the first occurrence of a temperature above 30 degrees Celsius. In our example dataset, the result will be:

| first_hot_day |
|---------------|
|      32       |

### Conclusion

The `FIRST_VALUE` function in SQL is a powerful tool for finding the first occurrence of a specific value in a dataset. In this blog post, we explored how to use it to find the first occurrence of a temperature above 30 degrees Celsius in a temperature dataset. By combining the `FIRST_VALUE` function with ordering and filtering, we were able to retrieve the desired result efficiently.

Using this technique, you can easily extract the first occurrence of any value in your dataset, opening up possibilities for various data analysis and business intelligence tasks.

---

**References**:
- [SQL FIRST_VALUE Function](https://www.sqlshack.com/sql-server-over-and-partition-by-clauses-in-t-sql/)