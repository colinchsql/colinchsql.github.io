---
layout: post
title: "SQL LAST_VALUE with numeric functions"
description: " "
date: 2023-09-28
tags: [NumericFunctions]
comments: true
share: true
---

In SQL, the `LAST_VALUE` function can be used to extract the last value in a column within a window of rows defined by an `ORDER BY` clause. This can be particularly useful with numeric functions to calculate running totals, find the maximum or minimum value in a window, or track changes in values over time.

Let's explore some examples of using the `LAST_VALUE` function with numeric functions.

## Example 1: Calculating a Running Total

Suppose you have a table called `sales` with columns `date`, `product`, and `quantity`. You want to calculate the running total of the quantity for each product over time.

```sql
SELECT
  date,
  product,
  quantity,
  LAST_VALUE(SUM(quantity)) OVER (PARTITION BY product ORDER BY date) AS running_total
FROM
  sales;
```
In this example, the `LAST_VALUE` function is used with the `SUM` function to calculate the running total of the `quantity` column for each `product` within the defined window ordered by `date`.

## Example 2: Finding the Maximum Value

Let's say you have a table called `sensor_data` with columns `timestamp` and `temperature`. You want to find the maximum temperature in a sliding window of the last 10 records.

```sql
SELECT
  timestamp,
  temperature,
  LAST_VALUE(temperature) OVER (ORDER BY timestamp ROWS BETWEEN 9 PRECEDING AND CURRENT ROW) AS max_temperature
FROM
  sensor_data;
```

In this example, the `LAST_VALUE` function is used to extract the value of the `temperature` column within the sliding window of the last 10 records, ordered by `timestamp`. This will give you the maximum temperature within the window.

## Conclusion

The `LAST_VALUE` function in SQL can be a powerful tool when combined with numeric functions. It allows you to extract the last value in a windowed set of rows, enabling calculations such as running totals, finding maximum or minimum values, or tracking changes over time. Understanding how to utilize this function can greatly enhance your data analysis capabilities. #SQL #NumericFunctions