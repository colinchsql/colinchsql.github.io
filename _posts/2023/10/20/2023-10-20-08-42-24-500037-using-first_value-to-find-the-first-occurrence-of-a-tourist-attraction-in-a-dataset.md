---
layout: post
title: "Using FIRST_VALUE to find the first occurrence of a tourist attraction in a dataset"
description: " "
date: 2023-10-20
tags: [DataAnalysis]
comments: true
share: true
---

When working with datasets that contain information about tourist attractions, it is often necessary to find the first occurrence of each attraction. This can be achieved using the `FIRST_VALUE` function in SQL.

The `FIRST_VALUE` function allows you to retrieve the first value from an ordered set of rows based on a specified column. It is commonly used in scenarios where you want to find the earliest or first occurrence of a particular attribute.

To demonstrate how to use the `FIRST_VALUE` function, let's assume we have a dataset called `attractions` with the following schema:

| attraction_id | attraction_name | city         | date_visited |
|---------------|-----------------|--------------|--------------|
| 1             | Statue of Liberty| New York City| 2021-01-15   |
| 2             | Eiffel Tower    | Paris        | 2020-08-05   |
| 3             | Great Wall of China| Beijing   | 2021-03-20   |
| 4             | Machu Picchu    | Cusco        | 2021-02-10   |
| 5             | Taj Mahal       | Agra         | 2020-12-01   |

We want to find the first occurrence of each tourist attraction based on the `date_visited` column.

The SQL query to achieve this using `FIRST_VALUE` would look like this:

```sql
SELECT DISTINCT
  attraction_id,
  FIRST_VALUE(attraction_name) OVER (PARTITION BY attraction_name ORDER BY date_visited) AS first_occurrence,
  city,
  date_visited
FROM attractions;
```

Let's break down the query:

- The `FIRST_VALUE` function is applied to the `attraction_name` column and ordered by `date_visited` within each partition of distinct attraction names.
- The `PARTITION BY` clause groups the dataset by the distinct values of `attraction_name`, creating partitions for each unique attraction.
- The `ORDER BY` clause sorts the rows within each partition based on the `date_visited` column in ascending order.
- The `DISTINCT` keyword ensures that each attraction appears only once in the result set.

The result of the above query would be:

| attraction_id | first_occurrence    | city         | date_visited |
|---------------|---------------------|--------------|--------------|
| 1             | Statue of Liberty   | New York City| 2021-01-15   |
| 2             | Eiffel Tower        | Paris        | 2020-08-05   |
| 3             | Great Wall of China | Beijing      | 2021-03-20   |
| 4             | Machu Picchu        | Cusco        | 2021-02-10   |
| 5             | Taj Mahal           | Agra         | 2020-12-01   |

By using the `FIRST_VALUE` function with the appropriate ordering, we were able to identify the first occurrence of each tourist attraction in the dataset.

[#SQL #DataAnalysis]