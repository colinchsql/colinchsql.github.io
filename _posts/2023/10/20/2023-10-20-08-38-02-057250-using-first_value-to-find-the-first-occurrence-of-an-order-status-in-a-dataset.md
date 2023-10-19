---
layout: post
title: "Using FIRST_VALUE to find the first occurrence of an order status in a dataset"
description: " "
date: 2023-10-20
tags: [References, GUID]
comments: true
share: true
---

When working with datasets, it is common to need to find the first occurrence of a particular value within a group. In SQL, the FIRST_VALUE function can be utilized to accomplish this task effectively. In this blog post, we will explore how to use the FIRST_VALUE function to find the first occurrence of an order status in a dataset.

## Table of Contents
- [Syntax of FIRST_VALUE](#syntax-of-first_value)
- [Example Usage](#example-usage)
- [Conclusion](#conclusion)

## Syntax of FIRST_VALUE

The syntax for using the FIRST_VALUE function is as follows:

```sql
FIRST_VALUE(<column>) OVER (
    [PARTITION BY <partition_column>]
    ORDER BY <order_by_column> [ASC | DESC]
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
)
```

- `<column>`: The column for which you want to find the first value.
- `<partition_column>` (optional): The column used to partition the dataset into groups. The function will find the first value within each group separately.
- `<order_by_column>`: The column used to determine the order of the dataset.
- `ASC | DESC`: Optional keyword specifying the order in which the dataset should be sorted. ASC (ascending) is the default.
- `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: Specifies the range of rows within which the function applies.

## Example Usage

Let's consider a simple table named `orders` representing online orders:

| order_id | order_status |
|----------|--------------|
| 1        | Pending      |
| 2        | Processing   |
| 3        | Processing   |
| 4        | Shipped      |

We want to find the first occurrence of each order status in the dataset.

Here is an example SQL query using the FIRST_VALUE function:

```sql
SELECT DISTINCT
  order_status,
  FIRST_VALUE(order_id) OVER (
    PARTITION BY order_status
    ORDER BY order_id ASC
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
  ) AS first_order_id
FROM
  orders;
```

The above query will return the following result:

| order_status | first_order_id |
|--------------|----------------|
| Pending      | 1              |
| Processing   | 2              |
| Shipped      | 4              |

In the result, the first_order_id column shows the first order_id for each order_status.

## Conclusion

The FIRST_VALUE function in SQL is a powerful tool for finding the first occurrence of a value in a dataset. It allows you to partition the dataset into groups and determine the order within each group. By understanding its syntax and usage, you can effectively extract the desired information from your datasets.

#References
1. [FIRST_VALUE Function - Microsoft Documentation](https://docs.microsoft.com/en-us/sql/t-sql/functions/first-value-transact-sql?view=sql-server-ver15)
2. [FIRST_VALUE Function - Oracle Documentation](https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/FIRST_VALUE.html#GUID-59DDC507-3D1A-479D-B3A2-1DBB319197CE)
3. [FIRST_VALUE Function - PostgreSQL Documentation](https://www.postgresql.org/docs/10/functions-window.html)