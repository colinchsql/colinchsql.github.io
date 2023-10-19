---
layout: post
title: "Using FIRST_VALUE to find the first occurrence of a hotel name in a dataset"
description: " "
date: 2023-10-20
tags: [WindowFunctions]
comments: true
share: true
---

When working with large datasets, it can be challenging to find specific information. In some cases, you may need to identify the first occurrence of a particular value within a dataset. In this blog post, we will explore how to use the `FIRST_VALUE` function in SQL to find the first occurrence of a hotel name in a dataset.

## Table of Contents
- [Introduction to FIRST_VALUE](#introduction-to-first_value)
- [Syntax of FIRST_VALUE function](#syntax-of-first_value-function)
- [Using FIRST_VALUE to find the first hotel name](#using-first_value-to-find-the-first-hotel-name)
- [Conclusion](#conclusion)

## Introduction to FIRST_VALUE

The `FIRST_VALUE` function is a window function in SQL that allows you to retrieve the first value in an ordered set of rows. It can be useful when you want to extract the first occurrence of a specific value within a dataset, based on a specific order.

## Syntax of FIRST_VALUE function

The syntax of the `FIRST_VALUE` function is as follows:

```sql
FIRST_VALUE(expression) OVER (PARTITION BY partition_expression ORDER BY sort_expression [ASC|DESC] ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
```

- `expression`: The column or expression for which you want to retrieve the first value.
- `partition_expression`: Optional. It divides the result set into partitions where the `FIRST_VALUE` function is independently calculated for each partition.
- `sort_expression`: Specifies the column or expression used to determine the order of the rows.
- `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: Defines the window frame of rows used by `FIRST_VALUE`. In this case, it includes all rows from the start of the partition up to the current row.

## Using FIRST_VALUE to find the first hotel name

Let's consider a dataset of hotel bookings, where each row represents a different booking. We want to find the first occurrence of each hotel name in the dataset.

Here's an example query that uses the `FIRST_VALUE` function to achieve this:

```sql
SELECT 
    hotel_name,
    FIRST_VALUE(hotel_name) OVER (ORDER BY booking_date ASC) AS first_occurrence
FROM 
    bookings
```

In the above query, we are selecting the hotel name column and applying the `FIRST_VALUE` function over the entire dataset, ordered by the booking date in ascending order. This will give us the first occurrence of each hotel name in the result set.

## Conclusion

The `FIRST_VALUE` function is a powerful tool for identifying the first occurrence of a specific value within a dataset. By using this function in SQL, you can easily extract the first occurrence of a hotel name or any other value based on a specific order. This can be particularly useful when analyzing large datasets and looking for specific information.

I hope this blog post has helped you understand how to use the `FIRST_VALUE` function. Happy querying!

\#SQL #WindowFunctions