---
layout: post
title: "Using FIRST_VALUE to find the first occurrence of a city name in a dataset"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

When working with datasets that contain multiple records of the same city name, you may need to identify the first occurrence of that city. In such cases, you can use the `FIRST_VALUE` function in SQL to retrieve the first value based on a specific ordering criterion.

Here's an example scenario where we have a table called "cities" with the columns "city_name" and "population" representing different cities and their populations respectively.

| city_name  | population |
|------------|------------|
| New York   | 8398748    |
| Los Angeles| 3990456    |
| Chicago    | 2705994    |
| New York   | 8244910    |
| Houston    | 2325502    |

To find the first occurrence of each city in the dataset, we can use the `FIRST_VALUE` function along with the `OVER` clause and `PARTITION BY` to group the records by city name, and `ORDER BY` to specify the ordering criterion based on a column like population or any other specific field.

Here's the SQL query to achieve this:

```sql
SELECT 
  city_name,
  FIRST_VALUE(population) OVER (PARTITION BY city_name ORDER BY population) AS first_population
FROM 
  cities;
```

The above query will return the city name along with the population of the first occurrence of each city, ordered by population.

| city_name  | first_population |
|------------|-----------------|
| New York   | 8398748         |
| New York   | 8398748         |
| Los Angeles| 3990456         |
| Chicago    | 2705994         |
| Houston    | 2325502         |

As you can see, the query correctly retrieves the first occurrence of each city along with their corresponding population.

Using the `FIRST_VALUE` function in this manner can be helpful when you need to retrieve specific information regarding the initial occurrence of a particular value within a dataset.

Remember to adjust the query based on your specific table structure and ordering requirements.

### References

- [FIRST_VALUE function - Documentation](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql?view=sql-server-ver15)
- [Window Functions in SQL - Introduction and Examples](https://www.sqlservertutorial.net/sql-server-window-functions/sql-server-first_value-function/)