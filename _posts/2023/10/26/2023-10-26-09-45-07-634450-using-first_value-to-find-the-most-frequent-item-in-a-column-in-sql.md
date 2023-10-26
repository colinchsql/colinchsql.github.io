---
layout: post
title: "Using FIRST_VALUE to find the most frequent item in a column in SQL"
description: " "
date: 2023-10-26
tags: [references]
comments: true
share: true
---

When working with large datasets, it is often necessary to find the most frequent item in a specific column. In SQL, there are several ways to accomplish this task. One approach is to use the FIRST_VALUE function, which allows us to retrieve the first value in a group based on a specific order.

## Syntax of the FIRST_VALUE function

The syntax for the FIRST_VALUE function in SQL is as follows:

```
FIRST_VALUE(expression) OVER (PARTITION BY column ORDER BY ordering_column)
```

- `expression`: The column or expression from which we want to retrieve the first value.
- `column`: The column that we want to group by.
- `ordering_column`: The column used to determine the order.

## Example Usage

Let's say we have a table called `customers` with the following schema:

```sql
CREATE TABLE customers (
  id INT,
  name VARCHAR(50),
  city VARCHAR(50)
);
```

To find the most frequent city in the `city` column, we can use the FIRST_VALUE function as follows:

```sql
SELECT DISTINCT
  FIRST_VALUE(city) OVER (ORDER BY COUNT(*) DESC) AS most_frequent_city
FROM
  customers
GROUP BY
  city;
```

In the above query, we use the COUNT(*) function to count the occurrences of each city in the `city` column. The ORDER BY clause ensures that the most frequent city appears first. The FIRST_VALUE function then retrieves the first city from the ordered list.

## Output

The result of the above query will be a single row containing the most frequent city in the `most_frequent_city` column.

```
most_frequent_city
-----------------
New York
```

In this example, "New York" is the most frequent city in the `city` column.

## Conclusion

The FIRST_VALUE function in SQL is a powerful tool for finding the most frequent item in a column. By combining it with other SQL functions like COUNT and GROUP BY, we can easily retrieve the desired result. Remember to adjust the column names and table names in the example to match your own database schema.

#references
- [SQL FIRST_VALUE function](https://www.w3schools.com/sql/sql_windowfunctions.asp)
- [SQL COUNT function](https://www.w3schools.com/sql/sql_count_avg_sum.asp)
- [SQL GROUP BY clause](https://www.w3schools.com/sql/sql_groupby.asp)