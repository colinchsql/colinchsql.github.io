---
layout: post
title: "Using FIRST_VALUE to find the first non-zero value in a dataset"
description: " "
date: 2023-10-20
tags: [references]
comments: true
share: true
---

In this tech blog post, we will explore how to use the `FIRST_VALUE` function to find the first non-zero value in a dataset. This can be particularly useful when analyzing numerical data and wanting to find the initial occurrence of a non-zero value.

## Table of Contents
- [Introduction](#introduction)
- [Syntax](#syntax)
- [Example](#example)
- [Conclusion](#conclusion)

## Introduction

The `FIRST_VALUE` function is a handy feature provided by many database management systems (DBMSs) like Oracle, SQL Server, and PostgreSQL, to name a few. It allows us to retrieve the first value from a set of records, based on a specified ordering, in this case, the order in which the records appear.

## Syntax

The syntax for using the `FIRST_VALUE` function is as follows:

```sql
FIRST_VALUE(column_name) OVER (
    PARTITION BY partition_column
    ORDER BY order_column
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
) AS first_value
```

- `column_name`: The name of the column from which we want to extract the first value.
- `partition_column`: (Optional) Provides partitioning of the data into separate groups. The `FIRST_VALUE` function will find the first non-zero value within each partition separately.
- `order_column`: Specifies the column(s) on which the ordering will be based.
- `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: Defines the range of rows we want the `FIRST_VALUE` function to consider. We want it to consider all the rows from the beginning until the current row.

## Example

Let's consider a fictional dataset of sales figures by month, where some months have zero sales. We want to find the first non-zero sales value for each product. Here's the sample data:

| Product  | Month     | Sales |
|----------|-----------|-------|
| Product1 | January   | 0     |
| Product1 | February  | 0     |
| Product1 | March     | 120   |
| Product2 | January   | 0     |
| Product2 | February  | 80    |
| Product2 | March     | 50    |
| Product2 | April     | 0     |

Now, let's write a SQL query to find the first non-zero sales value for each product:

```sql
SELECT 
    Product, 
    FIRST_VALUE(Sales) OVER (
        PARTITION BY Product
        ORDER BY Month
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS FirstNonZeroSales
FROM 
    SalesData
WHERE 
    Sales > 0;
```

The result of this query will be:

| Product  | FirstNonZeroSales |
|----------|------------------|
| Product1 | 120              |
| Product2 | 80               |

As you can see, the `FIRST_VALUE` function allows us to retrieve the first non-zero sales value for each product based on the month order.

## Conclusion

By using the `FIRST_VALUE` function in SQL, we can easily find the first non-zero value in a dataset. This can be particularly useful in scenarios where we need to analyze and extract specific information from our data. Understanding and utilizing such functionalities can greatly enhance our data analysis capabilities.

#references: